<p align="center">
    <b>HZLib</b>
</p>

<p align="center">
    Shared multi-loader library for Heria Zone mods — Fabric, Forge, and NeoForge
</p>

<p align="center">
    <a href="https://www.curseforge.com/minecraft/mc-mods/hzlib">
        <img alt="CurseForge Downloads" src="https://img.shields.io/curseforge/dt/1586461?logo=CurseForge">
    </a>
    <a href="https://modrinth.com/mod/hzlib">
        <img alt="Modrinth Downloads" src="https://img.shields.io/modrinth/dt/KxsiDURd?logo=Modrinth">
    </a>
    <a href="https://discord.gg/ZmCPM22FCK">
        <img alt="Discord" src="https://img.shields.io/discord/1156134479149158402?logo=Discord">
    </a>
</p>

<p align="center">
    <a href="https://github.com/heria-zone/reboot-lovely-robot/issues">Issues</a> ·
    <a href="#what-it-provides">What It Provides</a> ·
    <a href="#dependency-map">Dependency Map</a> ·
    <a href="#version-support">Version Support</a> ·
    <a href="#for-mod-developers">For Mod Developers</a>
</p>

---

> **⚠️ In Development**
> HZLib is in active development. The API is not yet frozen — breaking changes may occur between versions. Not recommended for third-party mods until a stable API release is announced.
>
> The codebase currently lives inside the [reboot-lovely-robot](https://github.com/heria-zone/reboot-lovely-robot) monorepo under `sources/common/hzlib-1.21.1/`. It will be extracted to its own repository once stable.

---

## About

HZLib is the shared foundation that all Heria Zone mods are built on. It provides a loader-agnostic entity framework, variant system, animation profiles, NBT data pipeline, and platform abstractions — written once, working across Forge, NeoForge, and Fabric without duplication.

If you're playing a Heria Zone mod, this is the engine underneath it. It does nothing on its own.

---

## What It Provides

### Entity Framework
- `NativeEntity` — root entity base class
- `NativeEntityFamily<T>` — family descriptor with feature composition, stat configuration, and variant management
- `EntityFeature` — composable feature system via `withFeature(Class, Feature)`

### Variant & Appearance System
- `TextureVariantFeature`, `ModelVariantFeature`, `AnimatorVariantFeature` — data-driven variant registration
- `SizeVariantFeature` with `SizeConfig` — dynamic hitbox management, per-pose `EntityDimensions`, stat multipliers, O(1) lookup
- `ConditionalAppearanceFeature` — switches active appearance based on runtime conditions
- `CompositeAppearanceFeature` — composes multiple appearance layers into a single resolved appearance

### Animation Profile System
- `AnimationProfile` — named slots (idle, walk, rest, sit, ride, attack, hurt) with full builder API and null-safe fallback
- `IdleSlot` / `IdleCondition` — declarative idle state system; replaces tick-driven standby logic
- `AnimationPool`, `WeightedAnimation`, `SelectionStrategy` (RANDOM, WEIGHTED_RANDOM, SEQUENTIAL), `LoopBehavior`
- `BoneVisibilityFeature` — declarative per-bone show/hide rules evaluated each render frame
- Zero GeckoLib or Minecraft imports in core profile classes — pure Java

### NBT Data Pipeline
- `DataCompound` — version-agnostic NBT wrapper; zero MC imports in pipeline code
- `DataField<T>` — typed field handles; string key encapsulated, zero literals at call sites
- `EntityDataSchema` — ordered field registry; write/read via `DataCompound`
- `MigrationChain` / `MigrationStep` — sole migration authority; cross-field capable
- Version-safe UUID storage across all supported MC versions

### Progression and Combat
- `LevelFeature`, `CombatLevelFeature` — entity levelling with attribute scaling
- `LinearAttributeStrategy`, `ExponentialAttributeStrategy` — pluggable scaling curves
- `ProtectionFeature`, `LevelBasedProtectionStrategy`, `EnchantmentProtectionCalculator`

### Platform Services
- `IPlatformServices` — cross-loader abstraction for entity/item/recipe/command registration, config, events, and networking
- Service locator pattern (`Services.java`) for clean loader-agnostic access

---

## Dependency Map

```
HZLib (this library)
│
├── HZLib: Animate (optional — GeckoLib adapter, planned)
│   ├── LovelyLib
│   │   ├── Lovely Robot: Legacy
│   │   ├── Lovely Robot: Tribute
│   │   └── Lovely Robot: Reboot
│   └── Monsters & Girls
│
├── Cubelings           (vanilla renderer — no HZLib: Animate needed)
├── Reignited HUD       (UI only — no HZLib: Animate needed)
└── [future Heria Zone mods]
```

HZLib core has zero GeckoLib imports. Mods with Blockbench-animated entities will use the optional **HZLib: Animate** adapter layer (planned). Mods using vanilla rendering only depend on HZLib core.

---

## Version Support

| Minecraft | Fabric | Forge | NeoForge |
|-----------|--------|-------|----------|
| 1.21.1    | ✅ v1.0.0 | ✅ v1.0.0 | ✅ v1.0.0 |
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

HZLib is published on CurseForge and Modrinth but the API is not yet frozen. Third-party mods should wait for a stable API release before building against it.

Once the API is stable, HZLib will be:
- Extracted to its own GitHub repository
- Published to a public Maven repository
- Documented with developer guides and API references

Follow the [Heria Zone Discord](https://discord.gg/ZmCPM22FCK) or [Patreon](https://patreon.com/heriazone) for updates.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) and [CONTRIBUTORS.md](CONTRIBUTORS.md).

---

## Issues

Report bugs via [GitHub Issues](https://github.com/heria-zone/reboot-lovely-robot/issues) — hosted in the reboot-lovely-robot repo until HZLib has its own.

---

## License

Licensed under the **GNU Lesser General Public License v3.0 (LGPL v3)**.

You are free to use HZLib in your mod, modify it, and distribute it — as long as modifications to HZLib itself are shared under the same license and credit is given to the original authors.

See [LICENSE](LICENSE) for the full terms.

---

## Credits

Developed by **MSymbios / Heria Zone**.
