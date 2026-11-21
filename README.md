# EvolutionWorldGen

This is the canonical repository for EvolutionWorldGen development.

## One-time source import

The repository is being bootstrapped from the verified Minecraft 26.3 Alpha4.1 source snapshot. To complete the import:

1. Download the exact Alpha4.1 source ZIP from the linked ChatGPT file.
2. On GitHub, open **Add file → Upload files** in this repository.
3. Upload the ZIP at the repository root with this exact filename:
   `EvolutionWorldGen-26.3-Alpha4.1-Tall-Tree-Registry-Fix-Source.zip`
4. Commit the upload to `main`.

The `.github/workflows/import-alpha41.yml` workflow checks the archive SHA-256, safely extracts the project files, removes the uploaded ZIP from the working tree, and commits the complete source into the repository.

Expected SHA-256:

`5099cb32f3a2b76f5a0ef574d5b5d9755f9dd6eab077caeccc2bd5c7f0a5cb93`

If the workflow cannot push because repository Actions permissions are read-only, open **Settings → Actions → General → Workflow permissions** and enable **Read and write permissions**, then rerun the workflow.

## Validation status

The Alpha4.1 snapshot passed its static JSON, structure-template, worldgen registry, tall-tree and spawn-bootstrap audits in the preparation environment. It has **not** yet passed a full Java 25 / Gradle 9.9.1 build or a live Minecraft 26.3 world-creation test. Those are the next validation gates.
