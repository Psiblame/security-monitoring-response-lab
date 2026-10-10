# Repository status and structure

Documentation reviewed on 2026-10-10; original runtime artifacts are missing. Twenty-five source images have been reviewed. Two safe copies are included with metadata removed and unchanged pixels. The other 23 originals remain private because identifying details have not been masked. No license is assigned.

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
│   ├── grafana-service-status.jpg
│   └── loki-service-status.jpg
└── samples/sanitized-events/.gitkeep
```

[Safe original exports](artifact-request.md) are needed to replace the empty directories. They are not substitute implementation examples. [Verification](verification.md) records document/privacy checks; [repository commands](local-commit.md) explain cloning and reviewing this project. Source reports, private audit and old portfolio material are outside this tree.
