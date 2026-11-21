# EvolutionWorldGen

This is the canonical repository for EvolutionWorldGen development.

## Current source handoff: Alpha4.4 — Original Voxel Structures

The current package is **EvolutionWorldGen 26.3 Alpha4.4 — Original Voxel Structures**. It includes 41 original, family-specific block-by-block NBT builds based on the approved visual concepts, the detailed natural Evolution Nexus platform, the Alpha4.3 vanilla `/locate` compatibility change, corrected End-island elevations, and the loot chest support/headroom audit.

1. Download the exact Alpha4.4 source ZIP provided in the conversation.
2. On GitHub, open **Add file → Upload files** in this repository.
3. Upload the ZIP at the repository root with this exact filename:
   `EvolutionWorldGen-26.3-Alpha4.4-Original-Voxel-Structures-Source.zip`
4. Commit the upload to `main`.

The `.github/workflows/import-alpha44.yml` workflow verifies the archive SHA-256, replaces the previous project tree, safely extracts the project files, removes the uploaded ZIP from the working tree, and commits the complete source into the repository.

Expected SHA-256:

`a3c10935e4d3e48d32744e13ba67a1ad14621f0364e88e55a01efd84fa024536`

If the workflow cannot push because repository Actions permissions are read-only, open **Settings → Actions → General → Workflow permissions** and enable **Read and write permissions**, then rerun the Alpha4.4 import workflow from the **Actions** tab.

## What Alpha4.4 changes

- Original family-specific procedural voxel builds for all 41 registered structure templates; no prior external survival-base schematics are used.
- Refined Lost Underground City, Cliffside Outposts, Ruined Settlements, Forest Waystations, Ashen Capital and Ruined Nether Cities so they do not read as single flat base pads.
- End floating structures and city buildings are aligned to their actual island/deck elevations.
- All 120 loot chests have a support block beneath and clear headroom above.
- The Evolution Nexus keeps its approved 25×7×25 footprint and 7×7 clear arrival centre.

Alpha4.3's fixed-origin placement adapter remains: the Nexus and Dragon's Crown use vanilla-locatable placement types while generation remains fixed at X/Z `(0,0)`.

## Validation status

Static structure-template, chest support/headroom, content, worldgen registry, tree-feature and spawn-bootstrap audits passed in the preparation environment. This does **not** certify a Java 25 / Gradle 9.9.1 build, registry loading, live Minecraft 26.3 world generation or runtime `/locate` results. Those remain required before deployment.
