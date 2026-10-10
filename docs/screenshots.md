# Screenshot evidence index

The index covers 25 screenshots from the lab's monitoring, response and preliminary WAF/IDS stages. IDs S02-S17 follow the numbered captures; S18 is the alternate dashboard view and S19-S26 are preliminary-stage images. There is no S01.

All images have public copies. Nineteen retain their decoded pixels unchanged. Six have small opaque masks only over password values or the lab WAN endpoints. Private IPs, generic users/hostnames, ports, paths, public WireGuard keys, source addresses and event IDs remain readable. Original captures stay private.

| ID | Private source name | Stage | Visible evidence / limit | Privacy / selection |
| --- | --- | --- | --- | --- |
| S02 | `2.jpg` | R1 | Four source panels and merged per-IP table visible. No query/export or delivery result. | [public copy](../assets/screenshots/s02-grafana-source-panels.png); reviewed |
| S03 | `3.jpg` | R1 | Top dashboard view: event counter 2668 and source panels. Counter is a snapshot. | [public copy](../assets/screenshots/s03-grafana-overview.png); reviewed |
| S04 | `4.jpg` | R1 | correlation-alert active/enabled; Python invocation visible. No delivered message. | [public copy](../assets/screenshots/s04-correlation-service.png); reviewed |
| S05 | `5.jpg` | R1 | Router firewall topic routed to remotesyslog. Does not show receiver delivery. | [public copy](../assets/screenshots/s05-router-syslog.png); reviewed |
| S06 | `6.jpg` | R1 | grafana-server active/enabled. No ingestion/delivery result. | [public copy](../assets/screenshots/grafana-service-status.jpg); reviewed |
| S07 | `7.jpg` | R1 | Alloy and Loki active/enabled, two unit outputs; overlaps S08/S09. | [public copy](../assets/screenshots/s07-alloy-loki-services.png); overlapping/duplicate evidence |
| S08 | `8.jpg` | R1 | Alloy active/enabled, config invocation and historical memory output. | [public copy](../assets/screenshots/s08-alloy-service.png); reviewed |
| S09 | `9.jpg` | R1 | Loki active/enabled and config argument. Memory value is historical. | [public copy](../assets/screenshots/loki-service-status.jpg); reviewed |
| S10 | `10.jpg` | R2 | Journal identifies fast.log and trap monitor; quarantine and external list-add messages. | [public copy](../assets/screenshots/s10-response-journal.png); reviewed |
| S11 | `11.jpg` | R2 | Trap listener restarts and connection lines; no complete SSH exchange. | [public copy](../assets/screenshots/s11-trap-connections.png); reviewed |
| S12 | `12.jpg` | R2 | Decoy file with client/SSH sections; username differs from report wording. | [public copy](../assets/screenshots/s12-decoy-config.png); reviewed |
| S13 | `13.jpg` | R2 | WireGuard latest handshake and received/sent bytes; private key displayed as hidden. | [public copy](../assets/screenshots/s13-wireguard-status.png); reviewed |
| S14 | `14.jpg` | R2 | Suricata journal: two rule files, 49310 rules loaded, zero failed; no SID hit. | [public copy](../assets/screenshots/s14-suricata-rule-load.png); reviewed |
| S15 | `15.jpg` | R2 | Historical TCP rule with !51820 and SID 1000002 visible. | [public copy](../assets/screenshots/s15-historical-suricata-rule.png); reviewed |
| S16 | `16.jpg` | R2 | Same reaction sequence as S10; command shown; not independent evidence. | [public copy](../assets/screenshots/s16-response-journal-alternate.png); overlapping/duplicate evidence |
| S17 | `17.jpg` | R2 | Router quarantine list includes a VM address and honeypot-trap comment. | [public copy](../assets/screenshots/s17-router-quarantine.png); reviewed |
| S18 | `pasted file.jpg` | R1 | Dashboard like S02 at a different scroll position. Separate rows, same layout. | [public copy](../assets/screenshots/s18-grafana-table-alternate.png); overlapping/duplicate evidence |
| S19 | `mini-lab/acess log nginx.jpg` | R3 | Nginx access-format output, HTTP methods/statuses and DVWA paths. | [public copy](../assets/screenshots/s19-nginx-access-events.png); reviewed |
| S20 | `mini-lab/eve json logs.jpg` | R3 | EVE JSON stats and invalid-timestamp alerts with severity 3. Not priority-1 response. | [public copy](../assets/screenshots/s20-suricata-eve-events.png); reviewed |
| S21 | `mini-lab/fast log suricata.jpg` | R3 | Repeated invalid-timestamp alerts, priority 3; does not prove blocking. | [public copy](../assets/screenshots/s21-suricata-fast-events.png); reviewed |
| S22 | `mini-lab/modsec log.jpg` | R3 | Multipart audit: numeric-Host warning, rule 920350, HTTP 200. Not a denial. | [public copy](../assets/screenshots/s22-modsecurity-warning.png); reviewed |
| S23 | `mini-lab/ngingx erROR .jpg` | R3 | ModSecurity access denied HTTP 403 and rule 949110; several request paths. | [public copy](../assets/screenshots/s23-modsecurity-denials.png); reviewed |
| S24 | `mini-lab/suricata block.jpg` | R3 | Router address list includes suricata-block entries, some with timeouts. | [public copy](../assets/screenshots/s24-router-blocklists.png); reviewed |
| S25 | `mini-lab/до modsec.jpg` | R3/R4 | ZAP UI before-labelled image: 33 alert tree entries. Target differs from S26. | [public copy](../assets/screenshots/s25-zap-before-labelled.png); reviewed |
| S26 | `mini-lab/после modsec.jpg` | R3/R4 | ZAP UI after-labelled image: 37 alert tree entries. No controlled baseline. | [public copy](../assets/screenshots/s26-zap-after-labelled.png); reviewed |

R1/R2/R3/R4 are mapped in [inventory](material-inventory.md). Repeated journals and dashboards are not independent tests. The earlier report claims 49314 rules, while S14 shows 49310; do not merge counts from different snapshots. The visible 33/37 ZAP totals are UI entries, not a validated reduction in vulnerabilities or a count of exploitation successes.

All copies and captions are in the [25-image gallery](../assets/screenshots/README.md). See the [test matrix](testing.md) for observations that still require raw events, original runtime artifacts or paired tests.
