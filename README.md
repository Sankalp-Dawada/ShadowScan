# ShadowScan

> Read-only API security recon — find zombie endpoints and leaked secrets before attackers do.

[![Status](https://img.shields.io/badge/status-in%20development-yellow)]()
[![License](https://img.shields.io/badge/license-MIT-blue)]()

## The Problem

Modern APIs sprawl fast. Old versions stay live after "deprecation," internal
debug routes leak into production, and secrets end up in response bodies or
headers by accident. These "zombie" endpoints and leaked credentials are a
real, common attack surface — not exploited through anything clever, just
things that were forgotten. <!-- TODO: add 1-2 sentence stat/citation from OWASP API Security Top 10 (e.g. API9:2023 Improper Inventory Management) -->

ShadowScan is a lightweight, read-only recon tool that finds both problems
before an attacker does.

## What It Does / Doesn't Do

- ✅ Passive, read-only reconnaissance only
- ✅ Zombie API detection — diffs your OpenAPI/Swagger spec against what's
  actually live
- ✅ Secret leakage detection — scans responses for exposed keys, tokens, and
  credentials using pattern matching + entropy analysis
- ❌ No exploitation
- ❌ No authentication bypass
- ❌ No active attacks against targets you don't own or have permission to test

<!--## Demo-->

<!-- TODO: record asciinema/GIF once CLI + vulnerable test API are working (Week 3-4) -->
<!--`[demo GIF / asciinema link goes here]`-->

## Architecture

```
shadowscan/
├── core/
│   ├── spec_parser.py       # parses OpenAPI/Swagger JSON/YAML
│   ├── endpoint_prober.py   # probes live endpoints
│   ├── zombie_detector.py   # diffs spec vs. live reality
│   ├── secret_scanner.py    # regex + entropy scanning
│   └── report_generator.py  # builds markdown/JSON reports
├── rules/
│   ├── secret_patterns.yaml
│   └── entropy_config.yaml
├── db/
│   └── scan_history.db
├── cli.py
├── tests/
├── examples/
│   └── vulnerable-api-demo/  # intentionally flawed test API used for demos
├── README.md
└── pyproject.toml
```

<!-- TODO: replace with an actual diagram image once modules are built -->

## Quickstart

<!-- TODO: fill in once cli.py exists (Week 3) -->
```bash
git clone https://github.com/Sankalp-Dawada/ShadowScan.git
cd shadowscan
pip install -r requirements.txt

shadowscan scan --spec openapi.json --url https://targetexample.com --output reportexample.md
```

## Design Decisions

<!-- TODO: fill in as you make real decisions, don't write these speculatively -->
- **Why regex + entropy hybrid for secret detection:** _TODO — write after Week 2_
- **Why SQLite for scan history:** _TODO — write after Week 3_
- **How false positives were reduced:** _TODO — write after tuning in Week 2_

## Project Status (Day 1 / Week 1)

This project is being built in public over 4 weeks. Current status:

- [ ] Repo scaffolding + pre-commit hooks (black, ruff)
- [ ] `spec_parser.py` — parse OpenAPI 3.0 spec into normalized endpoint list
- [ ] `endpoint_prober.py` — probe documented + common undocumented paths
- [ ] `zombie_detector.py` — diff spec vs. live reality
- [ ] Vulnerable test Flask API with intentional zombie endpoints
- [ ] `secret_patterns.yaml` + `secret_scanner.py` (Week 2)
- [ ] Entropy-based fallback detection (Week 2)
- [ ] CLI via Typer (Week 3)
- [ ] SQLite scan history (Week 3)
- [ ] Report generator — markdown + JSON output (Week 3)
- [ ] Unit tests + GitHub Actions CI (Week 4)
- [ ] Demo recording (Week 4)
- [ ] Companion blog post (Week 4)

## Roadmap (Post-MVP)

- BFLA (Broken Function Level Authorization) testing module
- LLM attack chain testing module
- Open-source Nipper-replacement module with GUI + sandbox execution
- Minimal FastAPI dashboard for viewing scan reports over time

## Responsible Use

<!-- TODO: expand into a full SECURITY.md before first public release -->
Only run ShadowScan against systems you own or have explicit written
permission to test.

## License

MIT
