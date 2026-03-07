### 2. DynamicHashMap

Embeds a hash map directly into entity buffers avoiding external allocations.

**Understanding & Use Case:** Standard `DynamicBuffer<T>` is a flat array, meaning looking up a specific element is $O(N)$. `DynamicHashMap` uses the raw bytes of a `DynamicBuffer` to store a fully functional Hash Map directly *inside* the entity.
**Use Case:** An RPG inventory system where an entity needs fast $O(1)$ lookups to check the quantity of a specific Item ID.

```csharp
using System;
using Unity.Burst;
using Unity.Entities;
using BovineLabs.Core.Iterators;

// 1. Define the buffer element implementing the BovineLabs interface
[InternalBufferCapacity(64)]
public struct InventoryHashMap : IDynamicHashMap<int, int>
{
    // Required by interface for memory layout
    public byte Value { get; }
}

public partial struct DynamicHashMapExampleSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        // Example: Initializing and using the map
        var entity = state.EntityManager.CreateEntity(typeof(InventoryHashMap));
        
        // 2. Initialize and get the HashMap view
        var buffer = state.EntityManager.GetBuffer<InventoryHashMap>(entity);
        var hashMap = buffer.InitializeHashMap<InventoryHashMap, int, int>(capacity: 16)
                            .AsHashMap<InventoryHashMap, int, int>();

        // 3. O(1) operations directly inside the buffer
        hashMap.AddOrSet(101 /* Item ID */, 5 /* Quantity */);
        hashMap.AddOrSet(202, 10);

        if (hashMap.TryGetValue(101, out int quantity))
        {
            // quantity is 5
        }
        
        // You can iterate over it like a normal map
        foreach (var kvp in hashMap)
        {
            int itemId = kvp.Key;
            int count = kvp.Value;
        }
    }
}
```