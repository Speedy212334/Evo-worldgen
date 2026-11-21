# EvolutionWorldGen engineering status — Alpha4.4

## Current prepared source

- Target: Minecraft Java 26.3, Fabric Loader 0.20.1, Fabric API 0.166.2+26.3.
- Toolchain target: Java 25 and Gradle wrapper 9.9.1.
- Source package: **Alpha4.4 — Original Voxel Structures**.
- Archive SHA-256: a3c10935e4d3e48d32744e13ba67a1ad14621f0364e88e55a01efd84fa024536.
- Repository is prepared with an Alpha4.4 import workflow; the project source will only enter main after the exact archive is uploaded and that workflow completes.

## Implemented structure work

- All 41 structure-template NBT assets are original, block-by-block procedural layouts, each with a unique family recipe and distinct NBT hash.
- The 40 non-Nexus structure families have been rebuilt to interpret the approved Overworld, Nether and End visual concepts. No old external survival-base schematic candidate or downloader is used.
- The Evolution Nexus retains the approved compact 25×7×25 spawn platform and unobstructed 7×7 centre, with additional stone/moss/lantern detailing.
- Dragon's Crown receives outer broken-arch and underside fragments while retaining the ten vanilla crystal/tower positions and central dragon-fight area.
- Geometry refinements remove the flat-pad appearance from the Lost Underground City, Cliffside Outposts, Ruined Settlements, Forest Waystations, Ashen Capital and Ruined Nether Cities.
- End structures and buildings are aligned to their actual floating-island/deck levels.
- All 120 loot chests are placed on solid support blocks with two clear blocks above.

## Placement and locate contract

- The Alpha4.3 fixed-origin placement adapter remains in place. It makes the Evolution Nexus and Dragon's Crown discoverable to vanilla's nearest-structure placement search without allowing generation away from their exact (0,0) origin chunks.
- The other 39 naturally distributed structure families retain their existing seed-and-salt random-spread placement settings.
- Expected vanilla commands:
  - /locate structure evolutionworldgen:evolution_nexus
  - /locate structure evolutionworldgen:dragons_crown
  - /locate structure evolutionworldgen:grand_bridges

## Static verification completed

- 41/41 NBT templates validate: dimensions, bounds, DataVersion 5023 palette schema, palette references, anchor metadata, loot-table binding and unique hashes.
- 40 structures have three distinct family-bound loot chests; the Nexus has none.
- All 120 loot chests pass the solid-support and headroom audit.
- 41 unique architecture/silhouette records and 41 distinct procedural recipes pass the content audit.
- 2,068 world-generation registry assertions pass across 41 structures, pools, sets, biome tags, salts and Overworld footprint bounds.
- Tall-tree feature audit passes.
- Spawn bootstrap audit passes (11 assertions).
- Python source scripts pass syntax compilation.
- The final source ZIP passes its archive integrity test.
- All 41 structure NBT assets differ from the Alpha4.3 baseline.

These are static/source-level checks only.

## Not yet verified

- No Java 25 / Gradle 9.9.1 build or Alpha4.4 JAR has been produced.
- No Minecraft 26.3 registry-load or disposable-world generation session has been completed for Alpha4.4.
- No live vanilla /locate structure tests have been completed with the Alpha4.4 JAR.
- The full terrain/footprint sampler remains unconnected to the live Fabric structure-start pipeline; full-footprint slope, burial, collision and fluid eligibility therefore still need implementation and runtime validation.
- Loot accessibility, interior pathing, large-structure terrain fit and Dragon's Crown gameplay interactions require in-game review.

## Preserved requirements

- Evolution Nexus at Overworld (0,0) in the Plains biome family, clear safe player-arrival area.
- All Overworld structures fully within inclusive X/Z bounds -10,000..+10,000, including footprint and margins.
- Terrain-conditioned placement must not force structures into unsuitable biomes, elevation, slopes, fluids or footprints.
- Structures must not overlap. Nether and End bounds are handled separately.
- Preserve the central End dragon fight, exit portal and outer gateways.
- All future structure redesigns should use distinct original voxel compositions, not reused generic schematics.