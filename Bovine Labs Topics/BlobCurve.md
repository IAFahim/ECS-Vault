# BlobCurve

Bakes Unity AnimationCurves into BlobAssets for fast Burst evaluation.

**Understanding & Use Case:** Unity's `AnimationCurve` is a managed object and cannot be passed into Burst jobs. `BlobCurve` converts the math of an `AnimationCurve` into pure unmanaged blob data (cubic bezier splines) that is incredibly fast to evaluate in Burst.

**Use Case:** Evaluating recoil patterns, tweening UI, or calculating damage falloff over distance inside highly parallelized `IJobEntity`.

```csharp
using Unity.Entities;
using Unity.Collections;
using Unity.Burst;
using UnityEngine;
using BovineLabs.Core.Collections;

public struct RecoilPattern : IComponentData
{
    public BlobAssetReference<BlobCurve> YAxisRecoil;
}

public class BlobCurveBaker : Baker<UnityEngine.Transform> // Pseudo-baker example
{
    public AnimationCurve SourceCurve;

    public override void Bake(UnityEngine.Transform authoring)
    {
        // BovineLabs conversion from AnimationCurve to BlobCurve
        var blobRef = BlobCurve.Create(SourceCurve, Allocator.Persistent);
        
        var entity = GetEntity(TransformUsageFlags.Dynamic);
        AddComponent(entity, new RecoilPattern { YAxisRecoil = blobRef });
    }
}

public partial struct BlobCurveEvaluationSystem : ISystem
{
    [BurstCompile]
    public void OnUpdate(ref SystemState state)
    {
        // Create a job to evaluate the curve
        new EvaluateRecoilJob { Time = (float)SystemAPI.Time.ElapsedTime }.ScheduleParallel();
    }

    [BurstCompile]
    private partial struct EvaluateRecoilJob : IJobEntity
    {
        public float Time;

        private void Execute(in RecoilPattern recoil)
        {
            // Evaluate the curve safely inside burst
            // We use the Sampler to cache the last node for much faster sequential reads
            var sampler = new BlobCurveSampler(recoil.YAxisRecoil);
            float recoilOffset = sampler.Evaluate(Time);
            
            // Apply recoilOffset...
        }
    }
}
```