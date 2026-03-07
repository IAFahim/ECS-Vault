### DynamicVariableMap

Maps keys to multiple variable columns within dynamic buffers.

**Understanding & Use Case:** Maps a key to multiple columns/values, similar to a database table or a struct of arrays (SoA), but hosted entirely inside a dynamic buffer.

**Use Case:** AI perception memory. The Key is the `TargetEntity`, Column 1 is the `LastSeenPosition` (float3), Column 2 is the `ThreatLevel` (int).

```csharp
using System;
using Unity.Burst;
using Unity.Entities;
using Unity.Mathematics;
using BovineLabs.Core.Iterators;
using BovineLabs.Core.Iterators.Columns;

[InternalBufferCapacity(256)]
public struct AiMemoryMap : IDynamicVariableMap<int, float3, int, MultiHashColumn<int>>
{
    public byte Value { get; }
}

public partial struct DynamicVariableMapExampleSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        var entity = state.EntityManager.CreateEntity(typeof(AiMemoryMap));
        var buffer = state.EntityManager.GetBuffer<AiMemoryMap>(entity);
        
        var varMap = buffer.InitializeVariableMap<AiMemoryMap, int, float3, int, MultiHashColumn<int>>()
                           .AsVariableMap<AiMemoryMap, int, float3, int, MultiHashColumn<int>>();

        int targetEntityId = 104;
        
        // Add Key (TargetId), Value (LastPosition), Column1 (ThreatLevel)
        varMap.Add(targetEntityId, new float3(10, 0, 10), 5);

        // Retrieve the data
        if (varMap.TryGetValue(targetEntityId, out float3 position, out int threatLevel))
        {
            // position = (10,0,10), threatLevel = 5
        }
    }
}
```
