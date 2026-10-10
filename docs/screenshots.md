# Screenshot evidence index

All 25 source images were individually viewed at original resolution. IDs S02-S17 follow the numbered source files; S18 is the pasted dashboard image and S19-S26 are preliminary-stage images. There is no S01. Source paths below identify private originals; they are deliberately not links to unreviewed originals.

Two images can be included without altering their pixels. JPEG capture metadata was removed, and decoded RGB bytes were verified equal to the originals. The other 23 originals remain private because their public copies would need irreversible pixel masks. No masked copies of these 23 images have been added. No regenerated output is used as evidence. The present gallery is incomplete.

| ID | Private source name | Stage | Visible evidence / limit | Privacy / selection |
| --- | --- | --- | --- | --- |
| S02 | `2.jpg` | R1 | Four source panels and merged per-IP table visible. No query/export or delivery result. | Public IPs, private IP, URL/filter identifier; browser chrome; **withheld; requires masks** |
| S03 | `3.jpg` | R1 | Top dashboard view: event counter 2668 and source panels. Counter is a snapshot. | Public IPs, private IP, URL/filter identifier; browser chrome; **withheld; requires masks** |
| S04 | `4.jpg` | R1 | correlation-alert active/enabled; Python invocation visible. No delivered message. | Account/host prompt and translucent background; **withheld; requires masks** |
| S05 | `5.jpg` | R1 | Router firewall topic routed to remotesyslog. Does not show receiver delivery. | Router account/hostname; **withheld; requires masks** |
| S06 | `6.jpg` | R1 | grafana-server active/enabled. No ingestion/delivery result. | No identifying pixel text found; screenshot-capture metadata removed; **selected metadata-clean copy** |
| S07 | `7.jpg` | R1 | Alloy and Loki active/enabled, two unit outputs; overlaps S08/S09. | Incidental translucent background/prompt edges; **withheld duplicate** |
| S08 | `8.jpg` | R1 | Alloy active/enabled, config invocation and historical memory output. | Incidental background account/prompt edge; **withheld; requires masks** |
| S09 | `9.jpg` | R1 | Loki active/enabled and config argument. Memory value is historical. | No identifying pixel text found; screenshot-capture metadata removed; **selected metadata-clean copy** |
| S10 | `10.jpg` | R2 | Journal identifies fast.log and trap monitor; quarantine and external list-add messages. | Hostname, VM address, real public source IP; translucent background; **withheld; requires masks** |
| S11 | `11.jpg` | R2 | Trap listener restarts and connection lines; no complete SSH exchange. | Account/hostname, source VM address; **withheld; requires masks** |
| S12 | `12.jpg` | R2 | Decoy file with client/SSH sections; username differs from report wording. | Account/hostname, private topology, decoy usernames and passwords; **withheld; whole credential lines must be masked** |
| S13 | `13.jpg` | R2 | WireGuard latest handshake and received/sent bytes; private key displayed as hidden. | Account/hostname, peer public keys, endpoint and overlay address; **withheld; requires masks** |
| S14 | `14.jpg` | R2 | Suricata journal: two rule files, 49310 rules loaded, zero failed; no SID hit. | Account/hostname in command, journal and prompt; **withheld; requires masks** |
| S15 | `15.jpg` | R2 | Historical TCP rule with !51820 and SID 1000002 visible. | Account/hostname and private source/destination addresses; **withheld; requires masks** |
| S16 | `16.jpg` | R2 | Same reaction sequence as S10; command shown; not independent evidence. | Account/hostname, VM address and real public source IP; **withheld duplicate** |
| S17 | `17.jpg` | R2 | Router quarantine list includes a VM address and honeypot-trap comment. | Router identity and VM address; **withheld; requires masks** |
| S18 | `pasted file.jpg` | R1 | Dashboard like S02 at a different scroll position. Separate rows, same layout. | Public/private IPs, URL/filter identifier; browser chrome; **withheld duplicate** |
| S19 | `mini-lab/acess log nginx.jpg` | R3 | Nginx access-format output, HTTP methods/statuses and DVWA paths. | Public client/target IPs in many wrapped lines; account/host prompt; **withheld; requires careful multiline masks** |
| S20 | `mini-lab/eve json logs.jpg` | R3 | EVE JSON stats and invalid-timestamp alerts with severity 3. Not priority-1 response. | Public source/private destination IPs and account/host prompt; **withheld; requires careful multiline masks** |
| S21 | `mini-lab/fast log suricata.jpg` | R3 | Repeated invalid-timestamp alerts, priority 3; does not prove blocking. | Public/private IPs wrapped over lines and account/host prompt; **withheld; requires careful multiline masks** |
| S22 | `mini-lab/modsec log.jpg` | R3 | Multipart audit: numeric-Host warning, rule 920350, HTTP 200. Not a denial. | Public/private host identifiers, transaction identifier and prompt; **withheld; requires careful multiline masks** |
| S23 | `mini-lab/ngingx erROR .jpg` | R3 | ModSecurity access denied HTTP 403 and rule 949110; several request paths. | Public/private IPs, request/transaction identifiers and prompt; **withheld; requires careful multiline masks** |
| S24 | `mini-lab/suricata block.jpg` | R3 | Router address list includes suricata-block entries, some with timeouts. | Router account/hostname and public source IPs; **withheld; requires masks** |
| S25 | `mini-lab/до modsec.jpg` | R3/R4 | ZAP UI before-labelled image: 33 alert tree entries. Target differs from S26. | Public target in tree/URL and incidental browsing domains; **withheld; requires masks** |
| S26 | `mini-lab/после modsec.jpg` | R3/R4 | ZAP UI after-labelled image: 37 alert tree entries. No controlled baseline. | Public target in tree/URL and incidental browsing domains; **withheld; requires masks** |

R1/R2/R3/R4 are mapped in [inventory](material-inventory.md). Repeated journals and dashboards are not independent tests. The earlier report claims 49314 rules, while S14 shows 49310; do not merge counts from different snapshots. The visible 33/37 ZAP totals are UI entries, not a validated reduction in vulnerabilities or a count of exploitation successes.

Selected copies: [S06 Grafana](../assets/screenshots/grafana-service-status.jpg) and [S09 Loki](../assets/screenshots/loki-service-status.jpg). See [test matrix](testing.md) for the observations that still require raw evidence.
