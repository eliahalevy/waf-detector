# WAF Detection Tools

Two Python scripts for detecting Web Application Firewalls (WAF) across domains and subdomains.

---

## Tools Overview

| | `waf_detector.py` | `waf_scanner_report.py` |
|---|---|---|
| **Input** | CLI arguments or a `.txt` file | Paste domains directly inside the script |
| **Output** | Terminal report + optional `.txt` file + optional `.json` | Terminal table + `waf_report.csv` |
| **Best for** | One-off scans, automation, scripting | Bulk scans pasted from Excel |
| **Extra outputs** | Detailed per-signal report | Clean CSV ready to open in Excel |

---

## Requirements

```bash
pip3 install requests
```

---

## waf_detector.py

Full-featured CLI scanner. Pass domains as arguments or from a file.

**Usage:**

```bash
# Scan a single domain
python3 waf_detector.py -d example.com

# Scan multiple domains
python3 waf_detector.py -d cloudflare.com sucuri.net akamai.com

# Scan from a text file (one domain per line)
python3 waf_detector.py -f domains.txt

# Save report to file
python3 waf_detector.py -f domains.txt -o report.txt

# Also export raw results as JSON
python3 waf_detector.py -f domains.txt -o report.txt --json
```

**Output includes:**
- WAF detected: Yes / No
- Vendor identification
- Confidence score (Medium / High / Very High)
- All signals found per domain with full detail
- Optional `.txt` report and `.json` export

---

## waf_scanner_report.py

Paste-and-run bulk scanner. No CLI needed — just paste your domains inside the script and run it.

**How to use:**

1. Open `waf_scanner_report.py` in any text editor
2. Find the `DOMAINS_RAW` block at the top
3. Copy your domain column from Excel and paste it between the triple quotes:

```python
DOMAINS_RAW = """
yourcompany.com
app.yourcompany.com
portal.yourcompany.com
"""
```

4. Run it:

```bash
python3 waf_scanner_report.py
```

**Output includes:**
- Live progress printed to terminal
- Formatted table printed at the end
- `waf_report.csv` saved automatically — ready to open in Excel

---

## Detection Methods

Both tools use the same 5-method detection engine:

| Method | What it checks |
|---|---|
| Header Detection | WAF-specific HTTP response headers (e.g. `cf-ray`, `x-sucuri-id`) |
| Cookie Fingerprint | WAF-injected cookies (e.g. `__cf_bm`, `visid_incap_`) |
| Response Code Analysis | HTTP 403/406/429 returned for malicious payloads vs normal requests |
| Block Page Content | WAF vendor keywords in response body |
| Timing Analysis | Response time delta between clean and malicious requests |

**Confidence scoring:**

| Unique signal methods found | Score |
|---|---|
| 1 method | 50% — Medium |
| 2 methods | 75% — High |
| 3+ methods | 95% — Very High |

---

## Supported WAF Vendors

Cloudflare · Imperva (Incapsula) · Akamai · Sucuri · AWS WAF · F5 BIG-IP · Barracuda · Fortinet FortiWeb · ModSecurity · Wordfence
