# EvolutionWorldGen engineering status

Updated: 2026-11-21

## Current working snapshot

- Target: Minecraft Java 26.3, Fabric Loader 0.20.1, Fabric API 0.166.2+26.3.
- Build toolchain: Java 25 and Gradle 9.9.1.
- Prepared source snapshot: **Alpha4.3 — Vanilla Locate Compatibility**.
- Archive SHA-256: `a4c6511f2317337d16c0bb1497e49fa3e1143ed5c1b6f23728930f0685b13392`.
- The GitHub repository has the Alpha4.3 import workflow and handoff documentation, but the full source is not in `main` until the exact Alpha4.3 ZIP is uploaded to the repository root and the workflow completes.

## Alpha4.2: Evolution Nexus spawn platform

The previous 220×110×220 monumental sanctuary was replaced by a compact, natural **25×7×25** platform, centred at the exact Overworld origin. Its design includes an irregular clipped-corner stone foundation, a 17×17 upper deck, an unobstructed 7×7 central arrival area, four short lantern posts, moss/grass patches and a narrow approach path. It has no building, roof, tall pillars, loot chests or interior spaces.

The Nexus remains restricted to the Plains biome family at exactly X/Z (0,0), with its fixed-origin placement. Its vanilla locate identity remains `/locate structure evolutionworldgen:evolution_nexus`.

## Alpha4.3: vanilla /locate compatibility

Minecraft 26.3's `ChunkGenerator.findNearestMapStructure` dispatches placement searches for `ConcentricRingsStructurePlacement` and `RandomSpreadStructurePlacement`. The original custom fixed-origin placement only implemented `StructurePlacement`, so vanilla's locator did not inspect the Nexus or Dragon's Crown placement.

Alpha4.3 makes `FixedOriginStructurePlacement` extend `RandomSpreadStructurePlacement`:

- `getPotentialStructureChunk` maps the one random-spread search-grid cell containing the configured fixed chunk to the exact fixed chunk.
- Every other search-grid cell delegates to vanilla random spread.
- `isPlacementChunk` still accepts only the exact configured chunk, so generation does not spread or create extra origins.
- The locator grid uses spacing 32, separation 31, linear spread and the original per-structure salt.

This applies to:
- Evolution Nexus: Overworld X/Z (0,0).
- Dragon's Crown: End X/Z (0,0).

The other 39 structure families already use `BoundedRandomSpreadStructurePlacement` or vanilla `minecraft:random_spread`, so their placement class is compatible with the native locator scan. The vanilla command IDs are unchanged.

## Static verification completed

- 41 compressed Minecraft 26.3 structure templates passed the NBT/template audit.
- 2,068 world-generation registry assertions passed across 41 structure definitions, 41 pools, 41 sets, biome tags, salts, footprint bounds and the locator-grid regression simulation.
- The locator-grid regression mirrors Minecraft 26.3's square-ring scan from positive and negative player chunk coordinates and verifies that the fixed-origin grid cell resolves to (0,0).
- Content/architecture audit passed.
- Tall-tree feature audit passed.
- Spawn bootstrap audit passed (11 checks).
- External-source provenance audit passed: 40 external CC BY 4.0 source mappings plus one separately recorded original, user-approved Nexus design.
- ZIP integrity check passed for the Alpha4.3 source archive.

These are static/source-level checks only. They do not certify a Gradle build, registry load, world creation or live locate behavior.

## Validation still required

1. Import the exact Alpha4.3 source ZIP into `Speedy212334/Evo-worldgen` using the repository handoff workflow.
2. Build on the user's Windows environment with Java 25 and Gradle 9.9.1.
3. Install the resulting JAR with the exact Minecraft 26.3/Fabric and terrain-mod versions listed in the compatibility documentation.
4. Create a disposable new world and confirm registry loading completes.
5. Test vanilla commands in the matching dimensions:
   - `/locate structure evolutionworldgen:evolution_nexus`
   - `/locate structure evolutionworldgen:dragons_crown`
   - `/locate structure evolutionworldgen:grand_bridges`
6. Confirm the first two return X/Z (0,0), that the Nexus origin biome passes the Plains-family requirement, and that the third returns its seed-and-salt random-spread position.
7. Verify that the locate search can find the structures from unexplored chunks. Vanilla may synchronously load candidate chunks to `ChunkStatus.STRUCTURE_STARTS); this does not mean the destination chunk must have been pre-explored.
8. Inspect actual generated structure starts and worldgen in a disposable new world.

## Known engineering gap

The source contains a seeded terrain/footprint placement planner, but the Alpha4 implementation report says its full terrain sampler is not yet connected to the live Fabric structure-placement pipeline. Existing placement alignment alone does not guarantee full-footprint slope suitability, no burial, or collision avoidance. This remains an overall worldgen engineering priority after baseline registry/world-creation validation.

## Product requirements to preserve

- Evolution Nexus at the exact world origin (0,0); the spawn area must be in a Plains-family biome.
- Every Overworld structure and the Nexus must remain fully inside X/Z -10,000 through +10,000, including the full footprint and margins.
- Placement must be conditioned on biome, terrain class, elevation, slope, surface shape, footprint clearance and dimension. Rarity applies only to suitable sites; never force an unsuitable placement to hit a target count.
- Structures must not overlap. Nether and End placement bounds are handled separately.
- The End redesign must preserve the central dragon fight, exit portal and outer gateways unless separately approved.
- The compact natural spawn platform is the approved Evolution Nexus design; future detail work must preserve its scale and clear centre.
