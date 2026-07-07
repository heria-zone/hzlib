# Changelog

All notable changes to HZLib will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

---

## [1.0.0] - 2026-07-04

### Changed (Breaking — ADR_018)

All `Internal*` class names have been replaced with canonical names reflecting
the Family / Variant / Appearance three-tier terminology. Any code built against
0.1.0-alpha must update imports.

**Common module:**

| Old name | New name |
|---|---|
| `InternalEntity` | `NativeEntity` |
| `InternalEntityType<T>` | `NativeEntityFamily<T>` |
| `InternalLogic` | `EntityLogic` |
| `InternalParticle` | `EntityParticles` |
| `InternalLayerRenderer<T>` | `LayerRenderPipeline<T>` |

**Loader modules (Fabric / Forge / NeoForge):**

| Old name | New name |
|---|---|
| `InternalAnimation` | `NativeAnimation` |
| `InternalModel<T>` | `NativeModel<T>` |
| `InternalLayerRenderer<T>` | `NativeRenderer<T>` |

Deferred (not yet renamed):
- `IInternalRenderLayer` — render layer interface
- `nativeEntity` field on `NativeEntity`

### Added

**NBT Data Pipeline (ADR_019)**
- `DataCompound` — pure-Java version-agnostic NBT wrapper; zero MC-native imports in pipeline code. MC-version-specific implementations live in version-scoped source sets.
- `NbtAdapterFactory` — registration point for the MC-version-specific `DataCompound` implementation
- `CompoundTagDataCompound` — 1.21.1 `CompoundTag` implementation of `DataCompound`
- `DataType<T>` — `INT`, `FLOAT`, `BOOLEAN`, `STRING`, `UUID`. UUID storage is version-safe; the adapter handles `putUUID()` vs two-long format automatically.
- `DataField<T>` — typed NBT field handles. String key encapsulated — zero literals at call sites. Typos are compile errors, not silent defaults.
- `EntityDataSchema` — ordered registry of `DataField<?>` handles. Write and read via `DataCompound`; no field name strings in `addAdditionalSaveData` / `readAdditionalSaveData`.
- `MigrationStep` / `MigrationChain` — sole migration authority. Steps receive and return `DataCompound`, enabling cross-field migration. Per-field migrators deliberately excluded.
- `FieldValueProvider` / `FieldValueConsumer` — typed interfaces for entity ↔ schema communication
- `McVersionProvider` — runtime MC version string provider for `McVersion` field in saved data

**Bone Visibility System (ADR_022 Change A)**
- `BoneVisibilityFeature` — declarative per-bone show/hide rules on `NativeEntityFamily`; evaluated each frame in `NativeModel.setCustomAnimations()`. Replaces reflection-based bone access.
- `BoneCondition` — `@FunctionalInterface` predicate; evaluated client-side per render frame
- `BoneRule` — pairs bone name with `BoneCondition` and hide/show polarity

**Idle Slot Animation System (ADR_022 Change D)**
- `IdleCondition` — `@FunctionalInterface` evaluated per locomotion controller tick
- `IdleSlot` — pairs `AnimationPool` with `IdleCondition`, priority, and activation threshold in ticks
- `idleStationaryTicks` field on `NativeEntity` — monotonic counter; incremented while entity is not moving and not in a vehicle; reset on movement
- `onIdleSlotChanged()` hook on `NativeEntity` — called when winning idle slot changes; override in subclasses to react (e.g. refresh hitbox dimensions on sit/stand)
- `AnimationProfile.idleSlots` — `idleSlot()` builder method; `.idle()` shorthand implicitly creates priority-0 always-true zero-threshold fallback slot

**Appearance System (ADR_020, ADR_021)**
- `ConditionalAppearanceFeature` — switches active appearance based on runtime conditions against entity state
- `CompositeAppearanceFeature` — composes multiple appearance layers into a single resolved appearance

**`NativeEntityFamily` additions (ADR_022 Change B)**
- `headBoneName` field — configurable head bone name for look-tracking in `NativeModel.setCustomAnimations()`. All existing families default to `"head"` — zero migration required. Set via `.headBone(String)`.

### Fixed

- `AnimationStateManager.resolveProfile()` returning `null` for all entities — `AnimationProfile` was attached as a family feature only; Step 1 of the resolver does not check features. Profile must be passed directly into `StandardAnimatorVariant` at registration time. (ADR_022 Change C)

### Deprecated

- `hzlib.api.entity.dynamic.*` — legacy variant system, zero consumers outside this package. Candidates for deletion in a future cleanup release.
- `hzlib.api.entity.monsters.*` — stub implementations extending `dynamic.*`, zero consumers. Candidates for deletion.

---

## [0.1.0-alpha] - 2026-06-24

Initial public release.

### Added

**Entity Framework**
- `NativeEntity` (then named `InternalEntity`) — root entity base with `finalizeSpawn()` lifecycle hook
- `NativeEntityFamily<T>` (then `InternalEntityType<T>`) — family descriptor with feature composition, stat configuration, variant management
- `EntityFeature` — composable feature system via `withFeature(Class, Feature)`

**Variant System**
- `TextureVariantFeature`, `ModelVariantFeature`, `AnimatorVariantFeature` — data-driven variant registration
- `SizeVariantFeature` with `SizeConfig` — dynamic hitbox per pose, stat multipliers, O(1) HashMap lookup
- `AnimatorVariantFeature` supports optional `AnimationProfile` per variant (backward compatible)

**Animation Profile System**
- `AnimationProfile` — named slots (idle, walk, rest, sit, ride, attack, hurt) with full builder API and null-safe `getAnimationForState()` fallback
- `AnimationPool`, `WeightedAnimation`, `SelectionStrategy` (RANDOM, WEIGHTED_RANDOM, SEQUENTIAL), `LoopBehavior`
- `AnimationSequence`, `SequenceStep`, `SequenceState` — pull-model exit conditions via `Predicate<LivingEntity>`
- `ISpecialAnimation` marker interface
- Zero GeckoLib or Minecraft imports in core profile classes

**Progression and Combat**
- `LevelFeature`, `CombatLevelFeature` — entity levelling with attribute scaling
- `LinearAttributeStrategy`, `ExponentialAttributeStrategy` — pluggable scaling curves
- `ProtectionFeature`, `LevelBasedProtectionStrategy`, `EnchantmentProtectionCalculator`

**Platform Services**
- `IPlatformServices` — cross-loader abstraction for registration, config, events, networking
- `Services` — service locator

**Utilities**
- Math, NBT, validation, and config bounds utilities in Common module

[Unreleased]: https://github.com/heria-zone/hzlib/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/heria-zone/hzlib/compare/v0.1.0-alpha...v1.0.0
[0.1.0-alpha]: https://github.com/heria-zone/hzlib/releases/tag/v0.1.0-alpha
