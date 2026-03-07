### BlobHashMap

Embeds read-only hash maps entirely inside BlobAssetReference data.

**Understanding & Use Case:** Native collections like `NativeHashMap` can't be stored in components and require disposal. `BlobHashMap` allows you to bake a fully functional, read-only hash map directly into a `BlobAssetReference`, which can be shared across all jobs/threads endlessly.

**Use Case:** Baking global game configuration, like a dictionary mapping `ItemTypeID` to its base `ItemStats`.

```csharp
using System;
using Unity.Burst;
using Unity.Collections;
using Unity.Entities;
using BovineLabs.Core.Collections;

public struct ItemStats { public int MaxStack; public float Weight; }

public struct GlobalItemConfig : IComponentData
{
    public BlobAssetReference<ConfigBlob> Blob;
}

public struct ConfigBlob
{
    public BlobHashMap<int, ItemStats> ItemDictionary;
}

public partial struct BlobHashMapExampleSystem : ISystem
{
    public void OnCreate(ref SystemState state)
    {
        using var tempMap = new NativeParallelHashMap<int, ItemStats>(16, Allocator.Temp);
        tempMap.Add(1, new ItemStats { MaxStack = 99, Weight = 0.1f });
        tempMap.Add(2, new ItemStats { MaxStack = 1, Weight = 5.0f });

        var builder = new BlobBuilder(Allocator.Temp);
        ref var root = ref builder.ConstructRoot<ConfigBlob>();

        // Extension from BovineLabs to easily move NativeHashMap into BlobHashMap
        builder.ConstructHashMap(ref root.ItemDictionary, ref tempMap);

        var blobRef = builder.CreateBlobAssetReference<ConfigBlob>(Allocator.Persistent);
        
        var entity = state.EntityManager.CreateEntity();
        state.EntityManager.AddComponentData(entity, new GlobalItemConfig { Blob = blobRef });
    }

    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        var config = SystemAPI.GetSingleton<GlobalItemConfig>();
        ref var map = ref config.Blob.Value.ItemDictionary;

        // O(1) thread-safe lookup directly from blob memory
        if (map.TryGetValue(1, out var ptrToStats))
        {
            int stack = ptrToStats.Ref.MaxStack; // 99
        }
    }
}
```
