# EvolutionWorldGen

This is the canonical repository for EvolutionWorldGen development.

## Current source handoff: Alpha4.5 — Vanilla Locate Preflight

The current package is **EvolutionWorldGen 26.3 Alpha4.5 — Vanilla Locate Preflight**. It retains all 41 original block-by-block structure NBT builds and the approved natural Evolution Nexus, and aligns the custom structure-placement preflight with Minecraft 26.3's native `/locate structure` search.

1. Download the exact Alpha4.5 source ZIP provided in the conversation.
2. On GitHub, open **Add file → Upload files** in this repository.
3. Upload the ZIP at the repository root with this exact filename:
   `EvolutionWorldGen-26.3-Alpha4.5-Vanilla-Locate-Preflight-Source.zip`
4. Commit the upload to `main`.

The `.github/workflows/import-alpha45.yml` workflow verifies the archive SHA-256, replaces the prior project tree, safely extracts the project files, removes the uploaded ZIP from the working tree, and commits the complete source into the repository.

Expected SHA-256:

`bff03ed453e9a91866dc1e1f939d148169a962f70796f491032dbe9f4f89ce1e`

If the workflow cannot push because repository Actions permissions are read-only, open **Settings → Actions → General → Workflow permissions** and enable **Read and write permissions**, then rerun the Alpha4.5 import workflow from the **Actions** tab.

## What Alpha4.5 fixes

- Minecraft 26.3's native nearest-structure search scans concentric-ring and random-spread placement classes. All 41 EvolutionWorldGen IDs now use one of those locator-compatible classes.
- The fixed-origin Nexus and Dragon's Crown still generate only at their exact `(0,0)` chunk. Their additional-chunk-restriction preflight now rejects every off-origin candidate before `/locate` needs to inspect or load it.
- The 15 bounded Overworld random-spread structures now apply their full-footprint `-10,000..+10,000` envelope during locator preflight as well as actual generation. Candidate chunks outside the allowed envelope are rejected before chunk inspection.
- The 24 vanilla random-spread structures keep vanilla seed/salt candidate calculation and behaviour.
- All 41 command IDs appear exactly once in `LOCATE-COMMANDS.txt`.

## Validation status

Static structure-template, content, registry, tree-feature, spawn-bootstrap, and 4,216 locator-preflight regression assertions pass in the preparation environment. This does **not** certify a Java 25 / Gradle 9.9.1 build, registry loading, or live Minecraft 26.3 `/locate` results. Runtime testing is still required before production use.