# EvolutionWorldGen engineering status

Updated: 2026-11-21

## Current working snapshot

- Target: Minecraft Java 26.3, Fabric Loader 0.20.1, Fabric API 0.166.2+26.3.
- Build toolchain: Java 25 and Gradle 9.9.1.
- Prepared source snapshot: **Alpha4.2 — Natural Spawn Platform**.
- Archive SHA-256: `3d7b6535d9454b2f14f934b9aa88cb8682a539582e856c1b555c5c4ae9fd22f3`.
- The GitHub repository has the import workflow and handoff documentation, but the full source is not in `main` until the exact Alpha4.2 ZIP is uploaded to the repository root and the workflow completes.

## Alpha4.2: Evolution Nexus spawn platform

The previous 220×110×220 monumental sanctuary has been replaced by a compact, natural **25×7×25** platform, centred at the exact Overworld origin. Its design includes:

- An irregular clipped-corner stone foundation and a 17×17 upper deck.
- An unobstructed 7×7 central arrival area.
- Four short stone lantern posts.
- Flush warm-light inlays, small perimeter moss/grass patches, and a three-block-wide approach path.
- No building, roof, tall pillars, loot chests, or interior spaces.

The Nexus remains restricted to the Plains biome family at exactly X/Z (0,0), with its existing fixed-origin structure placement. Its vanilla locate identity remains `/locate structure evolutionworldgen:evolution_nexus`.

Only the Nexus template and its supporting catalogue/design/audit/docs entries were changed. The other 40 structure templates remain unchanged.

## Static verification completed

- 41 compressed Minecraft structure templates passed the NBT/template audit.
- The Nexus is 25×7×25, contains 656 block placements, has a centred root anchor at local [12,1,12], and has zero loot chests.
- The other 40 templates retain their three loot chests each.
- 1,032 world-generation registry assertions passed.
- Content/architecture audit passed.
- Tall-tree feature audit passed.
- Spawn bootstrap audit passed (11 checks).
- External-source provenance audit passed: 40 external CC BY 4.0 source mappings plus one separately recorded original, user-approved Nexus design.
- ZIP integrity check passed.

These are static checks only. They do not certify a Gradle build, registry load, world creation, or live structure placement.

## Validation still required

1. Import the exact Alpha4.2 source ZIP into `Speedy212334/Evo-worldgen` using the repository handoff workflow.
2. Build on the user's Windows environment with Java 25 and Gradle 9.9.1.
3. Install the resulting JAR with the exact Minecraft 26.3/Fabric and terrain-mod versions listed in the compatibility documentation.
4. Create a disposable new world and confirm registry loading completes.
5. Confirm the Nexus generates at X/Z (0,0), the origin biome passes the Plains-family requirement, and the saved player spawn lands safely on the clear central pad.
6. Check the platform's visible geometry and height in-game, including the approach path and lantern placement.
7. Verify the `/locate` catalogue in a live world; do not treat static registration assertions as proof of runtime locate behavior.

## Known engineering gap

The source contains a seeded terrain/footprint placement planner, but the Alpha4 implementation report says its full terrain sampler is not yet connected to the live Fabric structure-placement pipeline. Existing placement alignment alone does not guarantee full-footprint slope suitability, no burial, or collision avoidance. This remains an overall worldgen engineering priority after baseline registry/world-creation validation.

## Product requirements to preserve

- Evolution Nexus at the exact world origin (0,0); the spawn area must be in a Plains-family biome.
- Every Overworld structure and the Nexus must remain fully inside X/Z -10,000 through +10,000, including the full footprint and margins.
- Placement must be conditioned on biome, terrain class, elevation, slope, surface shape, footprint clearance and dimension. Rarity applies only to suitable sites; never force an unsuitable placement to hit a target count.
- Structures must not overlap. Nether and End placement bounds are handled separately.
- The End redesign must preserve the central dragon fight, exit portal and outer gateways unless separately approved.
- The previous Abfielder Spawn Build is no longer the selected Nexus design. The original approved natural spawn-platform design is the current choice.
