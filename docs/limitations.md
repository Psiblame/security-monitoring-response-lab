# Limitations

- This is a centralized Loki/Alloy/Grafana monitoring stack with custom correlation and response, not a demonstrated enterprise SIEM. No original configs, response code, dashboard JSON or raw events are available, so it cannot yet be reproduced.
- Screenshots establish individual observations. There is no independently verified end-to-end run, Telegram delivery, negative/cooldown test, quarantine reachability test or rollback record.
- April preliminary-stage images and June monitoring/response images may describe different snapshots. Exact operating-system, package versions, interfaces and deployment chronology are unknown.
- Suricata misses direct VM-to-VM traffic on the hypervisor switch in the described topology. The TCP trap observes one port only and does not implement SSH authentication.
- WAN quarantine preserves the LAN by design. Firewall rule order, FastTrack/established flows and source-IP policy are unverified. Address-list membership does not prove a drop.
- The TCP rule's `!51820` does not exclude UDP WireGuard; the original logic is documented without silently changing it. Its TCP matching scope can also include legitimate services.
- Shared source IPs may reflect NAT, proxies or unrelated users. A correlation hit or 4xx count does not by itself prove an attack; the later external-activity note has insufficient accompanying evidence.
- Earlier response reports refer to EVE priority 1; later journals identify `fast.log`. The actual filter/severity and deduplication policy need source review. Priority-3 example alerts do not settle that discrepancy.
- The ZAP images have different targets and totals; settings, authenticated scope, timing and exported findings are missing. WAF denials do not remove underlying DVWA vulnerabilities.
- Syslog UDP loss/spoof resistance, reliable multiline parsing, retention, IP-cardinality strategy, authentication, script privileges, restart behavior and alert failure handling are not established by the material.
- Versions 3.7.2 (Loki), 1.16.1 (Alloy) and PHP 8.3 are recorded in the setup notes, not verified binary facts. There is no comparative memory benchmark or verified Promtail migration record.
- Screenshots retain lab addresses, system account names and diagnostic fields. Password values and lab WAN endpoints are masked; private originals remain outside the repository.

See [testing](testing.md) for evidence status and [artifact request](artifact-request.md) for concrete work needed to close these gaps.
