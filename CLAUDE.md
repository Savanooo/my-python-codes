# CLAUDE.md

This file provides guidance to AI assistants (Claude and others) working with this repository.

---

## Repository Overview

**Name**: my-python-codes
**Purpose**: A personal collection of practical Python programs covering GUI games, CLI utilities, and network security tools.
**Language**: Python 3 (requires 3.10+ for union type syntax `str | None` used in the port scanner)
**Note**: The README.md describes two security scripts (DNS Beaconing Detector, EDR-Style Process Detection) that are not currently present in the repository. The actual codebase contains four different projects listed below.

---

## Project Structure

```
my-python-codes/
├── CLAUDE.md                              # This file
├── README.md                              # High-level project description
├── blackjack game by python/
│   ├── blackjack game with python         # Tkinter blackjack card game (432 lines)
│   └── READNE.db                          # Binary database file (ignore)
├── calculator w python/
│   ├── calculator with python             # CLI arithmetic calculator (40 lines)
│   └── README.db                          # Binary database file (ignore)
├── racing game w python/
│   ├── racing game                        # Tkinter 2D racing game (349 lines)
│   └── README.db                          # Binary database file (ignore)
└── port scanner w python /                # Note: trailing space in directory name
    ├── port scanner w python              # Multi-threaded TCP port scanner (375 lines)
    └── README.db                          # Binary database file (ignore)
```

### Important path note

The directory `port scanner w python ` has a **trailing space** in its name. Always quote the path when referencing it in shell commands:

```bash
python3 "port scanner w python /port scanner w python" --help
```

### `.db` files

The `README.db` / `READNE.db` files in each subdirectory are binary SQLite database files, not text documentation. Do not attempt to read or edit them as text.

---

## Individual Projects

### 1. Blackjack Game (`blackjack game by python/blackjack game with python`)

- **Type**: GUI application
- **Framework**: Tkinter (Python standard library)
- **Language in source**: Turkish (variable names, comments, UI text)
- **Entry point**: Run directly — no `if __name__ == "__main__"` guard; the `Blackjack` class is instantiated at the bottom of the file
- **Key class**: `Blackjack`
- **Features**: Full blackjack rules, Unicode card symbols, betting system, ace value adjustment (11→1), blackjack bonus (1.5×), money/level tracking

**Run**:
```bash
python3 "blackjack game by python/blackjack game with python"
```

---

### 2. Calculator (`calculator w python/calculator with python`)

- **Type**: CLI REPL utility
- **Framework**: None (pure Python)
- **Language in source**: Turkish (comments, prompts, error messages)
- **Entry point**: Top-level script — executes immediately on run
- **Key function**: `hesapla(a, op, b)` — performs arithmetic
- **Supported operators**: `+`, `-`, `*`, `/`, `**`, `%`
- **Error handling**: Division by zero, modulo by zero, invalid numeric input

**Run**:
```bash
python3 "calculator w python/calculator with python"
```

---

### 3. Racing Game (`racing game w python/racing game`)

- **Type**: GUI application
- **Framework**: Tkinter Canvas
- **Language in source**: Turkish (variable names, comments, UI text)
- **Entry point**: Run directly — game loop starts at the bottom of the file
- **Key class**: `RacingGame`
- **Features**: 2D road rendering with animated lane lines, player car (arrow keys / A–D), enemy cars with collision detection, score and level progression, high score tracking, increasing difficulty per level

**Run**:
```bash
python3 "racing game w python/racing game"
```

---

### 4. Port Scanner (`port scanner w python /port scanner w python`)

- **Type**: CLI network tool
- **Framework**: None (stdlib: `socket`, `argparse`, `concurrent.futures`, `dataclasses`, `json`, `csv`)
- **Language in source**: English
- **Entry point**: `if __name__ == "__main__"` guard with `argparse`
- **Requires Python**: 3.10+ (uses `str | None` union type syntax)
- **Key classes**:
  - `ScanResult` (dataclass) — holds per-port result data
  - `PortScanner` — all scanning logic

**Features**:
- Multi-threaded scanning via `ThreadPoolExecutor` (default 200 workers)
- IPv4 and IPv6 support
- Banner grabbing
- Service name mapping (66 well-known ports built in)
- Scan modes: `quick` (top 20 ports), `top1024`, `custom`
- Custom port spec: ranges (`1-1024`) and lists (`22,80,443`)
- Export results to JSON or CSV
- Configurable timeout and thread count

**Run examples**:
```bash
# Quick scan of top 20 ports
python3 "port scanner w python /port scanner w python" example.com --mode quick

# Custom port range with JSON export
python3 "port scanner w python /port scanner w python" 192.168.1.1 --mode custom --ports 1-1024 --output results.json

# Show all options
python3 "port scanner w python /port scanner w python" --help
```

---

## Code Conventions

### Naming

| Context | Convention |
|---------|------------|
| Class names | `PascalCase` (e.g., `Blackjack`, `PortScanner`, `RacingGame`) |
| Method / function names | `snake_case` |
| Turkish projects | Identifiers may be Turkish words (e.g., `oyuncu_kartlar`, `deste`, `bahis`, `hesapla`) |
| English projects | Standard English identifiers |

### Language split

- **Games and calculator**: Written in Turkish — comments, variable names, and UI strings are all Turkish. Do not assume English when reading those files.
- **Port scanner**: Written in English — comments, docstrings, and all identifiers use English.

### Code style

- No linting or formatting configuration exists (no `.pylintrc`, no `pyproject.toml` with Black/isort settings).
- Files use **UTF-8** encoding (`# -*- coding: utf-8 -*-` declared in the port scanner).
- The port scanner uses type hints; the other files do not.
- Section dividers (`# -----------------------------`) are used in the port scanner to separate logical blocks.

### Error handling

- GUI apps use `tkinter.messagebox` for user-facing errors.
- CLI scripts use `try/except` around `input()` for input validation.
- The port scanner catches socket-level exceptions per thread and records `"filtered"` or `"closed"` status.

---

## Dependencies

All four projects use only the **Python standard library**. There are no third-party packages to install.

| Project | Standard library modules used |
|---------|-------------------------------|
| Blackjack | `tkinter`, `random` |
| Calculator | None beyond builtins |
| Racing Game | `tkinter`, `random` |
| Port Scanner | `socket`, `argparse`, `ipaddress`, `json`, `csv`, `time`, `dataclasses`, `datetime`, `concurrent.futures` |

No `requirements.txt`, `setup.py`, or `pyproject.toml` exists because there are no external dependencies.

---

## Running the Projects

Since the source files have no `.py` extension, run them by passing the full path to the Python interpreter:

```bash
# From the repo root
python3 "blackjack game by python/blackjack game with python"
python3 "calculator w python/calculator with python"
python3 "racing game w python/racing game"
python3 "port scanner w python /port scanner w python" <target> [options]
```

The GUI applications (blackjack, racing game) require a display environment (X11/Wayland on Linux, or a desktop environment). They will fail in headless terminals.

---

## Testing & CI

- **No tests exist.** There are no `tests/` directories, no `test_*.py` files, and no testing framework is configured.
- **No CI/CD.** There are no GitHub Actions workflows, `.travis.yml`, or any other CI configuration.

If adding tests, `pytest` is the recommended framework for this type of project.

---

## Git Workflow

- The repository uses feature branches prefixed with `claude/` for AI-assisted work.
- Commit messages in the history are short imperative sentences (e.g., `Create racing game`, `Delete portscanner.py`).
- There is no enforced commit message convention or pre-commit hooks.

---

## Known Issues / Caveats

1. **No `.py` extensions** — source files lack the standard `.py` extension, which means IDEs and linters may not automatically recognize them as Python. Pass the interpreter explicitly (`python3 <file>`).
2. **Trailing space in directory name** — `port scanner w python ` ends with a space; always quote the path in shell commands.
3. **README mismatch** — `README.md` describes scripts (DNS Beaconing Detector, EDR Process Detection) that do not exist in the repository.
4. **Minimum Python version** — The port scanner uses `str | None` union syntax, which requires Python 3.10+. The other scripts are compatible with Python 3.6+.
5. **Headless incompatibility** — Tkinter-based projects (blackjack, racing game) cannot run in headless/server environments without a virtual display (e.g., `Xvfb`).
