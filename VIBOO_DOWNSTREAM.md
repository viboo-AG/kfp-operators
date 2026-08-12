# Viboo downstream release

This branch contains Viboo-specific changes on top of Canonical KFP Operators.

The changes are maintained internally and have not been submitted to the upstream repository.

## Base

- Upstream repository: `canonical/kfp-operators`
- Upstream commit: `bbc97a3475fcd1295c59d1fd9b88567956e96492`
- KFP API tag: `kfp-api/rev2861`
- KFP profile controller tag: `kfp-profile-controller/rev2837`
- KFP UI tag: `kfp-ui/rev2872`

## Downstream concerns

- `fix(kfp-api): accept bucket from S3 provider`
- `fix(kfp-profile-controller): enable TLS for artifact proxy`
- `fix(kfp-ui): use archive bucket from storage provider`
- `fix(kfp-ui): make archive key format configurable`

Each concern is a separate commit so it can be retained, changed, or removed independently during an upgrade.

## Verification

Pushes to `release/**` run `.github/workflows/viboo-downstream-ci.yaml`.

The workflow lints, tests, and packs `kfp-api`, `kfp-profile-controller`, and `kfp-ui`.

The packed `.charm` files are stored as GitHub Actions artifacts.

## Upgrade procedure

1. Create a new release branch from the exact new upstream tag or commit.
2. Evaluate each downstream concern against the new upstream source.
3. Omit a concern if the new upstream source already provides equivalent behavior.
4. Cherry-pick each remaining concern separately and resolve any semantic changes.
5. Run the downstream CI workflow.
6. Deploy the packed charms to DEV with the existing `juju refresh --path` process.
7. Promote the same source commits to PROD only after DEV verification.
