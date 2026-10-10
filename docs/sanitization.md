# Published data and redaction

Screenshots keep the diagnostic information needed to understand the lab: private IPs, generic system users and hostnames, paths, ports, source addresses in event records, public WireGuard keys, rule IDs and transaction/flow IDs. These fields are not passwords or authentication secrets.

Two password values in the decoy configuration and the lab's WAN endpoint addresses are covered with small opaque black masks. The decoy host, account, port and path fields remain visible. No WireGuard private-key value appears in the available screenshot; it displays `(hidden)`.

The gallery contains 25 images: 19 with unchanged decoded pixels and six with targeted masks. Capture metadata is removed. Every pixel outside the masks matches the original; no log text or output is regenerated.

Original captures, credentials, raw credential-bearing exports and private audit files stay outside this repository. Future configuration files must omit real passwords, tokens, SSH/WireGuard private keys, preshared keys and session data.

The architecture uses the lab's private addressing. Public ingress addresses remain `PUBLIC_ENDPOINT` in documentation. IP activity alone does not establish an attack or identify a person.

See the [screenshot index](screenshots.md), [gallery](../assets/screenshots/README.md) and [verification](verification.md).
