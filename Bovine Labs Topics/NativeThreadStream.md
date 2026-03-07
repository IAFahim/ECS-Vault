### NativeThreadStream

Avoids pre-allocating large arrays by using block-based thread-safe streaming.

**Understanding & Use Case:** Unity's built-in NativeStream requires you to know exactly how many items each thread will write beforehand (by iterating twice). NativeThreadStream bypasses this limitation, allowing you to write dynamically sized data from parallel jobs directly into thread-local blocks without prior counting.  

**Use Case:** Gathering an unknown number of target entities (e.g., raycast hits, visible enemies) from a parallel job into a single stream, then reading them back.



```CS
using Unity.Burst;
using Unity.Collections;
using Unity.Entities;
using BovineLabs.Core.Collections;
using Unity.Jobs;
using Unity.Transforms;

public partial struct NativeThreadStreamExampleSystem : ISystem
{
	[BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        // 1. Allocate the stream (TempJob since we pass to jobs)
        var threadStream = new NativeThreadStream(Allocator.TempJob);

        // 2. Schedule Writer Job
        var writeJob = new GatherActiveEntitiesJob
        {
            Writer = threadStream.AsWriter<Entity>() // Typed writer
        };
        var writeHandle = writeJob.ScheduleParallel(state.Dependency);

        // 3. Schedule Reader Job (Processes gathered data)
        var readJob = new ProcessGatheredEntitiesJob
        {
            Reader = threadStream.AsReader()
        };
        state.Dependency = readJob.Schedule(writeHandle);

        // 4. Dispose safely after jobs finish
        state.Dependency = threadStream.Dispose(state.Dependency);
    }

    [BurstCompile]
    private partial struct GatherActiveEntitiesJob : IJobEntity
    {
        public NativeThreadStream.Writer<Entity> Writer;

        private void Execute(Entity entity, in LocalTransform transform)
        {
            // E.g. only gather entities above y = 0
            if (transform.Position.y > 0)
            {
                Writer.Write(entity);
            }
        }
    }

    [BurstCompile]
    private struct ProcessGatheredEntitiesJob : IJob
    {
        [ReadOnly] public NativeThreadStream.Reader Reader;

        public void Execute()
        {
            // Reader iterates over exactly how many threads wrote data
            for (int i = 0; i < Reader.ForEachCount; i++)
            {
                int count = Reader.BeginForEachIndex(i);
                for (int j = 0; j < count; j++)
                {
                    Entity e = Reader.Read<Entity>();
                    // Process entity...
                }
                Reader.EndForEachIndex();
            }
        }
    }
}
```