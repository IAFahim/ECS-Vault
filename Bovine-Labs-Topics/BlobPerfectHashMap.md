### BlobPerfectHashMap

Creates zero-collision hash maps inside blob assets for instant lookups.

**Understanding & Use Case:** Standard hash maps handle collisions via chaining or probing, which adds a tiny overhead. `BlobPerfectHashMap` is built during baking to find a perfect distribution size where **zero collisions** occur. This guarantees absolute fastest theoretical $O(1)$ lookups.

**Use Case:** Highly trafficked core-loop data, such as a custom Physics Material lookup table accessed by every collision event every frame.

```csharp
using System;
using Unity.Burst;
using Unity.Collections;
using Unity.Entities;
using BovineLabs.Core.Collections;

public struct PerfectConfigBlob
{
    public BlobPerfectHashMap<int, float> DamageMultipliers;
}

public partial struct BlobPerfectHashMapExampleSystem : ISystem
{
    public void OnCreate(ref SystemState state)
    {
        using var tempMap = new NativeHashMap<int, float>(16, Allocator.Temp);
        tempMap.Add(1, 1.5f); // Headshot
        tempMap.Add(2, 0.5f); // Legshot

        var builder = new BlobBuilder(Allocator.Temp);
        ref var root = ref builder.ConstructRoot<PerfectConfigBlob>();

        // Will loop internally during bake to find a bucket size resulting in 0 collisions
        builder.ConstructPerfectHashMap(ref root.DamageMultipliers, tempMap, nullValue: -1f);

        var blobRef = builder.CreateBlobAssetReference<PerfectConfigBlob>(Allocator.Persistent);
        
        // Usage inside Job/Update:
        ref var perfectMap = ref blobRef.Value.DamageMultipliers;
        if (perfectMap.TryGetValue(1, out var multiplier))
        {
            // multiplier.Ref == 1.5f
        }
        
        blobRef.Dispose();
    }
}
```