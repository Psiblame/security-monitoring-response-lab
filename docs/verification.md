# File and documentation checks

Checks completed on 2026-10-11 cover the repository files and screenshot copies.

- All 29 original source files retain their SHA-256 values.
- All 25 public copies have capture metadata removed.
- Nineteen images have unchanged decoded pixels.
- Six images have masks only on password values or lab WAN endpoints; all other pixels match the originals.
- Local/private addresses, generic hostnames and user names, ports, paths, public WireGuard keys and event IDs remain readable.
- Screenshot OCR and visual checks cover secret fields and remaining endpoint fragments.
- Relative links, Markdown fences and the Mermaid diagram text are checked.
- Text and metadata are checked for exposed credentials and unintended personal data.

These checks do not validate the running VMs or router. Full correlation, Telegram delivery, firewall effect, cooldown and recovery still need the test records listed in [testing](testing.md).

The [gallery](../assets/screenshots/README.md) and [selected evidence](portfolio-evidence.md) describe the visible results.
