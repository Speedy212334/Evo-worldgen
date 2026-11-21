# EvolutionWorldGen

This is the canonical repository for EvolutionWorldGen development.

## One-time source import

The repository is being bootstrapped from the verified Minecraft 26.3 **Alpha4.2** source snapshot. Alpha4.2 includes the newly implemented compact natural Evolution Nexus spawn platform; the other 40 structure templates are unchanged.

1. Download the exact Alpha4.2 source ZIP provided in the conversation.
2. On GitHub, open **Add file → Upload files** in this repository.
3. Upload the ZIP at the repository root with this exact filename:
   `EvolutionWorldGen-26.3-Alpha4.2-Natural-Spawn-Platform-Source.zip`
4. Commit the upload to `main`.

The `.github/workflows/import-alpha41.yml` workflow verifies the archive SHA-256, safely extracts the project files, removes the uploaded ZIP from the working tree, and commits the complete source into the repository.

Expected SHA-256:

`3d7b6535d9454b2f14f934b9aa88cb8682a539582e856c1b555c5c4ae9fd22f3`

If the workflow cannot push because repository Actions permissions are read-only, open **Settings → Actions → General → Workflow permissions** and enable **Read and write permissions**, then rerun the workflow.

## Current validation status

Static NBT, template, worldgen-registry, content, tree-feature, spawn-bootstrap, and external-source audits passed in the preparation environment. This does **not** certify a Java 25 / Gradle 9.9.1 build, registry loading, or live Minecraft 26.3 world creation. Those remain required before deployment.
