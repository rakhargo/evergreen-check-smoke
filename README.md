# evergreen-check external smoke

This small repository exercises [Evergreen's read-only GitHub Action](https://github.com/Fatihmaull/evergreen/blob/main/action.yml) outside the Evergreen monorepo for task `W4-D25-02`. It has no workspace packages, build artifacts, account key or deployment secret.

The manually dispatched workflow scans guinea-pig A on Stellar Testnet twice using the same declared storage keys. The green job uses the default 17,280-ledger threshold and must exit 0. The red job raises the threshold to 2,000,000 ledgers and must exit **1** for a real low-TTL verdict; that job and the overall workflow are expected to be red. An install/setup error or exit 2/3 would not satisfy the test.

The first run pinned the Evergreen Action to tested commit `2a4ab0a`. The workflow now exercises the public `Fatihmaull/evergreen@v1` tag, whose remote peeled commit was independently read back as that same SHA. The npm CLI stays pinned to `0.1.0`. The storage-key declaration in [`a-data-keys.json`](a-data-keys.json) is copied from [Evergreen's committed Testnet A scan evidence](https://github.com/Fatihmaull/evergreen/blob/main/docs/evidence/2026-09-08-scan-entry-types/data-keys.json); ledger keys are public inputs, not signing keys.

This fixture tests the external-consumer path. It does not claim an unrelated human performed the run.
