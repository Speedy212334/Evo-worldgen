# EvolutionWorldGen engineering status — Alpha4.5

## Current source snapshot

- Version: `0.1.0-alpha.4.5`.
- Minecraft Java 26.3 / Fabric Loader 0.20.1 / Fabric API 0.166.2+26.3.
- Java 25 / Gradle wrapper 9.9.1 target.
- Archive SHA-256: `bff03ed453e9a91866dc1e1f939d148169a962f70796f491032dbe9f4f89ce1e`.
- Repository handoff workflow is ready; the full source enters `main` only after the exact ZIP is uploaded and the workflow completes.

## Vanilla `/locate` parity

Minecraft 26.3's `ChunkGenerator.findNearestMapStructure` dispatches nearest-structure searches only for `ConcentricRingsStructurePlacement` and `RandomSpreadStructurePlacement`. It asks each placement for potential candidates on a square-ring grid. For each candidate, `StructureCheck.checkStart` calls `applyAdditionalChunkRestrictions` before biome/start validation and before the locator loads a candidate chunk to `STRUCTURE_STARTS` if further confirmation is needed.

Alpha4.5 aligns custom restrictions with that flow:

- Fixed-origin placement remains a `RandomSpreadStructurePlacement` subclass. Its locator-grid cell maps to the exact configured fixed chunk; its new preflight accepts only that chunk and preserves the parent restriction. The generation-time `isPlacementChunk` check still enforces the same exact origin.
- Bounded Overworld placement remains a `RandomSpreadStructurePlacement` subclass. Its new preflight now checks the exact same full-footprint block-coordinate envelope as generation, using overflow-safe chunk-to-block conversion.
- Standard vanilla random-spread placements retain their vanilla seed/salt calculation and locator path.

Coverage: 24 vanilla random-spread + 15 bounded random-spread + 2 fixed-origin random-spread = 41 structures.

## Static checks passed

- 41 structure definitions, 41 pools and 41 structure sets match the catalogue.
- All 41 IDs are listed exactly once in `LOCATE-COMMANDS.txt`.
- All placement types are recognised by Minecraft 26.3's locator dispatch.
- Fixed-origin grid search is tested at positive and negative coordinates up to the normal 100-grid-sector search radius.
- Fixed-origin preflight is restricted to the exact origin chunk.
- All 15 bounded Overworld placements pass first/last in-bounds candidate checks and reject candidates immediately beyond all four bounds.
- 4,216 worldgen registry/locator-preflight assertions pass.
- All 41 structure NBT templates, content audit, tall-tree audit and 11 spawn-bootstrap assertions pass.
- The Alpha4.5 source archive passes ZIP integrity validation.

These are static/source-level checks only.

## Not yet verified

- No Java 25 / Gradle 9.9.1 build or Alpha4.5 JAR has been produced.
- No Minecraft 26.3 registry-load or disposable-world session has been completed for Alpha4.5.
- No live `/locate structure` tests have been completed with the Alpha4.5 JAR.
- Vanilla `/locate` still checks biome/start eligibility and may inspect candidate chunks to `STRUCTURE_STARTS`; players do not need to pre-explore destination chunks.
- Full terrain/footprint slope, burial, collision and fluid sampling remains unconnected to the live Fabric structure-start pipeline.

## Preserved requirements

- Evolution Nexus at Overworld `(0,0)` in the Plains biome family, with the approved 25×7×25 platform and clear 7×7 arrival centre.
- Dragon's Crown at End `(0,0)`, preserving the vanilla dragon fight, exit portal and gateways.
- Every Overworld structure fully inside inclusive X/Z bounds -10,000..+10,000, including its footprint and margins.
- Terrain-conditioned placement must not force structures into unsuitable biome, elevation, slope, fluid or footprint conditions.
- Structures must not overlap. Nether and End bounds remain separately configured.
- Vanilla `/locate structure evolutionworldgen:<id>` remains the intended lookup interface.