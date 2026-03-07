### BlobBuilderExtensions

Simplifies allocating complex collections inside blob builders.

**Understanding & Use Case:** Building complex nested BlobAssets natively is very tedious involving strict pointer arithmetic. `BlobBuilderExtensions` provides straightforward methods like `AllocateHashMap`, `Construct`, and `Allocate` that dramatically simplify the code needed to bake arrays and maps into blobs.

**Use Case:** Writing a custom Baker that takes complex managed data (like Lists, Arrays, or Dictionaries of waypoints) and cleanly maps it into a BlobAsset.

```csharp
using System.Collections.Generic;
using Unity.Collections;
using Unity.Entities;
using BovineLabs.Core.Collections;

public struct WaypointNetworkBlob
{
    public BlobArray<float3> Waypoints;
    public BlobHashMap<int, int> NodeConnections;
}

public class BlobBuilderExtensionsExample
{
    public BlobAssetReference<WaypointNetworkBlob> BakeNetwork(List<Unity.Mathematics.float3> points, Dictionary<int, int> connections)
    {
        var builder = new BlobBuilder(Allocator.Temp);
        ref var root = ref builder.ConstructRoot<WaypointNetworkBlob>();

        using var nativePoints = new NativeArray<Unity.Mathematics.float3>(points.ToArray(), Allocator.Temp);

        // 1. Extension: Safely construct a BlobArray from a NativeArray automatically handling pointers
        builder.Construct(ref root.Waypoints, in nativePoints);

        // 2. Extension: Construct a BlobHashMap directly from a managed Dictionary!
        builder.ConstructHashMap(ref root.NodeConnections, connections);

        return builder.CreateBlobAssetReference<WaypointNetworkBlob>(Allocator.Persistent);
    }
}
```