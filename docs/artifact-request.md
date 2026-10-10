# Runtime artifacts to add

Export the actual files listed below as sanitized **copies**. Keep originals privately. Do not send tokens, passwords, SSH private keys, WireGuard private/preshared keys, private database dumps, full credential-bearing backups or packet captures. Review copies locally before transfer. A blank environment template should list variable names only.

| Host | Actual file or narrow export needed | Repository directory / purpose |
| --- | --- | --- |
| VM2 | `/etc/loki/config.yml` | `configs/loki/`; schema, storage, retention, auth and listener |
| VM2 | `/etc/alloy/config.alloy` | `configs/alloy/`; four source paths, multiline parsing, labels/fields and Loki writes |
| VM2 | Relevant UDP-514 input and MikroTik routing snippets from `/etc/rsyslog.conf` and `/etc/rsyslog.d/` | `configs/rsyslog/`; actual snippet names are unknown; include file/directory permission summary and relevant rotation policy |
| VM2 | `/etc/suricata/suricata.yaml`, `/var/lib/suricata/rules/local.rules`, relevant rule include/update settings | `configs/suricata/`; confirm capture/logging and SID 1000002 without replacing the original rule |
| VM2 | `/usr/local/bin/tzsp-suricata.sh`; tzsp2pcap source/revision, build options and version | `scripts/`; confirm conversion pipeline and runtime dependency |
| VM2 | `/usr/local/bin/suricata-block.py` | `scripts/`; resolve EVE vs fast input, severity threshold, SSH command and trap thread |
| VM2 | `/usr/local/bin/correlation_alert.py` | `scripts/`; exact LogQL, IP aggregation, query type, cooldown and error handling; replace Telegram token/chat destination with environment variable names |
| VM2 | `/usr/local/bin/honeypot.py` | `scripts/`; listener scope, log format, source attribution and payload handling |
| VM2 | Resolved unit contents and drop-ins for `loki`, `alloy`, `correlation-alert`, `honeypot`, `suricata-block`, `tzsp-suricata`; relevant Grafana overrides | `configs/systemd/`; use `systemctl cat UNIT` locally then redact environment values; no secret environment files |
| VM1 + VM2 | Sanitized `/etc/wireguard/wg0.conf` plus private-key-free handshake/transfer summaries | `configs/wireguard/`; remove `PrivateKey` and `PresharedKey` values, keep public keys and private lab endpoints; withhold WAN endpoint addresses |
| MikroTik | Narrow `/ip firewall filter`, NAT, relevant address-list membership, `/system logging` and logging actions, `/tool sniffer` TZSP settings, relevant interfaces/addresses and SSH service/account restrictions | `configs/mikrotik/`; version-aware exports with sensitive fields hidden are only a starting point; also remove WAN addresses, serial/software IDs and unrelated personal data; retain generic lab identities; do not send full backups |
| VM2 | `/etc/nginx/sites-available/dvwa`, relevant Nginx module/includes and `/etc/nginx/modsec/main.conf`, CRS includes/overrides | Reviewed proxy/WAF subdirectories under `configs/` when added; original files exist by report, but are not included |
| Grafana | Security Overview dashboard JSON export and exact four source queries plus transformation settings | `dashboards/`; remove personal annotations and nonlocal datasource endpoints; retain generic titles, UIDs and localhost/private endpoints; keep logical mapping consistent |
| VM1 | Sanitized decoy file and minimal Apache/PHP/DVWA settings relevant to proxy/testing | Reviewed web/decoy documentation when added; use explicitly fictional credentials, never real DB passwords |
| Both VMs | OS/version summary, package/binary versions, service-user/permission summary, Python imports and dependency versions | `docs/deployment.md`; original dependency files if they actually exist |

## Evidence to capture next

- A small text sample from each actual producer: Nginx, complete ModSecurity multipart transaction with identifying headers/cookies/bodies removed, Suricata EVE alert, MikroTik firewall syslog and trap log. Include matching sanitized timestamps/IP aliases for a scenario, not a synthesized replacement. Store under `samples/sanitized-events/` only after checking.
- For correlation: two true same-IP query results, one-condition/different-IP/threshold negative cases, cooldown behavior, and a token/chat-ID-free delivered message record. Provide exact metric queries and evaluation timestamps.
- For external blocking: triggering alert with severity/policy, response journal, corresponding list entry, effective firewall rule/counters and a controlled reachability result.
- For quarantine: trap connection and journal, selective router membership, WAN failure plus LAN/admin success, and selective recovery. Remove private/public addresses and personal identifiers before sharing.
- ZAP before/after HTML/JSON reports from identical scope, target, session/security level and settings; remove cookies, authorization, form tokens and personal URLs. Current screenshots are not a controlled comparison.

Do not use `wg showconf`, `wg show all dump`, SSH key files, Telegram bot APIs or blanket dumps as evidence sources. Inspect and sanitize the narrow exports above locally before adding copies to the repository.

Use the [controlled-test runbook](evidence-runbook.md) and [run record template](templates/test-run.md) to collect the missing evidence. Keep simulated/replay/test-only results separate from original-policy live detections.
