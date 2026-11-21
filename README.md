# EvolutionWorldGen

This is the canonical repository for EvolutionWorldGen development.

## One-time source import: Alpha4.3

The current source package is **EvolutionWorldGen 26.3 Alpha4.3 — Locate Compatibility**. It includes the previously approved compact natural Evolution Nexus spawn platform and the vanilla /locate compatibility fix for both fixed-origin structures.

1. Download the exact Alpha4.3 source ZIP provided in the conversation.
2. On GitHub, open **Add file → Upload files** in this repository.
3. Upload the ZIP at the repository root with this exact filename:
   `EvolutionWorldGen-26.3-Alpha4.3-Locate-Compatibility-Source.zip`
4. Commit the upload to `main`.

The `.github/workflows/import-alpha43.yml` workflow verifies the archive SHA-256, safely extracts the project files, removes the uploaded ZIP from the working tree, and commits the complete source into the repository.

Expected SHA-256:

`a4c6511f2317337d16c0bb1497e49fa3e1143ed5c1b6f23728930f0685b13392`

If the workflow cannot push because repository Actions permissions are read-only, open **Settings → Actions → General → Workflow permissions** and enable **Read and write permissions**, then rerun the Alpha4.3 import workflow from the **Actions** tab.

## What Alpha4.3 changes

Minecraft 26.3's vanilla nearest-structure search scans concentric-ring and random-spread placement classes. Alpha4.3 makes the custom fixed-origin placement extend the random-spread class so the Evolution Nexus and Dragon's Crown participate in vanilla `/locate structure` searching, while actual generation remains fixed at X/Z `(0,0)`. The other 39 structures retain their existing random-spread placements.

## Validation status

Static worldgen, template, content, tree-feature, spawn-bootstrap, external-source and locator-grid regression audits passed in the preparation environment. This does **not** certify a Java 25 / Gradle 9.9.1 build, registry loading, or live Minecraft 26.3 locate behavior. Those remain required before deployment.
