# Cadenzai downstream

This branch is a temporary, openly disclosed downstream of Immich. It exists
to preserve manual metadata edits when an XMP sidecar cannot be written, most
notably for read-only external libraries.

## Invariants

1. A successful sidecar write unlocks the edited database properties and lets
   metadata extraction reconcile them from the persisted XMP file.
2. A failed sidecar write fails the job, retains the edited database values,
   and leaves those properties locked against metadata extraction.
3. The original media library remains read-only. This patch never redirects,
   modifies, deletes, or copies an original asset.
4. Production consumes images by immutable digest. A failed update, test, or
   image build cannot move the production pin.

`DOWNSTREAM_BASE` records the exact upstream release merged into this branch.
The downstream update workflow merges a newer stable upstream tag into a pull
request. Merge conflicts or failed tests stop the update without publishing a
new production image.

Images built from the default `downstream` branch are published as
`ghcr.io/cadenzai/immich-server`. They identify this fork, its source commit,
and the GitHub Actions build in both OCI labels and Immich's build metadata.

This code is AI-assisted and is not presented to upstream as human-generated.
Do not open an upstream pull request without first obtaining explicit approval
under Immich's contribution policy. Remove the downstream patch and return to
the official image when upstream provides equivalent behavior.
