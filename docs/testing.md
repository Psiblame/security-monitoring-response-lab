# Test matrix and evidence strength

**Documented** means a result appears in a narrative. **Screenshot-supported** means the visible output supports a specific observation. **Not available** means the required artifact is absent. The table covers existing records; it is not a new end-to-end test run. Screenshot IDs refer to the complete [image index](screenshots.md).

| Action / scenario | Expected result | Available observation | Evidence / status |
| --- | --- | --- | --- |
| Start log stack | Services run and ingestion succeeds | Grafana, Loki and Alloy active/enabled | S06-S09; screenshot-supported service state, not ingestion completeness |
| Send router firewall syslog | rsyslog receives UDP 514 and Alloy forwards it | Router logging topic and Grafana MikroTik panel | S05, S02/S03/S18; receipt/config absent |
| Correlate four log sources | Per-IP table contains source counts | Four source panels and combined table visible | S02/S03/S18; transformation/query implementation not available |
| Generate >5 WAF blocks AND scan alert for same IP in one minute | One eligible Telegram notification | Curl + scan trial documented; service active | R1, S04; paired events/message absent |
| Supply only one condition, different IPs, or <=5 blocks | No correlated message | No negative-case record | Not available |
| Repeat eligible IP within ten minutes | Suppress repeat | Cooldown described | R1; implementation/result not available |
| Trigger external blocking | Relevant alert, list addition, effective drop | Response logs report addition; list entries visible | S10/S16/S24; exact alert policy/drop counters absent |
| Inspect preliminary IDS alerts | JSON and fast alerts agree | Invalid-timestamp alerts with severity/priority 3 | S20/S21; confirms alert output, not priority-1 automation |
| Run WAF-protected web requests | Matching attacks receive denial | ModSecurity access denied, HTTP 403; CRS anomaly scores visible | S23; screenshot-supported denial entries |
| Inspect multipart audit | Audit includes rule messages | Numeric Host warning with HTTP 200 visible | S22; a warning is not necessarily a block |
| Compare ZAP before/after | Same scope/settings, interpretable baseline | Titles/filenames label stages; visible totals 33 and 37, targets differ | S25/S26; comparison not controlled, no exported reports |
| Check WireGuard | Handshake and bidirectional bytes | Recent handshake and received/sent counters | S13; screenshot-supported runtime state |
| Read decoy, connect to trap | Trap records connection from VM1 | Decoy contents and trap connections visible | S12/S11; temporal reading-to-connection link unproven |
| Process trap log | VM1 added to quarantine | Journal reaction and router membership | S10/S16/S17; screenshot-supported outputs |
| Check WAN / LAN / admin during quarantine | Outgoing WAN unavailable; internal/admin retained | Only narrative reports WAN ping failure, LAN ping success and admin design | R2; ping/SSH/counter artifacts not available |
| Load local SID 1000002 | Rule loads, triggers only on visible matching TCP traffic | Rule text; two files, zero failed rules | S15/S14; loading supported, trigger explicitly absent in report |
| Remove quarantine selectively | WAN restored; flag and router state consistent | Recovery described only | R2; not executed or evidenced |

R1 = available task-3 report (`dod.txt`), R2 = task-4 report (`dod2.txt`), R3 = preliminary tasks-1/2 implementation report, R4 = preliminary assignment brief. Their relationship and chronology are discussed in [inventory](material-inventory.md). April and June screenshots must not be represented as one synchronized test run.

## Tests still needed on the lab

Capture same-window sanitized WAF/IDS raw events, the exact query result and a delivered notification; include negative and cooldown cases. Capture an external-response trigger with policy, selective list update, firewall counters and controlled reachability. Capture trap connection, response journal, list membership and WAN/LAN/admin checks with consistent timestamps, then selective recovery. Repeat the WAF comparison on the same permitted test target and settings and export ZAP reports. Demonstrate the known east-west blind spot before proposing a new sensor topology.

The [verification](verification.md) page records file and documentation checks; deployed test results belong in the test-run records.

## Planned evidence collection

The [controlled-test runbook](evidence-runbook.md) gives bounded lab scenarios, negative cases, recovery and measurement requirements. The [run template](templates/test-run.md) is blank and makes no success claim. Execution results for this plan are not recorded yet.
