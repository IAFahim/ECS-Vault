### DynamicMultiHashMap

Embeds a multi-value hash map into entity buffers.

**Understanding & Use Case:** Similar to `DynamicHashMap`, but allows storing multiple values against a single key, right inside an entity's dynamic buffer.
**Use Case:** A buff/debuff system. An entity might have multiple status effects applied by the same caster (Key = Caster Entity ID, Value = Effect ID).

```csharp
using System;
using Unity.Burst;
using Unity.Entities;
using BovineLabs.Core.Iterators;

[InternalBufferCapacity(64)]
public struct BuffMultiHashMap : IDynamicMultiHashMap<int, int>
{
    public byte Value { get; }
}

public partial struct DynamicMultiHashMapExampleSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        var entity = state.EntityManager.CreateEntity(typeof(BuffMultiHashMap));
        var buffer = state.EntityManager.GetBuffer<BuffMultiHashMap>(entity);
        
        // Initialize
        var multiMap = buffer.InitializeMultiHashMap<BuffMultiHashMap, int, int>()
                             .AsMultiHashMap<BuffMultiHashMap, int, int>();

        // Add multiple effects (Value) from the same source caster (Key)
        int casterId = 99;
        multiMap.Add(casterId, 10); // Poison
        multiMap.Add(casterId, 12); // Slow

        // Iterate over all buffs applied by this specific caster
        var enumerator = multiMap.GetValuesForKey(casterId);
        while (enumerator.MoveNext())
        {
            int buffId = enumerator.Current;
            // Apply buff logic...
        }
    }
}
```