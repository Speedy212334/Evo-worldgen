# EvolutionWorldGen engineering status — Alpha4.6

## Current prepared source

- Version: `0.1.0-alpha.4.6`.
- Minecraft Java 26.3 / Fabric Loader 0.20.1 / Fabric API 0.166.2+26.3.
- Java 25 / Gradle wrapper 9.9.1 target.
- Archive SHA-256: `4cae55ac668f2b32b2bbd9da850a492082ca57dd493099151344a95278d28f49`.
- The repository has the Alpha4.6 source-import workflow, but the complete project source enters `main` only after the exact archive is uploaded and the workflow completes.

## Vanilla locate coverage

- 24 structures use vanilla `minecraft:random_spread`.
- 15 Overworld structures use `BoundedRandomSpreadStructurePlacement`, a `RandomSpreadStructurePlacement` subclass with identical full-footprint bounds in `StructureCheck` preflight and generation.
- 2 fixed structures use `FixedOriginStructurePlacement`, also a `RandomSpreadStructurePlacement` subclass. Only the grid cell containing the exact configured origin resolves to the fixed chunk; every other candidate is rejected during both preflight and generation.
- Both custom codecs inherit Minecraft common placement fields, including `locate_offset`, frequency reduction, frequency and exclusion zones.
- All 41 command IDs are in `LOCATE-COMMANDS.txt`.

These checks establish source-level compatibility with Minecraft 26.3's native nearest-structure dispatcher. Runtime registry loading and `/locate` still require a real Java 25 Fabric server test. Vanilla may inspect candidate chunks to `STRUCTURE_STARTS`; prior player exploration is not required.

## Alpha4.6 structure improvements

- All 41 structure NBTs are newly generated and pass structural integrity checks.
- Nexus remains 25×7×25 with a clear 7×7 arrival centre and has extra natural approach/edge detail.
- 16 families receive stronger vertical architecture; a new audit checks their actual NBT palette markers and minimum vertical massing.
- The shared generic floating-island base has been removed from End structure generation. Each End structure now owns its own island, bridge, arena, district or ruin-cluster geometry.
- All 120 family loot chests have solid support and clear headroom.

## Static verification passed

- 3,119 world-generation/locator-preflight assertions across 41 structures.
- 41/41 NBT structure templates; anchors, 26.3 state palette schema, dimensions, bounds and loot bindings valid.
- 120/120 loot chest support/headroom checks.
- 41 unique architecture styles, silhouettes and procedural recipes.
- 16 NBT architecture-quality profiles pass family-specific block-count and vertical-massing checks.
- End-specific geometry audit confirms no universal generic shell is stamped under all End families.
- Tall-tree feature audit and 11 spawn-bootstrap assertions.
- Python source scripts compile.

## Not yet verified

- No Java 25 / Gradle 9.9.1 build or Alpha4.6 JAR has been produced.
- No live Minecraft 26.3 registry-load or `/locate` session has been completed for Alpha4.6.
- The full terrain/footprint slope, burial, collision and fluid sampler remains unconnected to the live Fabric structure-start pipeline. Large-structure terrain fit is not yet fully guaranteed.
- Interior navigation, loot access and Dragon's Crown gameplay still need in-game inspection.

## Preserved requirements

- Evolution Nexus at Overworld `(0,0)` in the Plains biome family.
- Dragon's Crown at End `(0,0)` while preserving the vanilla dragon fight, exit portal and outer gateways.
- All Overworld structure footprints and margins inside inclusive X/Z bounds -10,000..+10,000.
- No unsuitable-biome or unsuitable-terrain forced placements; no overlapping structures.
- Use vanilla `/locate structure evolutionworldgen:<id>` in the correct dimension.