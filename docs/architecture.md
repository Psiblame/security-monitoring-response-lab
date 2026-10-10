# Architecture

The lab uses two VMs on one hypervisor switch connected to MikroTik `ether3`. A preliminary exercise asks for two links per VM and another network between them, but the implementation report describes one shared subnet. The actual interface layout and NAT mappings require a RouterOS export; the requested topology must not be presented as the observed topology.

All addresses below are documentation aliases, not deployment instructions. The underlay uses documentation range `192.0.2.0/24`; the overlay uses a substituted private subnet. Images hide addresses rather than replace their pixels with fictional values.

| Role | Public documentation alias | Documented role / ports |
| --- | --- | --- |
| Router LAN | `192.0.2.1` | Syslog sender and SSH automation target |
| VM1 | `192.0.2.10` | Apache/DVWA; administrative SSH TCP 2222 |
| VM2 | `192.0.2.20` | Proxy, IDS, log stack and response; SSH tunnel target documented on TCP 2223 |
| VM1 WireGuard | `10.77.0.1/24` | SSH destination over the overlay |
| VM2 WireGuard | `10.77.0.2/24` | Listener UDP 51820; VM1 initiates to VM2 underlay |
| Public ingress / test sources | `PUBLIC_ENDPOINT`, `EXTERNAL_SOURCE_IP` | Original public addresses removed; NAT endpoints not verified |
| Identities | `LAB_ADMIN`, `ROUTER_AUTOMATION_USER`, `DECOY_USER` | Substituted accounts; no real credentials included |

## Traffic flows

External web requests reach VM2's Nginx reverse proxy and ModSecurity before being forwarded directly to VM1's Apache/DVWA. The preliminary exercise describes ports 80/443, but the actual NAT and TLS configuration is absent. The before/after ZAP screenshots show different target addresses; they cannot establish identical test conditions.

MikroTik mirrors observed `ether3` traffic through TZSP to VM2 on UDP 37008. The documented wrapper runs `tzsp2pcap -f | suricata -r /dev/stdin`; source, build flags and full invocation are missing. The mirror does not include VM1-to-VM2 traffic switched inside the hypervisor. The traceroute and neighbor-table diagnosis in the setup notes is not accompanied by command-output screenshots.

WireGuard encrypts the administration path between VMs. VM1 initiates to VM2 at the substituted underlay endpoint `192.0.2.20:51820`, with keepalive 25 documented. VM2 has no configured endpoint in the report. Screenshot S13 shows a recent handshake and transfers, not an SSH session or a quarantine test.

## Log and response flows

| Producer | File / transport documented | Consumer |
| --- | --- | --- |
| Nginx | `/var/log/nginx/access.log` | Alloy -> Loki |
| ModSecurity | Multipart `/var/log/modsec_audit.log` | Alloy -> Loki |
| Suricata | `/var/log/suricata/eve.json` | Alloy -> Loki; initial response described here |
| Suricata | `/var/log/suricata/fast.log` | Later response journal identifies this input |
| MikroTik | UDP 514 -> rsyslog -> `/var/log/mikrotik/firewall.log` | Alloy -> Loki |
| Trap | `/var/log/honeypot.log` | Second response-service thread -> router `quarantine` |
| Loki | `/loki/api/v1/query`, local port 3100 | Correlation program -> Telegram |

Grafana uses Loki at `http://localhost:3100`; port 3000 is accessed through an SSH local forward according to the report. Binding addresses and authentication are unverified. Source-IP extraction differs by source; the label/field mapping, proxy trust and original-IP preservation require real configurations.

The WAN rule is described as `chain=forward action=drop src-address-list=quarantine out-interface=ether1 log=yes log-prefix="QUARANTINE:"`. It targets VM1's outgoing WAN path only. It does not isolate VM1 from VM2 or shut down the proxy. Rule order, FastTrack and established-flow effects have not been verified.

The report's phrase about placing a filter rule "above DSTNAT" is ambiguous: dst-nat and forward filtering are separate processing stages. [RouterOS packet flow](https://help.mikrotik.com/docs/spaces/ROS/pages/328227/Packet%2BFlow%2Bin%2BRouterOS) places dst-nat in prerouting before forward filtering; an actual export is needed to assess this deployment.
