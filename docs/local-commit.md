# Working with this repository

Clone the standalone laboratory repository:

```sh
git clone https://github.com/Psiblame/security-monitoring-response-lab.git
cd security-monitoring-response-lab
git status --short
```

Review [verification](verification.md), [sanitization](sanitization.md) and the relevant evidence before adding files. Keep original reports, unmasked screenshots, raw exports and private audit records outside this repository.

When adding reviewed artifacts, stage only the intended paths, then inspect the changes:

```sh
git diff --cached --stat
git diff --cached --check
git status --short
```

Cloning this documentation does not deploy the laboratory. The original runtime configurations and programs listed in [artifact request](artifact-request.md) are still needed.
