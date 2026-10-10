# Repository status and structure

This repository contains architecture, setup notes and 25 historical screenshots. Nineteen image copies have unchanged decoded pixels; six have small masks over password values or lab WAN endpoints. Original runtime artifacts are still missing. No license is assigned.

```text
security-monitoring-response-lab/
├── README.md
├── .gitignore
├── docs/
│   ├── architecture.md
│   ├── deployment.md
│   ├── detection-and-response.md
│   ├── testing.md
│   ├── troubleshooting.md
│   ├── limitations.md
│   ├── report.ru.md
│   ├── artifact-request.md
│   ├── material-inventory.md
│   ├── portfolio-evidence.md
│   ├── screenshots.md
│   ├── sanitization.md
│   ├── verification.md
│   ├── local-commit.md
│   ├── evidence-runbook.md
│   ├── templates/test-run.md
│   └── repository-status.md
├── configs/
│   ├── loki/.gitkeep
│   ├── alloy/.gitkeep
│   ├── rsyslog/.gitkeep
│   ├── suricata/.gitkeep
│   ├── mikrotik/.gitkeep
│   ├── wireguard/.gitkeep
│   └── systemd/.gitkeep
├── scripts/.gitkeep
├── dashboards/.gitkeep
├── assets/screenshots/
│   ├── README.md
│   ├── s*.png (23 PNG copies)
│   ├── grafana-service-status.jpg
│   └── loki-service-status.jpg
└── samples/sanitized-events/.gitkeep
```

[Safe original exports](artifact-request.md) are needed to replace the empty directories. They are not substitute implementation examples. [Verification](verification.md) records document/privacy checks; [repository commands](local-commit.md) explain cloning and reviewing this project. Source reports, private audit and old portfolio material are outside this tree.
