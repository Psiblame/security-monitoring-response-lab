# Deployment record

These setup notes list the lab services, paths and installation sequence. Original configurations, binary checksums and a complete OS/package inventory are not included yet; the notes are not a complete deployment script.

## Documented services and files

| Component | Documented installation / configuration | Evidence |
| --- | --- | --- |
| Loki | `/usr/local/bin/loki`, `/etc/loki/config.yml`, `/var/lib/loki`, TCP 3100; `loki.service` | S07/S09 show active service and config argument; version 3.7.2 is recorded in the setup notes; not checked against the binaries |
| Alloy | `/usr/local/bin/alloy`, `/etc/alloy/config.alloy`; `alloy.service` | S07/S08 show active service and invocation; version 1.16.1 is recorded in the setup notes; not checked against the binaries |
| Grafana OSS | APT repository, TCP 3000; `grafana-server.service` | S06 shows service active; S02/S03/S18 show UI |
| rsyslog | UDP 514 input, firewall-message filtering and `/var/log/mikrotik/firewall.log` | Report plus S05 logging topic; daemon config/receipt evidence absent |
| Suricata / tzsp2pcap | `/usr/local/bin/tzsp2pcap`, wrapper `/usr/local/bin/tzsp-suricata.sh`, `tzsp-suricata.service` | S14 shows two rule files and zero failed rules; binary/config absent |
| Custom rule | `/var/lib/suricata/rules/local.rules`, included from `/etc/suricata/suricata.yaml` | S15 rule text; S14 loader summary |
| Nginx / ModSecurity | Site `/etc/nginx/sites-available/dvwa`; `/etc/nginx/modsec/main.conf`, CRS includes | S19 access output, S22 audit output, S23 denial output |
| VM1 web stack | Apache2, PHP 8.3 (documented), MariaDB; `/var/www/html/DVWA` | Report; package/config exports absent |
| WireGuard | `/etc/wireguard/wg0.conf` on both VMs; `wg-quick@wg0` | S13 runtime output only |
| Correlation program | `/usr/local/bin/correlation_alert.py`, `correlation-alert.service` | S04 active service, no source |
| Trap / response | `/usr/local/bin/honeypot.py`, `/usr/local/bin/suricata-block.py`; `honeypot.service`, `suricata-block.service` | S10/S11/S16 journals; source and units absent |

## Known sequence

1. Install VM1's web stack and DVWA. The preliminary assignment requests direct testing followed by temporary closure of direct public ports; closure and TLS are not evidenced.
2. Configure VM2's proxy, ModSecurity and CRS; compare controlled requests with WAF disabled/enabled. S23 supports particular 403 denials, not removal of every DVWA vulnerability.
3. Configure router TZSP mirroring, the conversion wrapper, Suricata and its logs. Confirm listener location and host firewall: a RouterOS `input` rule handles traffic destined to the router, not automatically UDP reception on VM2. The preliminary report's wording must be reconciled with actual rules.
4. Configure response automation and router address lists, with a restricted SSH account. The reports name RSA key authentication; key material and exact privileges are not available.
5. Install Loki/Alloy/Grafana, configure rsyslog and the four ingestion paths, then export the dashboard. Parser expressions, service users, retention and authentication are unknown.
6. Add correlation, WireGuard and the TCP decoy; validate reachability and negative response cases. Do not deploy the broad TCP rule before reviewing its scope and sensor visibility.

## Dependencies still to record

Record OS/release, installed package versions, Suricata build information, tzsp2pcap source/revision and build options, Python interpreter and imports/locked dependencies, ModSecurity connector, CRS version, Loki storage schema/retention and all unit permissions. The available `mini-lab/requirements.txt` is a Russian task brief, **not** a Python dependency list. No install command uses it.

Use the [artifact request](artifact-request.md) to fill the missing directories. Safe examples can then be derived from actual exports; they are intentionally absent now. Historical service screenshots do not verify any current upstream version or compatibility.
