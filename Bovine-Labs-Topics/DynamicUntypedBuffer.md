### DynamicUntypedBuffer

Stores mixed unmanaged types manually inside a single dynamic buffer.

**Understanding & Use Case:** ECS `DynamicBuffer<T>` only allows one specific struct type. `DynamicUntypedBuffer` acts like an unmanaged memory stream, allowing you to sequentially pack completely different struct types into a single buffer.

**Use Case:** An Event Queue or Command Buffer on a specific entity. E.g., An entity received a `DamageEvent` (8 bytes) and a `KnockbackEvent` (12 bytes) in the same frame.

```csharp
using Unity.Burst;
using Unity.Entities;
using Unity.Mathematics;
using BovineLabs.Core.Iterators;

public struct DamageEvent { public int Amount; }
public struct KnockbackEvent { public float3 Direction; }

[InternalBufferCapacity(128)]
public struct EntityEventQueue : IDynamicUntypedBuffer
{
    public byte Value { get; }
}

public unsafe partial struct UntypedBufferExampleSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        var entity = state.EntityManager.CreateEntity(typeof(EntityEventQueue));
        var buffer = state.EntityManager.GetBuffer<EntityEventQueue>(entity);
        
        var untypedBuffer = buffer.InitializeUntypedBuffer<EntityEventQueue>()
                                  .AsUntypedBuffer<EntityEventQueue>();

        // Add different structs to the same buffer
        untypedBuffer.Add(new DamageEvent { Amount = 50 });
        untypedBuffer.Add(new KnockbackEvent { Direction = math.up() });

        // Retrieve them (Requires you to know the order, usually done by reading a header ID first in real usage)
        ref readonly DamageEvent dmg = ref untypedBuffer.ElementAtRO<DamageEvent>(0);
        ref readonly KnockbackEvent kb = ref untypedBuffer.ElementAtRO<KnockbackEvent>(1);
    }
}
```