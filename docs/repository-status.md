# Repository status and structure

Documentation and all 25 public screenshot copies reviewed on 2026-10-10; original runtime artifacts are missing. Two JPEG copies have metadata removed and unchanged pixels. Twenty-three PNG copies use opaque masks over identifying fields, with every pixel outside the masks unchanged. Original files remain private. No license is assigned.

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
│   ├── s*.png (23 opaque-masked copies)
│   ├── grafana-service-status.jpg
│   └── loki-service-status.jpg
└── samples/sanitized-events/.gitkeep
```

[Safe original exports](artifact-request.md) are needed to replace the empty directories. They are not substitute implementation examples. [Verification](verification.md) records document/privacy checks; [repository commands](local-commit.md) explain cloning and reviewing this project. Source reports, private audit and old portfolio material are outside this tree.
