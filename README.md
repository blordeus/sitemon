# sitemon

A CLI tool that audits websites for performance, uptime, SSL health, and redirect chains. Supports one-off audits and scheduled monitoring with persistent history logging.

Built for freelancers and agencies managing multiple client sites.

---

## Features

- **Full site audit** — response time, HTTP status, redirects, SSL expiry, page size
- **Health scoring** — OK / WARNING / SLOW / ERROR / DOWN per site
- **Scheduled monitoring** — run every N minutes and log results over time
- **Excel export** — color-coded report with results, summary, and history sheets
- **History log** — every run is saved locally for trend analysis
- **File input** — pass a text file with one URL per line (supports `#` comments)

---

## Setup

**1. Clone the repo**
```bash
git clone https://github.com/blordeus/sitemon.git
cd sitemon
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

---

## Usage

```bash
# Audit specific URLs
python sitemon.py --urls https://example.com https://another.com

# Audit from a file
python sitemon.py --file sites.txt

# Export to Excel
python sitemon.py --file sites.txt --output report.xlsx

# Scheduled monitoring (every 30 minutes)
python sitemon.py --file sites.txt --schedule 30 --output monitor.xlsx

# View audit history
python sitemon.py --history

# Run without exporting
python sitemon.py --urls https://example.com --no-export
```

---

## sites.txt Format

```
# My client sites
https://clientone.com
https://clienttwo.com

# My own sites
https://bryanlordeus.com
```

Lines starting with `#` are treated as comments and skipped.

---

## Thresholds

| Metric | Warning | Critical |
|--------|---------|----------|
| Response time | > 1,500ms | > 3,000ms |
| SSL expiry | < 30 days | Expired |
| HTTP status | — | 4xx / 5xx |

---

## Output

### Terminal
```
[1/3] Checking https://example.com... ✅ OK (312ms)
[2/3] Checking https://slow-site.com... 🐢 SLOW (3200ms)
[3/3] Checking https://broken.com... ❌ ERROR
```

### Excel Report (3 sheets)
- **Audit Results** — current run, color-coded by status
- **Summary** — totals, averages, SSL warnings
- **History** — last 200 entries across all runs

---

## Project Structure

```
sitemon/
├── sitemon.py        ← main script
├── requirements.txt
├── sites.txt         ← example URL list (add your own)
├── .gitignore
└── README.md
```

---

## Tech Stack

- [requests](https://docs.python-requests.org/) — HTTP checks
- [openpyxl](https://openpyxl.readthedocs.io/) — Excel export
- [schedule](https://schedule.readthedocs.io/) — scheduled runs
- Python standard library: `ssl`, `socket`, `argparse`, `json`, `pathlib`

---

## License

MIT
