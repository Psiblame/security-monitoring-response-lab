# Preparation verification

Local review on 2026-10-10. These checks concern documentation and reviewed screenshot copies only; no VM, router, notification, attack, response or rollback was run.

- **Pass:** all 29 originals unchanged.
- **Pass:** required documents and empty runtime-artifact directories.
- **Pass:** standalone lab repository and no assigned license.
- **Pass:** relative links and Markdown fences.
- **Pass:** Mermaid nodes and edges checked as text; no rendering claim.
- **Pass:** scoped heuristic secret and original-identity scans.
- **Pass:** two service JPEG copies have unchanged decoded pixels and reviewed OCR.
- **Pass:** all 25 source images reviewed.
- **Pass:** all 23 masked PNG copies individually reviewed; OCR and secret checks passed.
- **Pass:** PNG metadata removed; masked pixels are opaque black, and every pixel outside the masks is identical to the original.

The [gallery](../assets/screenshots/README.md) includes all 25 reviewed copies. Keys, credential rows, identifying addresses/accounts and selected transaction identifiers are obscured with black rectangles. Unmodified originals and the detailed mask/checksum records remain private outside the repository.

Screenshots are historical observations from different stages. Masked addresses prevent independent source-IP equality checks. Original configurations, scripts, raw events and a dashboard export are still missing; deployed behavior and reproducibility remain unverified.

After adding future artifacts, repeat source integrity, links, scoped privacy/secret scanning and image review before staging.
