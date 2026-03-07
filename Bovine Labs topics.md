
|     |     |
| --- | --- |
|     |     |

Topic,Description
NativeThreadStream,Avoids pre-allocating large arrays by using block-based thread-safe streaming.  
DynamicHashMap,Embeds a hash map directly into entity buffers avoiding external allocations.  
DynamicMultiHashMap,Embeds a multi-value hash map into entity buffers.  
DynamicHashSet,Embeds a hash set directly into entity buffers.  
DynamicUntypedBuffer,Stores mixed unmanaged types manually inside a single dynamic buffer.  
DynamicVariableMap,Maps keys to multiple variable columns within dynamic buffers.  
BlobHashMap,Embeds read-only hash maps entirely inside BlobAssetReference data.  
BlobPerfectHashMap,Creates zero-collision hash maps inside blob assets for instant lookups.  
BlobCurve,Bakes Unity AnimationCurves into BlobAssets for fast Burst evaluation.  
BlobBuilderExtensions,Simplifies allocating complex collections inside blob builders.  
PooledNativeList,Eliminates NativeList allocation overhead by reusing TLS-based memory pools.  
NativeCounter,Provides a Burst-compatible thread-safe counter for parallel jobs.  
NativeKeyedMap,Optimizes hash map performance by specifically targeting integer keys.  
NativeLinearCongruentialGenerator,Provides extremely fast procedural random generation directly in Burst.  
NativeParallelMultiHashMapFallback,Prevents map capacity exceptions by spilling over into a fallback queue.  
NativePartialKeyedMap,Highly constrained integer map optimized for extreme performance needs.  
ThreadList,Avoids lock contention by using thread-local storage for temporary lists.  
ThreadRandom,Avoids state conflicts by using thread-local random generators.  
UnmanagedPool,Enables blazing fast unmanaged object pooling using spin locks.  
UnsafeArray,Bypasses NativeArray structural overhead for internal fast paths.  
UnsafeSlabAllocator,Prevents memory fragmentation using fast block-based chunk allocations.  
BitArray256,Replaces booleans with compact bitmasks for SIMD and memory efficiency.  
FixedArray,Provides fixed-size array structs without unsafe fixed buffer limitations.  
MemoryLabelAllocator,Tracks ECS memory allocations tightly using custom profiler labels.  
AabbExtensions,Provides fast mathematical expansion and shrinking of bounding boxes.  
ArchetypeChunk.DidChange,Safely checks component versions without triggering false dependencies.  
ArchetypeChunk.GetNativeArrayReadOnly,Bypasses change filters when reading chunk data for optimization.  
ArchetypeChunk.GetDynamicBufferAccessor,Retrieves untyped buffers from raw chunks safely.  
BufferAccessor.GetUnsafe,Bypasses safety checks to read buffers faster internally.  
BufferLookup.GetROAndChunk,Retrieves both buffer data and chunk index simultaneously.  
ComponentLookup.GetOptionalComponentDataRW,Safely retrieves component pointers that might not exist.  
ComponentLookup.SetChangeFilter,Manually marks a component changed without modifying its data.  
EntityQueryBuilder.WithAllRW,Provides a cleaner shorthand for building read-write queries.  
EntityQuery.QueryHasSharedFilter,Efficiently checks if a query filters by a specific SharedComponent.  
EntityQuery.ReplaceSharedComponentFilter,Swaps SharedComponent filters instantly without rebuilding queries.  
EntityQuery.GetFirstEntity,Provides an unsafe fast path for fetching the first matched entity.  
EntityQuery.GetSingletonBufferNoSync,Skips dependency sync overhead when reading singleton buffers.  
IJobParallelForDeferExtensions,Schedules deferred jobs directly using dynamic buffer lengths.  
ListExtensions.AddRangeNative,Quickly copies NativeArrays directly into managed Lists.  
MathematicsExtensions.Encapsulate,Merges AABBs purely mathematically without Unity bounds overhead.  
NativeHashMapExtensions.GetOrAddRef,Returns references to map values avoiding double-lookup costs.  
NativeHashMapExtensions.ClearAndAddBatchUnsafe,Mass-populates hash maps bypassing safety checks for speed.  
NativeListExtensions.ReserveNoResize,Thread-safe block allocation directly inside a NativeList.  
NativeStreamExtensions.WriteLarge,Safely writes massive continuous data blocks into NativeStreams.  
SystemState.GetSingletonEntity,Retrieves singleton entities easily directly from SystemState.  
SystemState.GetManagedSingleton,Enables retrieving managed class components as singletons.  
World.IsClientWorld,Simplifies checking Netcode client and server topological states.  
IJobChunkWorkerBeginEnd,Adds setup and teardown hooks per thread in chunk jobs.  
IJobForThread,Divides work evenly by thread count rather than item count.  
IJobHashMapDefer,Defers hash map iterations until previous parallel jobs resolve.  
IJobParallelForDeferBatch,Uses custom batch sizes for deferred parallel array processing.  
KSettingsBase,Compiles string-based settings into fast byte keys for Burst.  
ConfigVarAttribute,Binds CLI arguments and editor prefs directly to SharedStatic variables.  
ConfigVarManager,Automatically parses and applies configurations at runtime startup.  
SharedStaticStringContainer,Safely bridges managed strings to FixedStrings inside Burst.  
MemoryAllocator,Simplifies tracking and freeing multiple complex unmanaged allocations.  
Ptr,Wraps void pointers in a struct making them equitable for collections.  
CopyEnableable,Synchronizes enableable component states automatically between two components.  
TimerFixed,Decrements fixed float timers across chunks highly efficiently.  
TimerEnableable,Automatically disables entities when their timer component reaches zero.  
TimerTriggerResetJob,Resets timer values across entire chunks in bulk.  
StateFlagModel,Manages bitmask-based state machines adding or removing tag components.  
StateModelEnableable,Toggles enableable components for states instead of structural changes.  
StateModelWithHistory,Maintains a ring buffer of previous states allowing easy rollbacks.  
StatefulCollisionEvent,Converts immediate physics collisions into persistent enter stay exit states.  
StatefulTriggerEvent,Converts immediate physics triggers into persistent enter stay exit states.  
CalculateEventMapBucketsJob,Dynamically optimizes physics event hash maps in parallel.  
AlwaysUpdatePhysicsWorld,Forces spatial map updates independently of the fixed simulation tick.  
SubSceneLoadData,Provides granular component control over when SubScenes stream in.  
SubSceneEntity,Tracks the actual internal entities spawned by loaded SubScenes.  
AssetLoad,Defers heavy GameObject asset loading safely within ECS systems.  
GameObjectCleanup,Automatically destroys hybrid GameObjects after ECS conversion finishes.  
ObjectDefinition,Maps ScriptableObjects to ECS entity IDs automatically at bake time.  
ObjectGroupMatcher,Uses optimized hash sets to check if entities belong to groups.  
ObjectId,Wraps integer IDs inside a struct for type-safe ECS identification.  
UIDAttribute,Provides a custom inspector to assign guaranteed unique IDs.  
BurstTrampoline,Calls managed delegates from Burst compiled jobs using unmanaged pointers.  
BurstUtil.IsEmpty,Checks entity query emptiness directly inside Burst jobs.  
ButtonEvent,Consumes and produces boolean events safely across systems.  
CodecService,Wraps LZ4 compression and decompression directly for NativeArrays.  
CommandLineArgs,Fetches CLI arguments instantly without allocating new string arrays.  
CurveRemapUtility,Normalizes AnimationCurves to clip lengths using pure mathematics.  
DebugUtil.SplitInt,Splits floats into integers allowing debugging logs inside Burst.  
Deserializer,Provides a high-performance unmanaged byte array reader.  
Serializer,Provides a high-performance unmanaged byte array writer.  
EnableMaskCreator,Manually constructs EnabledMasks allowing custom enableable iteration.  
EntityLock,Provides per-entity spin locks allowing parallel localized component writes.  
GlobalRandom,Provides globally accessible random generators per thread in Burst.  
HSV,Native math implementation converting HSV values to RGB Colors.  
HalfSizeTriangleMatrix,Optimizes 2D distance matrix storage by halving required memory.  
InitSystemBase,Automatically removes initialization systems from update loops after running.  
IntersectionTests,Provides fast AABB-Triangle intersection math strictly for Burst.  
LibraryLoader,Wraps cross-platform unmanaged DLL loading for Unity ECS.  
LimitedRateNoCatchUpManager,Creates fixed timestep managers that prevent simulation death spirals.  
ConvexHullBuilder,Native implementation of QuickHull for runtime mesh generation.  
MeshSimplifier,Provides runtime mesh decimation entirely using Burst.  
TerrainToMesh,Converts Unity Terrains to native meshes asynchronously using jobs.  
NoAllocHelpers,Uses unsafe utilities to resize managed Lists without allocations.  
PhysicsLayerUtil,Converts Collider masks accurately into ECS CollisionFilters.

Pin,Pins managed objects to access raw byte data securely.  
PolygonUtility,Burst-compatible polygon area and clockwise or counter-clockwise checks.  
QueryEntityEnumerator,Manual chunk iteration using UnsafeChunkCacheIterator and v128 masks.  
ReflectionUtility,Caches reflection lookups to avoid runtime allocation overhead.  
ShortHalfUnion,Memory overlap union for fast casting between short and half.  
IntFloatUnion,Memory overlap union for zero-cost casting between int and float.  
SpinLock,Custom fast spinlock using Interlocked.CompareExchange for ECS thread synchronization.  
SubSceneUtil,Simplifies checking SubScene streaming states directly via ECS components.  
SyncEnableStateUtil,Synchronizes enableable states between two different components efficiently.  
TimeProfiler,Low-overhead custom Unity profiler marker wrapping ProfilerUnsafeUtility.Timestamp.  
TransformUtility,Calculates LocalToWorld manually including PostTransformMatrix inside Burst jobs.  
TypeManagerEx,Caches component type names as FixedString128Bytes using SharedStatic for logging.  
TypeManagerOverrides,Overrides internal TypeManager buffer capacities and enableable flags during baking.  
TypeManagerUtil,Resolves WriteGroup components programmatically into enableable or normal component arrays.  
TypeUtility,Helpers to match and extract open generic arguments from types.  
WorldUtility,Filters out internal advanced worlds to return only live gameplay worlds.  
WriteGroupMatcher,Evaluates chunk components against a write group mask dynamically.  
mathex.mod,Returns the true mathematical modulus of two numbers instead of remainder.  
mathex.minMax,SIMD accelerated vector array bounds calculation using float4 intrinsics.  
mathex.add,SIMD accelerated integer array additions across memory blocks.  
mathex.GenerateGaussianNoise,Box-Muller transform for Burst-compiled standard normal distribution.  
mathex.FromToRotation,Computes the shortest quaternion rotation between two vectors in Burst.  
Worlds,Constants for WorldSystemFilterFlags targeting Server Client Menu or Service worlds.  
GhostComponentAttribute,Optimization flag controlling which Ghost variants include specific components.  
GhostFieldAttribute,Optimization flags dictating Netcode quantization and smoothing actions.  
ReflectionTestHelper,Sets private fields via reflection to facilitate deep ECS unit testing.  
TestLeakDetectionAttribute,Custom NUnit attribute to pinpoint memory leaks in ECS tests.  
BakerExtensions.AddEnabledComponent,Adds a component and sets its enableable state in one call.  
BakerExtensions.AddEnabledBuffer,Adds a buffer and sets its enableable state simultaneously.  
PhysicsMassOverrideAuthoring,Forces rigidbodies into kinematic states using custom baking rules.  
RemovePhysicsVelocityAuthoring,Strips PhysicsVelocity components during the baking phase cleanly.  
BakerCommands,Wraps IBaker into IEntityCommands for shared instantiation utility functions.  
AuthoringSettingsUtility,Locates and caches ScriptableObject settings safely during the baking process.  
SettingsAuthoring,Bakes multiple SettingsBase ScriptableObjects into generic singleton entities.  
TagAuthoring,Bakes arbitrary empty component tags onto entities using an inspector array.  
TransformAuthoring,Explicitly overrides TransformUsageFlags for an entity directly in the baker.  
AssemblyBuilderWindow,Automates generating asmdef files enforcing DisableAutoTypeRegistration.  
ChangeFilterTrackingSystem,Monitors DidChange triggers globally detecting inefficient chunk change filters.  
ComponentAssetBaseDrawer,Custom property drawer for picking ECS component types via assets.  
TypeSearchProvider,Quick Search provider specifically filtering for unmanaged ECS component types.  
ConfigVarPanel,Renders SharedStatic variables automatically into debug UIs using UI Toolkit.  
CoreBuildSetup,Injects custom SettingsSingleton objects into the preloaded assets list automatically.  
CreateEditorWorld,Lazy initializes the default ECS world explicitly for editor tool usage.  
EditorMenus.DataModeHierarchySet,Forces Hierarchy windows to switch DOTS Data Modes programmatically.  
InspectorSearch,Injects a search bar directly into the ECS GameObject inspector window.  
SelectedEntityEditorSystem,Synchronizes the Editor's active GameObject selection into an ECS singleton.  
AssemblyGraphWindow,Visualizes ECS package dependencies to detect circular or incorrect data flow.  
ComponentDependencyWindow,Maps exactly which ECS systems read or write specific component types.  
SystemDependencyWindow,Maps which ECS systems directly depend on other systems via components.  
CoreEditorPreferencesProvider,Leverages Unity SettingsProvider for generic ECS-related tooling preferences.  
GameObjectHelper.AddAuthoringComponent,Adds generated Authoring components to GameObjects via Editor scripts.  
SerializedHelper.IterateAllChildren,Flattens and iterates SerializedObjects while safely skipping m_Script properties.  
TextAssetHelper,Creates and updates binary TextAsset files directly from NativeArray byte data.  
BitFieldAttributeEditor,Renders integer bitmasks as multi-select dropdowns in the Inspector.  
BlobAssetOwnerInspector,Visualizes raw BlobAssetBatch pointer memory data directly in the Editor.  
HalfDrawer,Provides custom Inspector GUI for half and half-vector mathematics types.  
InlineObjectProperty,Inlines ScriptableObject editors directly into their parent's inspector view.  
MinMaxAttributeDrawer,Renders a min-max slider specifically customized for Vector2 ECS fields.  
PrefabElementEditor,Redirects inspector changes on an instance directly to the source prefab.  
StableTypeHashAttributeDrawer,Dropdown selecting ECS component types saving their StableTypeHash as ulong.  
ToggleOption,UI Toolkit element synchronizing a boolean toggle with an ECS configuration field.  
UnityObjectRefInspector,Resolves and renders UnityObjectRef pointers back to the original Unity asset.  
WeakObjectReferenceInspector,Renders WeakObjectReference fields seamlessly within the ECS component inspector.  
EntitySelection.GetAllSelectionsInWorld,Maps Unity instance IDs to ECS entities efficiently via EntityGuid.  
LoadPrefabsAsEntities,Editor tool intercepting prefab imports to load them directly as entities.  
ReloadToolbarButton,Injects domain and subscene reload buttons into the Unity main toolbar.  
WelcomeWindow,Custom dashboard for enabling ECS extension features and defining compiler flags.  
BaseObjectWindow,Abstract UI Toolkit foundation designed for creating robust ECS debugging lists.  
FeatureToggle,UI element specifically designed to toggle C# compiler defines for ECS.  
PrefabInstance,Instantiates prefabs directly as entities bypassing standard SubScene overhead.  
EntityBlobBakedData,Injects baked blobs into BlobAssetStore safely during the PostBaking phase.  
EntityBlobBakingSystem,Merges scattered baked blob data into a single BlobPerfectHashMap component.  
CloneTransformAuthoring,Automatically mirrors a specific entity's LocalTransform onto another via component.  
LifeCycleAuthoring,Prepares entities with init and destroy tags for managed lifecycle phases.  
LookupAuthoring,Maps Unity types to DynamicHashMap components on a manager entity.  
ObjectDefinitionAuthoring,Bakes ScriptableObject configurations into bitmask ECS category fields.  
SubSceneEditorSet,Differentiates SubScenes that only load in the editor for testing purposes.  
MainToolbarPresetPostProcessor,IL weaving tool to inject Unity internal toolbar attributes automatically.  
AnalyzersProjectFileGeneration,Upgrades Unity csproj files to include custom Roslyn Analyzers configurations.  
InitializeAllOnLoadExt,Centralizes ECS editor initialization hooks avoiding multiple domain reload triggers.  
ComponentInspectorWindow,Allows inspecting ECS components mapped to ScriptableObject data definitions.  
ObjectInstantiate.Editor,Tracks ObjectChangeEvents to dynamically swap instances in the editor hierarchy.  
StartupSceneSwap,Overrides the active loaded scene immediately upon entering Play Mode.  
SubSceneEditorSystem,Intercepts and overrides SubScene load lists based on debug toggles.  
SubSceneEditorToolbar,Adds quick-toggles for loading/unloading SubScenes directly to the main toolbar.  
SubScenePrebakeSystem,Preloads specific SubScenes automatically using SceneSectionStreamingSystem in the editor.  
ViewModelToolbar,Extracts and displays active UI Toolkit ViewModels for immediate debugging.  
CloneTransformSystem,Copies LocalTransform values from a target entity to another every frame.  
AfterSceneSystemGroup,Ideal placement for systems initializing entities just streamed from SubScenes.  
AfterTransformSystemGroup,Executes simulation systems that read but do not write transforms.  
BeforeTransformSystemGroup,Executes simulation systems that explicitly write or modify transforms.  
BeginSimulationSystemGroup,Best phase for polling user input before fixed step simulations execute.  
InstantiateCommandBufferSystem,Special ECB system dedicated to pre-scene entity instantiation tasks.  
DestroyEntityCommandBufferSystem,Final ECB in the frame strictly dedicated to entity destruction cleanup.  
DestroyEntitySystem,Centralized system batching entity destruction preventing scattered synchronization points.  
DestroyOnDestroySystem,Propagates destruction recursively down LinkedEntityGroup hierarchies efficiently.  
DestroyOnSubSceneUnloadSystem,Flags entities for destruction exactly when their parent SubScene unloads.  
DestroyTimer,Utility tracking float timers and tagging entities for destruction at zero.  
EndInitializeEntityCommandBufferSystem,ECB system playing back structural changes immediately after entity initialization.  
InitializeEntitySystem,Clears the InitializeEntity tag automatically after the initialization group runs.

Pin,Pins managed objects to access raw byte data securely.  
PolygonUtility,Burst-compatible polygon area and clockwise or counter-clockwise checks.  
QueryEntityEnumerator,Manual chunk iteration using UnsafeChunkCacheIterator and v128 masks.  
ReflectionUtility,Caches reflection lookups to avoid runtime allocation overhead.  
ShortHalfUnion,Memory overlap union for fast casting between short and half.  
IntFloatUnion,Memory overlap union for zero-cost casting between int and float.  
SpinLock,Custom fast spinlock using Interlocked.CompareExchange for ECS thread synchronization.  
SubSceneUtil,Simplifies checking SubScene streaming states directly via ECS components.  
SyncEnableStateUtil,Synchronizes enableable states between two different components efficiently.  
TimeProfiler,Low-overhead custom Unity profiler marker wrapping ProfilerUnsafeUtility.Timestamp.  
TransformUtility,Calculates LocalToWorld manually including PostTransformMatrix inside Burst jobs.  
TypeManagerEx,Caches component type names as FixedString128Bytes using SharedStatic for logging.  
TypeManagerOverrides,Overrides internal TypeManager buffer capacities and enableable flags during baking.  
TypeManagerUtil,Resolves WriteGroup components programmatically into enableable or normal component arrays.  
TypeUtility,Helpers to match and extract open generic arguments from types.  
WorldUtility,Filters out internal advanced worlds to return only live gameplay worlds.  
WriteGroupMatcher,Evaluates chunk components against a write group mask dynamically.  
mathex.mod,Returns the true mathematical modulus of two numbers instead of remainder.  
mathex.minMax,SIMD accelerated vector array bounds calculation using float4 intrinsics.  
mathex.add,SIMD accelerated integer array additions across memory blocks.  
mathex.GenerateGaussianNoise,Box-Muller transform for Burst-compiled standard normal distribution.  
mathex.FromToRotation,Computes the shortest quaternion rotation between two vectors in Burst.  
Worlds,Constants for WorldSystemFilterFlags targeting Server Client Menu or Service worlds.  
GhostComponentAttribute,Optimization flag controlling which Ghost variants include specific components.  
GhostFieldAttribute,Optimization flags dictating Netcode quantization and smoothing actions.  
ReflectionTestHelper,Sets private fields via reflection to facilitate deep ECS unit testing.  
TestLeakDetectionAttribute,Custom NUnit attribute to pinpoint memory leaks in ECS tests.  
BakerExtensions.AddEnabledComponent,Adds a component and sets its enableable state in one call.  
BakerExtensions.AddEnabledBuffer,Adds a buffer and sets its enableable state simultaneously.  
PhysicsMassOverrideAuthoring,Forces rigidbodies into kinematic states using custom baking rules.  
RemovePhysicsVelocityAuthoring,Strips PhysicsVelocity components during the baking phase cleanly.  
BakerCommands,Wraps IBaker into IEntityCommands for shared instantiation utility functions.  
AuthoringSettingsUtility,Locates and caches ScriptableObject settings safely during the baking process.  
SettingsAuthoring,Bakes multiple SettingsBase ScriptableObjects into generic singleton entities.  
TagAuthoring,Bakes arbitrary empty component tags onto entities using an inspector array.  
TransformAuthoring,Explicitly overrides TransformUsageFlags for an entity directly in the baker.  
AssemblyBuilderWindow,Automates generating asmdef files enforcing DisableAutoTypeRegistration.  
ChangeFilterTrackingSystem,Monitors DidChange triggers globally detecting inefficient chunk change filters.  
ComponentAssetBaseDrawer,Custom property drawer for picking ECS component types via assets.  
TypeSearchProvider,Quick Search provider specifically filtering for unmanaged ECS component types.  
ConfigVarPanel,Renders SharedStatic variables automatically into debug UIs using UI Toolkit.  
CoreBuildSetup,Injects custom SettingsSingleton objects into the preloaded assets list automatically.  
CreateEditorWorld,Lazy initializes the default ECS world explicitly for editor tool usage.  
EditorMenus.DataModeHierarchySet,Forces Hierarchy windows to switch DOTS Data Modes programmatically.  
InspectorSearch,Injects a search bar directly into the ECS GameObject inspector window.  
SelectedEntityEditorSystem,Synchronizes the Editor's active GameObject selection into an ECS singleton.  
AssemblyGraphWindow,Visualizes ECS package dependencies to detect circular or incorrect data flow.  
ComponentDependencyWindow,Maps exactly which ECS systems read or write specific component types.  
SystemDependencyWindow,Maps which ECS systems directly depend on other systems via components.  
CoreEditorPreferencesProvider,Leverages Unity SettingsProvider for generic ECS-related tooling preferences.  
GameObjectHelper.AddAuthoringComponent,Adds generated Authoring components to GameObjects via Editor scripts.  
SerializedHelper.IterateAllChildren,Flattens and iterates SerializedObjects while safely skipping m_Script properties.  
TextAssetHelper,Creates and updates binary TextAsset files directly from NativeArray byte data.  
BitFieldAttributeEditor,Renders integer bitmasks as multi-select dropdowns in the Inspector.  
BlobAssetOwnerInspector,Visualizes raw BlobAssetBatch pointer memory data directly in the Editor.  
HalfDrawer,Provides custom Inspector GUI for half and half-vector mathematics types.  
InlineObjectProperty,Inlines ScriptableObject editors directly into their parent's inspector view.  
MinMaxAttributeDrawer,Renders a min-max slider specifically customized for Vector2 ECS fields.  
PrefabElementEditor,Redirects inspector changes on an instance directly to the source prefab.  
StableTypeHashAttributeDrawer,Dropdown selecting ECS component types saving their StableTypeHash as ulong.  
ToggleOption,UI Toolkit element synchronizing a boolean toggle with an ECS configuration field.  
UnityObjectRefInspector,Resolves and renders UnityObjectRef pointers back to the original Unity asset.  
WeakObjectReferenceInspector,Renders WeakObjectReference fields seamlessly within the ECS component inspector.  
EntitySelection.GetAllSelectionsInWorld,Maps Unity instance IDs to ECS entities efficiently via EntityGuid.  
LoadPrefabsAsEntities,Editor tool intercepting prefab imports to load them directly as entities.  
ReloadToolbarButton,Injects domain and subscene reload buttons into the Unity main toolbar.  
WelcomeWindow,Custom dashboard for enabling ECS extension features and defining compiler flags.  
BaseObjectWindow,Abstract UI Toolkit foundation designed for creating robust ECS debugging lists.  
FeatureToggle,UI element specifically designed to toggle C# compiler defines for ECS.  
PrefabInstance,Instantiates prefabs directly as entities bypassing standard SubScene overhead.  
EntityBlobBakedData,Injects baked blobs into BlobAssetStore safely during the PostBaking phase.  
EntityBlobBakingSystem,Merges scattered baked blob data into a single BlobPerfectHashMap component.  
CloneTransformAuthoring,Automatically mirrors a specific entity's LocalTransform onto another via component.  
LifeCycleAuthoring,Prepares entities with init and destroy tags for managed lifecycle phases.  
LookupAuthoring,Maps Unity types to DynamicHashMap components on a manager entity.  
ObjectDefinitionAuthoring,Bakes ScriptableObject configurations into bitmask ECS category fields.  
SubSceneEditorSet,Differentiates SubScenes that only load in the editor for testing purposes.  
MainToolbarPresetPostProcessor,IL weaving tool to inject Unity internal toolbar attributes automatically.  
AnalyzersProjectFileGeneration,Upgrades Unity csproj files to include custom Roslyn Analyzers configurations.  
InitializeAllOnLoadExt,Centralizes ECS editor initialization hooks avoiding multiple domain reload triggers.  
ComponentInspectorWindow,Allows inspecting ECS components mapped to ScriptableObject data definitions.  
ObjectInstantiate.Editor,Tracks ObjectChangeEvents to dynamically swap instances in the editor hierarchy.  
StartupSceneSwap,Overrides the active loaded scene immediately upon entering Play Mode.  
SubSceneEditorSystem,Intercepts and overrides SubScene load lists based on debug toggles.  
SubSceneEditorToolbar,Adds quick-toggles for loading/unloading SubScenes directly to the main toolbar.  
SubScenePrebakeSystem,Preloads specific SubScenes automatically using SceneSectionStreamingSystem in the editor.  
ViewModelToolbar,Extracts and displays active UI Toolkit ViewModels for immediate debugging.  
CloneTransformSystem,Copies LocalTransform values from a target entity to another every frame.  
AfterSceneSystemGroup,Ideal placement for systems initializing entities just streamed from SubScenes.  
AfterTransformSystemGroup,Executes simulation systems that read but do not write transforms.  
BeforeTransformSystemGroup,Executes simulation systems that explicitly write or modify transforms.  
BeginSimulationSystemGroup,Best phase for polling user input before fixed step simulations execute.  
InstantiateCommandBufferSystem,Special ECB system dedicated to pre-scene entity instantiation tasks.  
DestroyEntityCommandBufferSystem,Final ECB in the frame strictly dedicated to entity destruction cleanup.  
DestroyEntitySystem,Centralized system batching entity destruction preventing scattered synchronization points.  
DestroyOnDestroySystem,Propagates destruction recursively down LinkedEntityGroup hierarchies efficiently.  
DestroyOnSubSceneUnloadSystem,Flags entities for destruction exactly when their parent SubScene unloads.  
DestroyTimer,Utility tracking float timers and tagging entities for destruction at zero.  
EndInitializeEntityCommandBufferSystem,ECB system playing back structural changes immediately after entity initialization.  
InitializeEntitySystem,Clears the InitializeEntity tag automatically after the initialization group runs.