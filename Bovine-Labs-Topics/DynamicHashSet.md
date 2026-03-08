### DynamicHashSet

Embeds a hash set directly into entity buffers.

**Understanding & Use Case:** An $O(1)$ lookup set embedded inside an entity buffer. It guarantees uniqueness of elements.

**Use Case:** Tracking unlocked abilities, achievements, or visited waypoints on a player entity without duplicating entries.

```csharp
using System;
using Unity.Burst;
using Unity.Entities;
using BovineLabs.Core.Iterators;

[InternalBufferCapacity(32)]
public struct UnlockedAbilitiesSet : IDynamicHashSet<int>
{
    public byte Value { get; }
}

public partial struct DynamicHashSetExampleSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        var entity = state.EntityManager.CreateEntity(typeof(UnlockedAbilitiesSet));
        var buffer = state.EntityManager.GetBuffer<UnlockedAbilitiesSet>(entity);
        
        var hashSet = buffer.InitializeHashSet<UnlockedAbilitiesSet, int>()
                            .AsHashSet<UnlockedAbilitiesSet, int>();

        int fireballId = 5;
        int dashId = 2;

        hashSet.Add(fireballId);
        hashSet.Add(dashId);
        
        // Adding again does nothing (returns false)
        bool addedAgain = hashSet.Add(fireballId); 

        // Extremely fast O(1) checks during gameplay
        if (hashSet.Contains(fireballId))
        {
            // Allow casting fireball
        }
    }
}
```