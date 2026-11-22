# EvolutionWorldGen

This is the canonical repository for EvolutionWorldGen development.

## Current source handoff: Alpha4.6 — Locator and Structure Quality

The current package is **EvolutionWorldGen 26.3 Alpha4.6**. It retains all 41 original procedural Minecraft NBT builds, refines the Evolution Nexus, strengthens 16 weaker architectural silhouettes, removes the shared generic End island shell, and extends static tests for vanilla `/locate structure` compatibility.

1. Download the exact Alpha4.6 source ZIP provided in the conversation.
2. On GitHub, open **Add file → Upload files** in this repository.
3. Upload the ZIP at the repository root with this exact filename:
   `EvolutionWorldGen-26.3-Alpha4.6-Locator-and-Structure-Quality-Source.zip`
4. Commit the upload to `main`.

The `.github/workflows/import-alpha46.yml` workflow verifies the archive SHA-256, replaces the previous project tree, safely extracts the full source, removes the uploaded ZIP from the working tree, and commits the project files.

Expected SHA-256:

`4cae55ac668f2b32b2bbd9da850a492082ca57dd493099151344a95278d28f49`

If the workflow cannot push because repository Actions permissions are read-only, open **Settings → Actions → General → Workflow permissions** and enable **Read and write permissions**, then rerun the Alpha4.6 import workflow from the **Actions** tab.

## Locator implementation

All 41 structures use placement classes recognised by Minecraft 26.3's nearest-structure search: 24 vanilla random-spread, 15 bounded random-spread subclasses and 2 fixed-origin random-spread subclasses. The fixed Nexus and Dragon's Crown remain at `(0,0)` in their respective dimensions. Both custom placements apply the same preflight restrictions as generation; both codecs inherit vanilla common placement fields including locate offsets.

## Structure quality

Alpha4.6 adds family-specific vertical architecture to 16 weak/flat silhouettes and removes the universal generic floating-island shell under all End structures. Each End family now has its own island, bridge, ruin-cluster or district footprint. The Nexus keeps the 25×7×25 platform and unobstructed 7×7 arrival centre, with additional weathered details and approach markers.

## Static validation status

Static audits pass: 3,119 locator/worldgen assertions; 41/41 structure NBT templates; 120/120 loot chest support/headroom checks; 41 unique architecture profiles/recipes; 16 family-specific NBT massing profiles; tree features; and 11 spawn-bootstrap assertions.

This does **not** certify a Java 25 / Gradle 9.9.1 build, registry loading or live Minecraft 26.3 `/locate` behaviour. Those remain required before production deployment.