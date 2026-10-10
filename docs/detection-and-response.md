# Detection and response

The sections below describe detection rules, response outputs and outstanding validation work. Missing source code prevents confirmation of parser behavior, response thresholds, error handling and notification semantics.

## 1. Correlated Telegram notification

The report describes two Loki metric queries every 60 seconds: IPs with **more than five** ModSecurity blocks in a one-minute window, and IPs with Suricata scan signatures matching `ET SCAN.*` in that window. Python takes `set(A) & set(B)`. A ten-minute cooldown applies per source IP. A three-minute experiment is mentioned; the documented final window is one minute.

The only query fragments available are `count_over_time(...[1m]) > 5`, `| json` and `alert_signature=~"ET SCAN.*"`. They are not complete executable LogQL queries. Stream selectors, aggregation by IP, mapping of EVE `alert.signature` to `alert_signature`, and what qualifies as a ModSecurity **block** are unavailable. Counting all audit messages would not implement the described policy.

[LogQL comparisons](https://grafana.com/docs/loki/latest/query/query_reference/) normally filter false vector elements unless `bool` is requested. The [Loki instant query endpoint](https://grafana.com/docs/loki/latest/reference/loki-http-api/#query-logs-at-a-single-point-in-time) accepts metric queries, not raw log queries. Review the real programs for either pitfall before claiming the two-query implementation works.

Expected cases: ModSecurity alone -> no notification; Suricata alone -> no notification; both with the same IP and matching window -> eligible notification; different IPs -> no notification; repeat within cooldown -> suppressed. These negative cases and a delivered message are not available. S04 confirms a running service, not delivery or cooldown. The later external-activity note has no accompanying record that establishes attribution.

Dashboard panels join four sources on `src_ip` (Merge transformation documented). S02/S03/S18 show tables, counts and a combined view; JSON/query exports are absent. Shared IP activity and Nginx 4xx volume are investigation leads, not proof of a multi-vector attack. A single screenshot counter is not a throughput measurement.

## 2. External source blocking

The preliminary stage describes reading EVE JSON and responding only to priority/severity 1 alerts. The later report describes preserving an existing `fast.log` monitor and adding a second trap-log thread. S10/S16 explicitly show `/var/log/suricata/fast.log` and a successful-add message for `suricata-block`; S24 shows address-list entries. The priority-3 stream alerts in S20/S21 do **not** demonstrate the documented priority-1 trigger.

The assumed response is SSH from VM2 to a restricted router account followed by an address-list update, then a firewall drop rule. Neither the exact matching policy nor firewall counters are present. List membership and a script's success message do not alone establish packet loss, duration or rollback behavior. The runtime source is needed to resolve the EVE/fast.log difference.

## 3. Decoy-triggered WAN quarantine

VM1 has a decoy file `/var/www/html/DVWA/db_backup.sql.config` with fabricated credentials pointing to VM2 TCP 2222. S12 shows the file; only the two password values are masked; host and account fields remain visible. The text and screenshot use different decoy-account names; this is not evidence of an exact shared configuration.

The trap program documentedly sends `SSH-2.0-OpenSSH_8.9p1` and logs connections. This is a TCP listener with an SSH banner, not an SSH protocol implementation. A connection can be a test or unexpected contact; it does not by itself prove compromise or that the decoy file was read.

A second response thread watches `/var/log/honeypot.log` for `[ALERT]` connection messages and adds VM1 to router `quarantine`. The documented duplicate guard is `/tmp/vm1-quarantined.flag`, and `tail -n 0` processes only newly appended lines. S11 shows connections; S10/S16 show reaction messages; S17 shows list membership. The script's source-IP verification, SSH exit handling and log-rotation behavior remain unknown.

The documented firewall rule matches `src-address-list=quarantine` and `out-interface=ether1` in `forward`. Its intended result is loss of **outgoing WAN** access while VM2 and administration remain reachable. No ping outputs, live SSH session or firewall counters are available. Do not label it full isolation.

## Custom TCP rule and its limitation

S15 displays the rule below. The protocol, negated port and options are reproduced from the historical rule. This is a documented historical excerpt, not a deployable configuration file:

```text
alert tcp 192.0.2.10 any -> 192.0.2.20 !51820 (msg:"lateral movement vm1->vm2 isolate"; flow:to_server; sid:1000002; rev:1;)
```

`tcp` limits it to TCP, and `!51820` excludes **TCP destination port 51820**; it does not express an exception for UDP WireGuard. It is also broad: it does not distinguish every legitimate TCP service from lateral movement. `flow:to_server` describes flow direction, not proof of malicious initiation. These meanings follow [Suricata rule format](https://docs.suricata.io/en/suricata-7.0.12/rules/intro.html); the installed version is not established.

S14 shows zero failed rules, not an SID 1000002 detection. The setup notes record no direct VM1-to-VM2 traffic in EVE because the router mirror misses the hypervisor-switch path. Proposed VLAN/routed separation or hypervisor mirroring would require topology changes and fresh testing. The deployed fallback described here is the trap log, with visibility limited to its listening port.

## Recovery and operational gaps

Recovery requires removing the quarantine address-list entry and deleting the flag. Before any real recovery, reconcile the target VM entry and local flag, use a selective router operation, and validate WAN, proxy and admin behavior. A broad removal of all list members is not an appropriate verified runbook. No rollback operation was executed here. Flag loss on reboot, concurrent threads, cooldown persistence, allowlisting, SSH failures and established/FastTrack traffic need source review and controlled tests.
