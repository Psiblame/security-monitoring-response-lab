# Material inventory

Source material: four UTF-8 text reports and 25 JPEG screenshots. Runtime configuration files, Python programs, shell scripts, a RouterOS export, the Grafana dashboard JSON and raw events are not included yet.

| ID | Available text | Meaning |
| --- | --- | --- |
| R1 | `cybersecurity/dod.txt` | Task 3 implementation report: Loki/Alloy/Grafana, four logs, per-IP panels and correlated notification |
| R2 | `cybersecurity/dod2.txt` | Task 4 implementation report: WireGuard, decoy, trap, WAN quarantine and sensor blind spot |
| R3 | `cybersecurity/mini-lab/dod.txt` | Earlier tasks 1/2 implementation report: TZSP/Suricata/response and DVWA/proxy/WAF |
| R4 | `cybersecurity/mini-lab/requirements.txt` | Assignment brief in Russian; not a Python requirements file |

These are complementary numbered stages, not two versions of a task-3 DoD. Common VM roles, paths and network descriptions support documenting them as earlier/later stages of the lab. They do not prove identical deployed configurations or a common test run. R3 describes EVE/priority-1 response; R2 and June journals describe fast-log response. R4's requested extra links are not established by R2's implemented topology.

The root images show May/June service starts and June observations. Preliminary-folder images show April log entries and ZAP states. Dates are visible screenshot content, not verified host-time metadata. Actual deployment chronology is uncertain.

Every image is mapped in [screenshots](screenshots.md); source names, evidence scope, privacy findings and selection decisions are retained there. Source filenames were not changed. `pasted file.jpg` repeats the dashboard layout from `2.jpg` at a different visible scroll position; S07 overlaps the Loki/Alloy service evidence from S08/S09. They are not additional independent tests.

Missing artifacts are enumerated in [artifact request](artifact-request.md). Empty directories deliberately contain `.gitkeep`; screenshots are not treated as original configurations or scripts.
