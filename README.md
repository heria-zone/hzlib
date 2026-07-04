<p align="center">
    <b>HZLib</b>
</p>

<p align="center">
    Shared multi-loader library for Heria Zone mods — Fabric, Forge, and NeoForge
</p>

<p align="center">
    <a href="https://modrinth.com/mod/hzlib">
        <img alt="Modrinth" src="https://img.shields.io/modrinth/dt/hzlib?logo=Modrinth">
    </a>
    <a href="https://discord.gg/KdZZMj89bU">
        <img alt="Discord" src="https://img.shields.io/discord/1156134479149158402?logo=Discord">
    </a>
</p>

<p align="center">
    <a href="https://github.com/heria-zone/reboot-lovely-robot/issues">Issues</a> ·
    <a href="#what-it-provides">What It Provides</a> ·
    <a href="#version-support">Version Support</a> ·
    <a href="#for-mod-developers">For Mod Developers</a>
</p>

---

> **⚠️ In Development**
> HZLib is in active development and has not reached a stable API release. Breaking changes may occur between alpha versions. Not recommended for third-party mods until the API is frozen.

---

## About

HZLib is the shared foundation that all Heria Zone mods are built on. It provides a loader-agnostic entity framework, variant system, animation profiles, and platform abstractions — written once, working across Forge, NeoForge, and Fabric without duplication.

If you're playing a Heria Zone mod, this is the engine underneath it. It does nothing on its own.

---

## What It Provides

### Entity Framework
- `InternalEntityType<T>` — base entity type with feature composition, stat configuration, and variant management
- `InternalEntity` — base entity class with `finalizeSpawn()` lifecycle hook
- `EntityFeature` — composable feature system via `withFeature(Class, Feature)`

### Variant System
- `TextureVariantFeature`, `ModelVariantFeature`, `AnimatorVariantFeature` — data-driven variant registration
- `SizeVariantFeature` with `SizeConfig` — dynamic hitbox management, per-pose `EntityDimensions`, stat multipliers, O(1) lookup
- `AnimatorVariantFeature` supports optional `AnimationProfile` per variant

### Animation Profile System
- `AnimationProfile` — named animation slots (idle, walk, rest, sit, ride, attack, hurt) with full builder API and null-safe fallback
- `AnimationPool`, `WeightedAnimation`, `SelectionStrategy` (RANDOM, WEIGHTED_RANDOM, SEQUENTIAL), `LoopBehavior`
- `AnimationSequence` — pull-model exit conditions via `Predicate<LivingEntity>`
- Pure Java core — zero GeckoLib or Minecraft imports in profile classes

### Progression and Combat
- `LevelFeature`, `CombatLevelFeature` — entity levelling with attribute scaling
- `LinearAttributeStrategy`, `ExponentialAttributeStrategy` — pluggable scaling curves
- `ProtectionFeature`, `LevelBasedProtectionStrategy`, `EnchantmentProtectionCalculator`

### Platform Services
- `IPlatformServices` — cross-loader abstraction for entity/item/recipe/command registration, config, events, and networking
- Service locator pattern (`Services.java`) for clean loader-agnostic access

### Utilities
- Math, NBT, validation, and config bounds utilities in the Common module

---

## Who Uses It

```
HZLib  ←  LovelyLib  ←  Lovely Robot (Legacy, Tribute, Reboot)
HZLib  ←  Monsters & Girls
HZLib  ←  [future Heria Zone mods]
```

HZLib is the lowest layer. Mod-specific libraries like LovelyLib build on it. Content mods build on those — or directly on HZLib for mods that don't need a mid-layer library.

---

## Version Support

| Minecraft | Fabric | Forge | NeoForge |
|-----------|--------|-------|----------|
| 1.21.1    | ✅     | ✅    | ✅       |
| 1.20.1    | Planned | Planned | — |
| 1.19.4    | Planned | Planned | — |
| 1.19.2    | Planned | Planned | — |
| 1.18.2    | Planned | Planned | — |
| 1.17.1    | Planned | Planned | — |
| 1.16.5    | Planned | Planned | — |
| 1.12.2    | —      | Planned | — |
| 1.7.10    | —      | Planned | — |

Backport priority follows the dependent mods. 1.21.1 is the reference implementation. Backports down to 1.16.5 come first, then 1.12.2 and 1.7.10 as long-term targets.

---

## For Mod Developers

HZLib is not yet published as a standalone Maven artifact. The API is not frozen — do not build third-party mods against it until a stable release is announced.

Once stable, HZLib will be:
- Extracted to its own GitHub repository
- Published to a public Maven repository
- Documented with developer guides and API references

Follow the [Heria Zone Discord](https://discord.gg/KdZZMj89bU) or [Patreon](https://patreon.com/heriazone) for updates.

---

## Issues

Report bugs or issues via [GitHub Issues](https://github.com/heria-zone/reboot-lovely-robot/issues) (hosted in the reboot-lovely-robot repo until HZLib has its own).

---

## License

© Heria Zone. All Rights Reserved.

---

## Credits

Developed by **MSymbios / Heria Zone**.
