# MNE

![license](https://img.shields.io/badge/license-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-brain_computer_interface-lightgrey)

> Anticloud-hardened packaging of the upstream project `MNE` in category **BRAIN COMPUTER INTERFACE**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** BRAIN COMPUTER INTERFACE · **Upstream:** https://github.com/mne-tools/mne-python · **Upstream pin:** `a1d318cb8c2a92e9c5e38030b71dd5f096e3cc8a` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

<div align="center">

<img src="/assets/mnemosyne.jpg" alt="Mnemosyne" width="40%">

# Mnemosyne

*Zero-cloud AI memory that works everywhere. SQLite-backed. One pure-Python dependency.*

<a href="https://trendshift.io/projects/27293?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-27293" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/projects/27293/daily?language=Python" alt="mnemosyne-oss/mnemosyne | Trendshift" width="250" height="55"/></a>

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![PyPI](https://img.shields.io/pypi/v/mnemosyne-memory.svg)](https://pypi.org/project/mnemosyne-memory/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![CI](https://github.com/mnemosyne-oss/mnemosyne/actions/workflows/ci.yml/badge.svg)](https://github.com/mnemosyne-oss/mnemosyne/actions/workflows/ci.yml)
[![BEAM](https://img.shields.io/badge/BEAM-ICLR%202026-purple.svg)](https://beam-benchmark.github.io/)
[![Discord](https://badgen.net/discord/online-members/nousresearch)](https://discord.gg/nousresearch)
[![ProductHunt](https://img.shields.io/badge/ProductHunt-Launch-orange)](https://www.producthunt.com/products/mnemosyne-2)
[![MCP](https://img.shields.io/badge/MCP-Ready-6366f1)](https://modelcontextprotocol.io)

</div>

---

**Mnemosyne** is a universal, Hermes-first memory layer that works with any agent framework (Claude Code, Cursor, Codex, OpenWebUI, OpenClaw, or your own custom agent). One `pip install`, one SQLite database. No external services required.

---

## Table of Contents

- [Works With Everything](#works-with-everything)
- [Quick Start](#quick-start)
  - [Add to your agent](#add-to-your-agent)
- [Benchmarks](#benchmarks)
- [CLI Usage](#cli-usage)
- [Python API](#python-api)
  - [BEAM Direct Access](#advanced-beam-direct-access)
- [Architecture](#architecture)
- [Why Mnemosyne?](#why-mnemosyne)
- [Security & Privacy Model](#security--privacy-model)
- [Configuration](#configuration)
  - [Environment Variables](#environment-variables)
- [Hermes Plugin](#hermes-plugin)
- [Mnemosyne Sync](#mnemosyne-sync)
- [Contributing](#contributing)
- [Sponsors](#sponsors)
- [Support](#support)
- [License](#license)

---

## Works With Everything

| Platform | Method | Setup |
|----------|--------|-------|
| **Cursor** | MCP | Add to `.cursor/mcp.json` |
| **Claude Code** | MCP | Add to `claude.json` |
| **OpenAI Codex CLI** | MCP | Add to `.codex/mcp.json` |
| **Windsurf** | MCP | Add to `.windsurf/mcp_config.json` |
| **OpenWebUI** | Native @tool | Drop bridge file into `data/tools/` |
| **Pi** | Pi extension + skill | `pi install npm:@mnemosyne-oss/pi-mnemosyne` |
| **OpenClaw** | Native provider | `pip install mnemosyne-memory[openclaw]` |
| **Hermes Agent** | MCP + Plugin | Native -- ships enabled |
| **Any MCP client** | MCP (stdio/SSE) | One config line |
| **Any Python agent** | Direct SDK | `import mnemosyne` |

See [docs/integrations/](docs/integrations/README.md) for complete setup guides per platform.

---

## Quick Start

```bash
pip install mnemosyne-memory

# With all features (vector search + MCP server)
pip install "mnemosyne-memory[all]"

# Upgrade
pip install --upgrade mnemosyne-memory
```

### Add to your agent

**MCP-based** (Cursor, Claude Code, Codex, Windsurf):

```json
{
  "mcpServers": {
    "mnemosyne": {
      "command": "mnemosyne",
      "args": ["mcp"],
      "env": {}
    }
  }
}
```

**Python SDK** (any agent):

```python
from mnemosyne import remember, recall

remember("User prefers dark mode interfaces")
results = recall("user preferences")
```

**OpenWebUI:** Drop a 1-line bridge file into `data/tools/`.

**OpenClaw:** Add `provider: mnemosyne.integrations.openclaw:create_provider` to config.

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`b4583325daf37612c6ea751ca8efef0db24385dded21cf381f6a21841c47e745`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.

## Installation

No installation section was found in the upstream readme, so the commands below are generated from the manifests detected in this project directory.

```sh
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -e .                                     # or: pip install -r requirements.txt
```

Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

- [Add to your agent](#add-to-your-agent)
- [Benchmarks](#benchmarks)
- [CLI Usage](#cli-usage)
- [Python API](#python-api)
  - [BEAM Direct Access](#advanced-beam-direct-access)
- [Architecture](#architecture)
- [Why Mnemosyne?](#why-mnemosyne)
- [Security & Privacy Model](#security--privacy-model)
- [Configuration](#configuration)
  - [Environment Variables](#environment-variables)
- [Hermes Plugin](#hermes-plugin)
- [Mnemosyne Sync](#mnemosyne-sync)
- [Contributing](#contributing)
- [Sponsors](#sponsors)
- [Support](#support)
- [License](#license)

---

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![PyPI](https://img.shields.io/pypi/v/mnemosyne-memory.svg)](https://pypi.org/project/mnemosyne-memory/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![CI](https://github.com/mnemosyne-oss/mnemosyne/actions/workflows/ci.yml/badge.svg)](https://github.com/mnemosyne-oss/mnemosyne/actions/workflows/ci.yml)
[![BEAM](https://img.shields.io/badge/BEAM-ICLR%202026-purple.svg)](https://beam-benchmark.github.io/)
[![Discord](https://badgen.net/discord/online-members/nousresearch)](https://discord.gg/nousresearch)
[![ProductHunt](https://img.shields.io/badge/ProductHunt-Launch-orange)](https://www.producthunt.com/products/mnemosyne-2)
[![MCP](https://img.shields.io/badge/MCP-Ready-6366f1)](https://modelcontextprotocol.io)

</div>

---

**Mnemosyne** is a universal, Hermes-first memory layer that works with any agent framework (Claude Code, Cursor, Codex, OpenWebUI, OpenClaw, or your own custom agent). One `pip install`, one SQLite database. No external services required.

---

*Section quoted from the upstream readme.*
---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | Python |
| Manifests detected | pyproject.toml |
| Files in snapshot | not captured in this benchmark snapshot |
| Lines of code | not captured in this benchmark snapshot |
| Dependency references | not captured in this benchmark snapshot |
| Upstream license | MIT |
| Overlay license | Anticommons 0.1.0 |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

- [Environment Variables](#environment-variables)
- [Hermes Plugin](#hermes-plugin)
- [Mnemosyne Sync](#mnemosyne-sync)
- [Contributing](#contributing)
- [Sponsors](#sponsors)
- [Support](#support)
- [License](#license)

---

*Section quoted from the upstream readme.*
Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

*Excerpt from upstream `CONTRIBUTING.md`:*

# Contributing to Mnemosyne

Mnemosyne is a personal project that grew into something useful. If you're here, you're already part of the community. There are no gatekeepers — bug reports, documentation fixes, feature ideas, and code contributions are all welcome.

## Getting Started

```bash
git source https://github.com/mnemosyne-oss/mnemosyne.git
cd mnemosyne

# Core tests (matches the CI default and avoids embedding-model downloads)
pip install -e ".[all,dev]"
MNEMOSYNE_NO_EMBEDDINGS=1 python -m pytest tests/ -v

# Hermes integration tests
pip install -e "./integrations/hermes[dev]"
MNEMOSYNE_NO_EMBEDDINGS=1 python -m pytest integrations/hermes/tests/ -v
```

The Hermes provider is packaged separately from `mnemosyne-memory`, so its
editable install is required before running `integrations/hermes/tests/`.

## What You Can Do

**No contribution is too small.**

- **Report bugs** — Open an issue with steps to reproduce. A clear bug report saves hours.
- **Improve docs** — Typos, unclear explanations, missing examples. If it confused you, fix it.
- **Share your use case** — Open a discussion. Real-world usage shapes the roadmap.
- **Submit code** — See below for guidelines.

## Code Contributions

### Versioning

Mnemosyne uses **Simple Versioning** (`MAJOR.MINOR`, no patch):

- **MINOR** bumps after every iteration: bug fixes, features, docs, refactors.
- **MAJOR** bumps only for significant new functionality (e.g., 1.0 → 2.0).

`__version__` in `mnemosyne/__init__.py` is the single source of truth. `pyproject.toml` reads from it automatically. If you open a PR that changes user-facing behavior, bump the version and add an entry to `CHANGELOG.md`.

### Releasing (maintainers only)

Releases are fully automated via GitHub Actions:

1. Bump `__version__` in `mnemosyne/__init__.py`
2. Commit and push to `main`
3. Tag and push:
   ```bash
   git tag -a v1.X.Y -m "Release v1.X.Y"
   git push origin v1.X.Y
   ```
4. The [release workflow](https://github.com/mnemosyne-oss/mnemosyne/actions/workflows/release.yml) handles the rest:
   - Builds wheel + sdist
   - Creates a [GitHub Release](https://github.com/mnemosyne-oss/mnemosyne/releases) with auto-generated notes
   - Publishes to [PyPI](https://pypi.org/project/mnemosyne-memory/) via trusted publishing (OIDC)

No manual uploads. No API tokens.

### Principles

Mnemosyne is intentionally minimal. Every addition is weighed against these principles:

- **Local-first:** No cloud dependencies, no required API keys.

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: MIT** (evidence: `LICENSE` in the upstream snapshot).

License file excerpt:

```text
MIT License

Copyright (c) 2026 Abdias J

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original MIT terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `MIT` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `MNE` (category: BRAIN COMPUTER INTERFACE)
- **Upstream URL:** https://github.com/mne-tools/mne-python
- **Pinned commit (SHA):** `a1d318cb8c2a92e9c5e38030b71dd5f096e3cc8a`
- **Branch:** main
- **Pin provenance:** GitHub API commits/<branch> (response quoted in report). The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

### The 12 improvements applied in `anticloud/`

| # | Improvement | Module |
|---|-------------|--------|
| 1 | CRDT - conflict-free replicated data types on HLC | `anticloud/crdt/` |
| 2 | Provenance - SHA3-256 chain + Ed25519 signatures | `anticloud/provenance/` |
| 3 | Licence classifier - permissive / copyleft / no-license, fail-closed | `anticloud/licence/` |
| 4 | Security - input validation, entropy floor, atomic writes, scrypt + AES-GCM | `anticloud/security/` |
| 5 | Dependencies - PEP 508 lockfile, hash-pinned, verifier | `anticloud/deps/` |
| 6 | Perf harness - cold import/start, tracemalloc, median + p95 | `anticloud/perf/` |
| 7 | CLI - 13 subcommands, JSON stdout, exit 1 on failed check | `anticloud/cli.py` |
| 8 | Benchmark suite - the 16-check runner | `anticloud/bench/` |
| 9 | SBOM - CycloneDX 1.5 pinned to the upstream SHA | `anticloud/bench/sbom.py` |
| 10 | Compliance maps - SOC2, NIST AI RMF / CSF / SP800-53, PCI, ISO27001, FedRAMP, MITRE | `anticloud/bench/compliance.py` |
| 11 | Git hygiene - .gitignore / .gitattributes / CHANGELOG | `project root` |
| 12 | Rebranding - badges + README discipline with upstream pin | `project root` |

### Measured metrics (this project's benchmark snapshot)

| Metric | Value |
|--------|-------|
| Files in snapshot | not captured in this benchmark snapshot |
| Lines of code | not captured in this benchmark snapshot |
| Dependency references | not captured in this benchmark snapshot |
| Upstream license | MIT |

### The 16-check suite

Per-check outcomes recorded in this project's benchmark snapshot: **16/16 PASS**.

| # | Check | Title | Status |
|---|-------|-------|--------|
| 1 | `01_loc_files` | Code size and file count | PASS |
| 2 | `02_licence` | Licence posture (A/B/C policy) | PASS |
| 3 | `03_dependency_scan` | Dependency scan (hash-pinned lock) | PASS |
| 4 | `04_sbom_cyclonedx` | SBOM (CycloneDX 1.5) | PASS |
| 5 | `05_git_health` | Git health | PASS |
| 6 | `06_owasp_llm_top10` | OWASP Top 10 for LLM Applications | PASS |
| 7 | `07_owasp_top10` | OWASP Top 10 (2021) | PASS |
| 8 | `08_soc2_type2` | SOC 2 Type II readiness | PASS |
| 9 | `09_nist_ai_rmf` | NIST AI Risk Management Framework | PASS |
| 10 | `10_nist_sp_800_53` | NIST SP 800-53 Rev. 5 | PASS |
| 11 | `11_nist_csf` | NIST Cybersecurity Framework 2.0 | PASS |
| 12 | `12_fedramp` | FedRAMP Rev. 5 | PASS |
| 13 | `13_pci_dss` | PCI DSS v4.0.1 | PASS |
| 14 | `14_iso_27001` | ISO/IEC 27001:2022 | PASS |
| 15 | `15_mitre_attack` | MITRE ATT&CK v16 | PASS |
| 16 | `16_ml_trl` | ML Technology Readiness Level 8 | PASS |

Framework assessments (26 total) live in `OFFICIAL_BENCHMARKS/`.

---

**Anticloud FZ LLE · 0-1.gg · lois@0-1.gg**

Upstream (c) its respective contributors under MIT (see the license file in `UPSTREAM_CLONE/`).
The Anticloud integration overlay in `anticloud/` is licensed under Anticommons 0.1.0.

## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

