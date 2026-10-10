# Sanitization and publication boundary

The source reports and 25 source JPEGs remain unchanged in the private `cybersecurity/` workspace. A private audit records their original checksums and the image review. They are not copied wholesale into this candidate.

Public documentation uses VM1/VM2/router roles, substituted underlay `192.0.2.0/24`, substituted WireGuard addresses `10.77.0.1/2`, and identifiers `LAB_ADMIN`, `ROUTER_AUTOMATION_USER`, `DECOY_USER`, `PUBLIC_ENDPOINT`, `EXTERNAL_SOURCE_IP`. These are documentation aliases, not real deployment settings. Source addressing and local account names are removed from the public Russian report; an actual available public source address is replaced by an explicit external-source placeholder. Generic product paths and nonidentifying ports/signature IDs remain.

Credentials shown in the decoy screenshot are still withheld even though the report calls them fictional. Peer public keys, account/host prompts, real public IPs, private topology addresses, dashboard URL/filter identifiers and incidental terminal/window content are reviewed. A hidden private-key marker is not a available private key. No actual Telegram token or real SSH/WireGuard private-key value was visibly found in the included material; this does not establish the safety of missing scripts/configs.

All 25 reviewed copy decisions are described in [screenshots](screenshots.md) and the [gallery](../assets/screenshots/README.md). Twenty-three PNG copies use opaque black rectangles; two JPEG copies have metadata removed only. Pixels outside the masks retain the original decoded values, and no original file was changed. All unmodified originals remain private. Text, images and metadata require scoped review before staging; `.gitignore` does not remove already tracked secrets. Image editing must preserve evidence, with no invented output or credential replacement represented as real output.

No license is added. Original reports, unmasked screenshots, private audit records and other workspace projects are excluded from this repository. Missing original sources must be reviewed and sanitized when added.
