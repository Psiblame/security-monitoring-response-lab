# Selected portfolio evidence

Seven screenshots provide a short first review of the lab's monitoring, WAF, IDS, response outputs and network administration. The full gallery preserves supporting material and historical context.

These images come from different test stages. They support the visible observations below; they do not establish one synchronized end-to-end response test. Source addresses remain visible, making matching rows and entries readable. The screenshots still do not establish one synchronized test window.

## Start with these seven images

| Order | Evidence | Skill demonstrated | What the image supports |
| --- | --- | --- | --- |
| 1 | [S03 — Grafana overview](../assets/screenshots/s03-grafana-overview.png) | Centralized security monitoring | Four source panels and a historical event counter; collection completeness is not established |
| 2 | [S23 — ModSecurity denials](../assets/screenshots/s23-modsecurity-denials.png) | WAF log analysis | HTTP 403 denial entries, CRS rule 949110 and request paths |
| 3 | [S21 — Suricata fast.log](../assets/screenshots/s21-suricata-fast-events.png) | IDS event analysis | Signature, classification and priority 3 output; these entries do not prove automated blocking |
| 4 | [S10 — Response journal](../assets/screenshots/s10-response-journal.png) | Python service operation and journal analysis | Trap-monitor activity and list-addition messages; firewall enforcement is not shown |
| 5 | [S17 — MikroTik quarantine](../assets/screenshots/s17-router-quarantine.png) | Router address-list administration | Quarantine membership; WAN loss, retained administration and recovery are not shown |
| 6 | [S24 — MikroTik blocklists](../assets/screenshots/s24-router-blocklists.png) | External-source response configuration | suricata-block entries and selected timeouts; effective traffic drops are not shown |
| 7 | [S13 — WireGuard status](../assets/screenshots/s13-wireguard-status.png) | Linux network administration | Recent handshake and received/sent counters; an administrative SSH session is not shown |

For a SOC / Blue Team review, begin with the dashboard, WAF and IDS records, then inspect the response outputs and their limits. For a Linux administration review, begin with WireGuard and the service-status images listed below.

## Supporting images

These ten images add detail for a technical discussion. They are optional for the first pass.

| Evidence | Use |
| --- | --- |
| [S02 — Grafana source panels](../assets/screenshots/s02-grafana-source-panels.png) | Additional dashboard and merged-table view |
| [S04 — Correlation service](../assets/screenshots/s04-correlation-service.png) | Active/enabled service and Python invocation; message delivery is not shown |
| [S05 — Router syslog](../assets/screenshots/s05-router-syslog.png) | Router logging route; receiver delivery is not shown |
| [S06 — Grafana service](../assets/screenshots/grafana-service-status.jpg) | Active/enabled systemd state |
| [S08 — Alloy service](../assets/screenshots/s08-alloy-service.png) | Active/enabled state and configuration invocation |
| [S09 — Loki service](../assets/screenshots/loki-service-status.jpg) | Active/enabled state and configuration argument |
| [S11 — Trap connections](../assets/screenshots/s11-trap-connections.png) | Listener and connection records; no complete SSH exchange |
| [S14 — Suricata rule loading](../assets/screenshots/s14-suricata-rule-load.png) | Loaded rules and zero failed rules; no custom-rule hit |
| [S19 — Nginx access log](../assets/screenshots/s19-nginx-access-events.png) | HTTP methods, status codes and paths |
| [S20 — Suricata EVE JSON](../assets/screenshots/s20-suricata-eve-events.png) | Structured events and severity 3 records |

## Historical context and overlapping views

| Evidence | Reason to retain it outside the first review |
| --- | --- |
| [S12 — Decoy configuration](../assets/screenshots/s12-decoy-config.png) | Only password values are masked; host, account, port and path fields remain visible |
| [S15 — Historical Suricata rule](../assets/screenshots/s15-historical-suricata-rule.png) | Shows the original TCP rule; see the [protocol limitation](detection-and-response.md) |
| [S22 — ModSecurity warning](../assets/screenshots/s22-modsecurity-warning.png) | HTTP 200 warning; it is not a WAF denial |
| [S07 — Combined Alloy/Loki status](../assets/screenshots/s07-alloy-loki-services.png) | Overlaps S08/S09 |
| [S16 — Alternate response journal](../assets/screenshots/s16-response-journal-alternate.png) | Repeats the S10 reaction sequence |
| [S18 — Alternate Grafana table](../assets/screenshots/s18-grafana-table-alternate.png) | Overlaps the dashboard views |
| [S25 — ZAP before-labelled view](../assets/screenshots/s25-zap-before-labelled.png) | Different target and no controlled baseline |
| [S26 — ZAP after-labelled view](../assets/screenshots/s26-zap-after-labelled.png) | Cannot demonstrate a reduction in vulnerabilities when compared with S25 |

The selection covers all 25 images: seven for the first review, ten for supporting detail and eight for historical context or overlapping views. The [complete gallery](../assets/screenshots/README.md), [evidence index](screenshots.md) and [test matrix](testing.md) retain the detailed captions and gaps.

## Linking the project from a CV

Use a link to this repository or this page as the project evidence. Keep the screenshots in the repository so the CV can stay compact and searchable.

Original scripts, configurations, raw events and the dashboard export are still missing. The [repository status](repository-status.md) records these gaps; screenshots alone do not make the deployment reproducible.
