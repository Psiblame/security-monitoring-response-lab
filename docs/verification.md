# Preparation verification

Local review on 2026-10-10. These checks concern documentation and selected screenshot copies only; no VM, router, notification, attack, response or rollback was run.

- **Pass:** originals unchanged.
- **Pass:** required documents.
- **Pass:** empty original artifact directories.
- **Pass:** scoped lab repository and no license.
- **Pass:** relative links.
- **Pass:** markdown fences.
- **Pass:** mermaid text edges and nodes.
- **Pass:** heuristic secret scan.
- **Pass:** source address identity privacy.
- **Pass:** selected images pixel integrity and ocr.
- **Pass:** all 25 source images reviewed.

All 29 source files retain the recorded SHA-256 values. Relative links and Markdown fences were checked. Mermaid nodes/edges were checked as text; no Mermaid renderer was used. Scoped heuristic/privacy scanning reviewed all candidate files; substituted WireGuard IPs are intentional placeholders. Two selected image copies retain exactly the same decoded pixels as their originals and have no identity/address/token candidates in the OCR check; visual review remains necessary.

All 25 original images were individually viewed. Twenty-three remain private because identifying details have not been masked. Pixel redaction of these images has not been performed. No original configurations, scripts, raw events or dashboard export have been available, so deployed behavior and reproducibility remain unverified.

Detailed private reports and checksums remain outside the candidate. After any future config/script/image addition, repeat source integrity, links and scoped privacy/secret review before staging.
