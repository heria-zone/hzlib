# HZLib — Architecture Decision Records

The canonical ADRs for HZLib live in the [reboot-lovely-robot monorepo](https://github.com/heria-zone/reboot-lovely-robot/tree/main/docs/development/decisions). They are not duplicated here to avoid maintenance drift.

## HZLib-Relevant ADRs

| ADR | Title | Summary |
|---|---|---|
| ADR_003 | Entity Hierarchy Foundation | Establishes the initial `NativeEntity` / `NativeEntityFamily` hierarchy |
| ADR_009 | Entity Hierarchy Refactoring | Refines the three-tier entity class structure |
| ADR_010 | Animation Profile System | Introduces `AnimationProfile`, `AnimationPool`, `SelectionStrategy`, `LoopBehavior` — the pure-Java animation declaration layer |
| ADR_011 | Variant and Spawn System Refactoring | String-based variant system, `TextureVariantFeature`, `SizeVariantFeature` |
| ADR_012 | InternalEntity Consolidation | Consolidates the shared entity base — precursor to ADR_018 rename |
| ADR_015 | EmanationFeature | Rule-based passive ability system (`EmanationFeature`, `EmanationRule`, `EmanationCondition`) |
| ADR_017 | OverlayFeature | Multi-slot composited layer renderer (`OverlayFeature`, `OverlaySlot`, `SlotMode`) |
| ADR_018 | Ecosystem Terminology and Rename | Full `Internal*` → canonical name rename; establishes Family / Variant / Appearance vocabulary |
| ADR_019 | Entity Data Pipeline | `DataCompound`, `DataField<T>`, `EntityDataSchema`, `MigrationChain` — version-agnostic NBT pipeline |
| ADR_020 | Conditional Appearance Feature | `ConditionalAppearanceFeature` — runtime condition-based appearance switching |
| ADR_021 | Composite Appearance Feature | `CompositeAppearanceFeature` — layered appearance composition |
| ADR_022 | Animation System Unification | `BoneVisibilityFeature`, `IdleSlot`, `IdleCondition`, `headBoneName` on `NativeEntityFamily`, animation missing-wire fix |

## Reading Order

If you are new to HZLib's architecture, read in this order:

1. `docs/architecture/HZLib-EntityType-Architecture.md` — entity framework overview
2. ADR_018 — understand the naming conventions before reading any code
3. ADR_010 — animation profile system
4. ADR_019 — data pipeline
5. ADR_022 — animation unification (most recent major change)
6. `docs/api/` — feature-specific API documentation
