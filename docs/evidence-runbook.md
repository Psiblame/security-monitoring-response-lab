# Evidence collection and controlled test runbook

This is a plan for future lab tests. It has no recorded execution results. Obtain the [actual sources and sanitized exports](artifact-request.md) first: exact queries, response input/policy, units and runtime parameters cannot be reconstructed from screenshots.

## Evidence standard

For each run capture event -> producer log -> ingestion/detector -> decision -> action -> measured effect -> selective recovery. Assign a run ID, record UTC start/end, clock synchronization, topology, source roles and config/script hashes. Keep raw captures private outside the candidate. Publish only reviewed copies. A service state or address-list entry supports its own observation, not the complete chain.

| Test level | Input | Claim supported |
| --- | --- | --- |
| Unit / simulated | Fixtures, mock clock and Loki/SSH/notification dependencies | Logic/boundaries/error handling; no live detection or delivery |
| Replay | Recorded events/PCAP with separate parser/sensor outputs | Rule/parser behavior on those inputs; no current capture proof |
| Controlled live | Small real traffic series between owned lab endpoints | Behavior of the recorded deployment under stated conditions |

Keep fixture streams and replay outputs separate from production log inputs and response watchers. A temporary LAB TEST signature is a test-only configuration change. It does not verify the original ET SCAN policy and must never be renamed into an apparent ET alert to claim success.

## Preconditions

- Export actual Python programs, units, ingestion/query configs, rules and Grafana JSON. Resolve EVE vs fast.log and the true severity threshold.
- Record versions, dependencies, service users, restricted router privileges, host-key verification and secret handling.
- Use two controlled client sources for different-IP cases; confirm observed IPs after NAT/proxy normalization.
- External response traffic must traverse the router mirror. Direct VM-to-VM traffic uses the known unsensed path.
- Preserve a separate management path and designate an owned WAN TCP probe with a successful baseline and independent control client.
- Confirm exact firewall scope/order, existing connections and FastTrack. Record differences between any test profile and the original deployment.

Do not interpret an empty query, missing notification or unreachable target as a pass until the detector and baseline are known working.

## Run dossier

Use the [test-run template](templates/test-run.md). Each dossier needs commands/exit codes, before-state and counters, producer events, exact A/B queries and responses at a common evaluation time, decision journal, action result, after-state, recovery and a justified PASS/FAIL/INCONCLUSIVE verdict. Include actual timestamps, query response types, rule/SID/severity and observed source role.

Store raw exports under a private directory outside this candidate. Later place reviewed text copies under `samples/sanitized-events/RUN_ID/`. Mask passwords, tokens, private/preshared keys, session cookies/Authorization, personal chat identities and lab WAN endpoints. Keep private addresses, generic system accounts, public peer keys and event identifiers visible. Keep a private consistent alias mapping; retain event order and meaningful timestamps. Do not fill an unexecuted dossier with invented results.

## Four-source ingestion

Generate a normal Nginx request with a run marker, a confirmed ModSecurity denial, a sensor-visible IDS event, and an event logged by an actual router rule. For each show the matching local record, Loki raw result, normalized source IP and corresponding panel. For router logs include sender, rsyslog file receipt and Loki. A narrow temporary logging rule, if required, is a separately recorded change.

Check multipart WAF transaction handling: six denied HTTP transactions must not be inflated by counting their separate audit sections. Measure source-to-Loki delay. Keep the run ID in event content rather than adding uncontrolled indexed-label cardinality.

Use metric queries with `/loki/api/v1/query` and raw log queries with `/loki/api/v1/query_range`; save query time and parsing errors. [Loki API](https://grafana.com/docs/loki/latest/reference/loki-http-api/) defines these endpoint types. Missing/malformed source IP or parser errors are not valid negative-test zeros.

## WAF baseline and blocked request

Set `LAB_HOST`, `LAB_PROXY_IP` and all target variables to the actual lab endpoints. These examples assume an owned HTTP listener on port 80. For HTTPS use the proper hostname and trusted lab CA.

```bash
curl -sS --connect-timeout 3 --max-time 10 \
  --resolve "${LAB_HOST}:80:${LAB_PROXY_IP}" \
  -o /dev/null -w 'control status=%{http_code} time=%{time_total}\n' \
  "http://${LAB_HOST}/DVWA/?lab_run=${LAB_RUN_ID}"

curl -sS --connect-timeout 3 --max-time 10 --get \
  --resolve "${LAB_HOST}:80:${LAB_PROXY_IP}" \
  --data-urlencode "lab_run=${LAB_RUN_ID}" \
  --data-urlencode 'id=1 OR 1=1' \
  -o /dev/null -w 'probe status=%{http_code} time=%{time_total}\n' \
  "http://${LAB_HOST}/DVWA/"
```

The probe is a candidate, not a guaranteed CRS trigger. Identify actual rule IDs/anomaly score/disruptive action in the corresponding audit record. Distinguish application/Nginx 403 from a WAF block. Compare the same owned target, host, method/path/payload, app snapshot, session/security level and client settings with the recorded WAF modes; restore protection after the isolated comparison. Export same-scope ZAP reports if used. A WAF denial does not prove the underlying application vulnerability is removed.

## C: correlated notification

The documented policy is more than five WAF blocks and a matching ET SCAN alert from one source in a rolling one-minute window, evaluated every 60 seconds, with a 600-second per-IP cooldown. Verify the original code/queries rather than assuming this is deployed.

Once a request is confirmed blocked, run six bounded repeats from client A:

```bash
for LAB_CASE_N in 1 2 3 4 5 6; do
  curl -sS --connect-timeout 3 --max-time 10 --get \
    --resolve "${LAB_HOST}:80:${LAB_PROXY_IP}" \
    --data-urlencode "lab_run=${LAB_RUN_ID}" \
    --data-urlencode "case=${LAB_CASE_N}" \
    --data-urlencode 'id=1 OR 1=1' \
    -o /dev/null -w "case=${LAB_CASE_N} status=%{http_code}\n" \
    "http://${LAB_HOST}/DVWA/"
  sleep 1
done
```

Confirm six qualifying transactions in A, not just six client commands. [LogQL count_over_time](https://grafana.com/docs/loki/latest/query/metric_queries/) counts log entries; actual pipeline/query design must preserve the desired transaction unit.

A small starting scan from the same client towards one owned mirrored target:

```bash
nmap -sT -Pn -T3 --max-retries 1 --max-rate 10 \
  -p 22,80,443,2222,2223 "$LAB_SENSOR_VISIBLE_TARGET"
```

This does not guarantee ET SCAN detection. Read a truly enabled ET scan rule, its SID/threshold/protocol/ports, then use an appropriately bounded test and inspect EVE. [Nmap timing](https://nmap.org/book/man-performance.html) explains the rate controls. If no matching alert is observed, original-policy end-to-end validation is incomplete; isolated fixture/replay or a separately labeled test-only detector can test other parts.

Align observed poll time, ingestion delay and the rolling 60-second window. Save a common manual evaluation timestamp for A/B. A severity-1 auto-ban may interrupt this scenario before the six requests complete: record the interference and any separate profile/ordering used to isolate the mechanisms.

| Case | Input | Expected |
| --- | --- | --- |
| C01 | >5 WAF blocks only; B proven empty | No alert |
| C02 | B only; A proven below threshold | No alert |
| C03 | A and B from different observed IPs | No alert |
| C04 | Exactly five blocks plus scan | No alert |
| C05 | Six qualifying blocks plus scan, same IP/window | One eligible decision and one visibly delivered message |
| C06 | Fresh eligible input during cooldown | Suppressed repeat with recorded reason |
| C07 | Fresh eligible input after cooldown | New eligible delivery |
| C08 | One condition outside the window | No alert |
| C09 | Missing IP, Loki timeout/error or malformed input | Explicit error/skip; no arbitrary response |
| C10 | Sender failure | No false delivery claim; explicit retry policy |

Use mock clock/fixtures for exact thresholds and cooldown boundaries, plus controlled live positive/negative and cooldown runs. Observe at least two complete polls for a live negative case. Preserve the WAF transactions, EVE signature, both query results, intersection decision, sender result and visible sanitized message. API acceptance alone is not visible delivery.

## B: IDS-to-router blocking

Before: client A and independent B can reach a known TCP endpoint; A is absent from `suricata-block`; record actual rule/counters. Trigger the actual policy and preserve its source alert and severity.

If there is no suitable safe original trigger, this new illustrative smoke rule can test a separate temporary profile; it is not an original artifact:

```text
alert http any any -> any any (msg:"LAB TEST benign HTTP marker"; flow:established,to_server; http.uri; content:"/lab-ids-marker"; sid:1000999; rev:1; priority:1;)
```

Check SID uniqueness and installed syntax, restrict actual source/destination/port, validate, use only for the test, then remove it. The broad header is illustrative, not deployment-ready. URI matching needs sensor-visible plaintext HTTP or a decryption point; an encrypted HTTPS URI cannot be matched this way. See [Suricata HTTP keywords](https://docs.suricata.io/en/suricata-7.0.12/rules/http-keywords.html). An HTTP 404 can still carry the marker URI for IDS matching.

Preserve trigger -> parser/SSH result -> list member -> firewall counter change -> a new TCP attempt from A failing while B works -> selective recovery and restored access. Record repeated input and a below-threshold case. Membership alone is not packet-drop proof.

Read-only router observations:

```text
/ip firewall address-list print detail where list=suricata-block
/ip firewall filter print stats where src-address-list=suricata-block
```

Test a previously established TCP flow separately from a new flow. [RouterOS packet flow](https://help.mikrotik.com/docs/spaces/ROS/pages/328227/Packet%2BFlow%2Bin%2BRouterOS) describes FastTrack bypass behavior. Do not clear every connection or silently change FastTrack to manufacture a result. Record the actual scope; any policy improvement needs a separate version/test.

## Q: decoy-triggered WAN quarantine and recovery

Before: VM1 can reach an owned WAN TCP probe, VM2 LAN, and the proxy/admin paths work. VM1 is absent from `quarantine`; record actual flag/list state and counters. An independent node must keep checking the WAN probe.

Trigger on VM1:

```bash
timeout 5 nc -v -w 3 "$LAB_VM2_IP" 2222
```

Capture banner/connection, trap log and reaction journal within the run interval. A connection does not itself prove exploitation or reading the decoy file.

```bash
journalctl --utc -u suricata-block.service \
  --since "$LAB_START_UTC" --until "$LAB_END_UTC" \
  --no-pager -o short-iso-precise

ping -c 3 "$LAB_VM2_IP"
curl -sS --connect-timeout 3 --max-time 8 \
  "http://${LAB_WAN_PROBE_IP}:${LAB_WAN_PROBE_PORT}/health"
```

`/health` denotes a preselected/created owned test endpoint, not a known existing deployment artifact. Preserve exit codes and failed-connection observations. Repeat a new SSH session from VM2 to VM1 over WireGuard, without connection reuse, and a proxy request. Record private-key-free `wg show wg0 latest-handshakes` / `wg show wg0 transfer` summaries and sanitize public peer keys.

```text
/ip firewall address-list print detail where list=quarantine
/ip firewall filter print stats where src-address-list=quarantine
```

PASS requires matching trap/reaction/list evidence, actual outgoing WAN drop with a healthy control, and preserved LAN/new admin/proxy access. Test an existing WAN flow separately. Describe WAN-only quarantine accurately.

Selective recovery uses the actual VM1 address in place of this example address:

```text
/ip firewall address-list remove [find list=quarantine address=192.168.3.253]
```

After checking the real flag/state lifecycle, remove only its corresponding local flag on VM2:

```bash
sudo rm -- /tmp/vm1-quarantined.flag
```

Confirm no immediate re-add, consistent flag/router state and restored WAN/admin/proxy. Record any required maintenance stop/start and race handling. Normal legitimate traffic must not quarantine VM1; duplicate trap input must not produce an endless action stream.

## Visibility and robustness

Document the actual switch/mirror path. Prove a direct VM1->VM2 packet arrives at its destination, then compare the bounded live IDS window. Missing alert alone could be a rule error: replay the saved direct-path PCAP with the same rule in a separate sensor/output disconnected from response watchers. A replay match plus the absent live capture supports visibility diagnosis, not live detection. Do not publish unreviewed PCAPs.

Preserve the known TCP `!51820` versus UDP WireGuard distinction. A future VLAN/routed mirror improvement requires separate before/after topology and fresh tests.

After source review, test dependency failures with mocks/test copies; restart, log rotation, duplicate handling, below-policy/non-target sources, error-state logging and selective recovery. Confirm flag creation only after the chosen successful-action policy, explicit cooldown persistence and bounded retries. Record missed downtime events from `tail -n 0` if observed. These are future tests/improvements, not implemented claims.

## Measurements and completion

Record request, producer, first Loki visibility, evaluation, action, observed effect and recovery timestamps with clock assumptions. Distinguish HTTP latency, notification API acceptance and visible delivery. Predeclare any timing budget; report measured failures. For the main chains collect 3-5 independent repeats when feasible, publish N and min/median/max, and preserve inconclusive/failed runs.

A strong finished package includes actual code/configs, dashboard JSON, dependencies, three run dossiers with positive/negative/recovery evidence, a short triage timeline, explicit limitations and an executable reviewed recovery procedure. Future evidence/config additions require fresh scoped privacy review.
