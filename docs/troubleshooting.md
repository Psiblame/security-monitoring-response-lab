# Troubleshooting notes

These notes combine recorded in the setup notes fixes with unexecuted checks to perform on the lab. Preserve access and inspect the actual rules/configurations before making changes.

| Symptom | Documented cause / fix | Follow-up still needed |
| --- | --- | --- |
| Router logs never arrive | VM2 UFW blocked UDP 514; sender-specific permission was added | Verify actual router sender address, rsyslog input, received messages and file ingestion; UDP delivery/loss is unmeasured |
| Router log file not writable | Directory owner did not permit the `syslog` account; ownership corrected | Confirm daemon identity and narrow directory/file permissions, log rotation and Alloy read access; do not grant world-write access |
| WireGuard has no handshake / 0 received | VM2 UFW blocked UDP 51820; a VM1-only rule fixed it | Confirm underlay endpoint, UDP listener, routes and AllowedIPs; use a private-key-free status summary, not full key output |
| VM1 SSH fails over tunnel | Report uses TCP 2222 rather than 22 | Check destination overlay address, listener and firewall; handshake alone does not prove SSH reachability |
| Local rule loads but never triggers | Hypervisor switch forwards VM-to-VM traffic directly; router TZSP mirror misses it | Check capture location and sanitized EVE output. A loaded rule does not create visibility. Trap logs cover only TCP 2222 |
| Correlation messages rare | One-minute overlap window often excludes one source; a three-minute window was tried | Check timestamps, source-IP extraction and ingestion delay before changing requirements; no delivery-latency measurement exists |
| Repeated or missing quarantine | Flag plus `tail -n 0` described | Review actual flag lifecycle, restarts, log rotation and SSH failure handling; skipping historical lines can also miss downtime events |

The deployment account has no proof of timezone synchronization, retention, syslog transport reliability or exact service privileges. These are export/review items, not confirmed defects. Keep the already demonstrated blind spot explicit when troubleshooting detections.
