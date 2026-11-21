# EvolutionWorldGen engineering status

Updated: 2026-11-21

## Current baseline

- Intended baseline: Minecraft Java 26.3, Fabric Loader 0.20.1, Fabric API 0.166.2+26.3.
- Build toolchain: Java 25 and Gradle 9.9.1.
- Candidate source snapshot: Alpha4.1, SHA-256 `5099cb32f3a2b76f5a0ef574d5b5d9755f9dd6eab077caeccc2bd5c7f0a5cb93`.
- The repository is being bootstrapped from that snapshot; the import workflow is in `.github/workflows/import-alpha41.yml`.

## Verified in preparation environment

The following static checks passed against the Alpha4.1 archive:

- Tall oak and spruce feature schema audit.
- JSON/resource parse audit (234 JSON files).
- 41 compressed Minecraft structure templates.
- 1,032 world-generation registry assertions.
- 11 spawn-bootstrap assertions.
- External build-source mapping audit: 41 families mapped to 21 CC BY 4.0 source candidates.

These are static checks only. They do not certify a Gradle build, registry load, world creation, or live placement.

## Validation still required

1. Build on the user's Windows environment with Java 25 and Gradle 9.9.1.
2. Install the resulting Alpha4.1 JAR with the exact Minecraft 26.3/Fabric and terrain-mod versions listed in the compatibility documentation.
3. Create a disposable new world and confirm registry loading completes.
4. Confirm the Nexus is generated at X/Z (0,0), the origin biome passes the Plains-family requirement, and player spawn is placed correctly.
5. Test the tall-tree features and representative Overworld, Nether, and End structures.
6. Verify the `/locate` catalogue in a live world; do not treat static registration assertions as proof of working locate commands.

## Known engineering gap

The source contains a seeded terrain/footprint placement planner, but the Alpha4 implementation report says its full terrain sampler is not yet connected to the live Fabric structure-placement pipeline. Existing placement alignment alone does not guarantee full-footprint slope suitability, no burial, or collision avoidance. This integration is a priority after baseline registry/world-creation validation.

## Product requirements to preserve

- Evolution Nexus at the exact world origin (0,0); the spawn area must be in a Plains-family biome.
- Every Overworld structure and the Nexus must remain fully inside X/Z -10,000 through +10,000, including the full footprint and margins.
- Placement must be conditioned on biome, terrain class, elevation, slope, surface shape, footprint clearance and dimension. Rarity must apply only to suitable sites. Never force an unsuitable placement to hit a target count.
- Structures must not overlap. Nether and End placement bounds are handled separately.
- The End redesign must preserve the central dragon fight, exit portal and outer gateways unless separately approved.
- The currently selected Spawn Build schematic is a separate dependency; do not replace it with a different design. Import it only after the user supplies the actual licensed schematic file and its permitted-use terms are checked.
