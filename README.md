# osint
inspiration from usershearch via reddit
A powerful **2-in-1 OSINT suite** engineered for deep **Email and Username Intelligence**.

With **290+ total scan vectors**—including **105+ email-integrated sites** and **185+ username platforms**—you can map digital footprints, analyze target behavior, uncover interests, and verify account registrations in seconds.

The ultimate reconnaissance tool for hunting down targets using just an email or username—now fully integrated with **Hudson Rock** for instant data breach intelligence.


## Features

- ✅ **Deep Email & Username OSINT:** Look up email registrations and perform advanced username profiling across 290+ platforms.
- ✅ **Profile Data Extraction:** Goes beyond basic availability checks to scrape and extract rich metadata, account details, and digital footprints from target profiles.
- ✅ **Dual-Mode Engine:** Run targeted email campaigns, massive username sweeps, or simultaneous dual-identifier scans.
- ✅ **Granular Status Reporting:** Get crystal-clear results (`Registered`/`Available` for emails; `Found`/`Not Found`/`Error` for usernames) backed by precise exception handling.
- ✅ **Modular & Extensible:** Built on a highly decoupled, modular architecture, adding new platform modules takes just a few lines of code.
- ✅ **Mass Bulk Scanning:** High-throughput processing for bulk lists of usernames and emails via structured input files.
- ✅ **Permutation Generator:** Wildcard-based username variation generation to catch typosquatting or alternative aliases.
- ✅ **Multi-Format Export:** Clean console output paired with structured, automated exports to **JSON** and **CSV** for easy pipeline integration.
- ✅ **Advanced Proxy Rotation:** Built-in proxy pivoting with automated rotation and pre-scan health checks to bypass strict rate-limiting.
- ✅ **Smart Auto-Update System:** Keeps your signatures and modules fresh with interactive, seamless PyPI update prompts.

## Virtual Environment (optional but recommended)

```bash
# create venv
python3 -m venv .venv
````
## Activate venv
```bash
# Linux / macOS
source .venv/bin/activate

# Windows (PowerShell)
.venv\Scripts\Activate.ps1
```
## Installation

#### 🐍 Via PyPI (Standard Python Setup)
```bash
# Upgrade pip to the latest version
python3 -m pip install --upgrade pip

# Install the package globally or in your virtual environment
pip install user-scanner
```

#### ❄️ Via Nix (Linux & macOS)

```bash
# Run the scanner instantly without installing anything permanently
nix run github:kaifcodec/user-scanner/main -- --help

# Drop into a temporary shell where the 'user-scanner' command is active
nix shell github:kaifcodec/user-scanner/main

# (For Developers) Clone the repo and drop into an isolated workspace
nix develop .
```

---
### Important Flags

See [Important flags](docs/FLAGS.md) here and use the tool powerfully


## Usage

### Basic username/email scan

Scan a single email or username across **all** available modules/platforms:

```bash
user-scanner -e johndoe@gmail.com   # single email scanning 
user-scanner -u johndoe             # single username scanning 
```
### Verbose mode 

Use `-v` flag to show the url of the sites being checked
```bash
user-scanner -v -e johndoe@gmail.com -c dev
```
Output:
```sh
  ...
  [✔] Huggingface [https://huggingface.co] (johndoe@gmail.com): Registered
  [✔] Envato [https://account.envato.com] (johndoe@gmail.com): Registered
  [✔] Replit [https://replit.com] (johndoe@gmail.com): Registered
  [✔] Xda [https://xda-developers.com] (johndoe@gmail.com): Registered
  ...
```

### Selective scanning

Scan only specific categories or single modules:

```bash
user-scanner -u johndoe -c dev                # developer platforms only
user-scanner -e johndoe@gmail.com -m github   # only GitHub
```

### Bulk email/username scanning

Scan multiple emails/usernames from a file (one email/username per line):
- Can also be combined with categories or modules using `-c` , `-m` and other flags

```bash
user-scanner -ef emails.txt     # bulk email scan
user-scanner -uf usernames.txt  # bulk username scan
```

### Pattern generation
See [Pattern Syntax](docs/PATTERNS.md) for more details

---
### Library mode for email_scan
Only available for `user-scanner>=1.2.0`

See full usage (eg. category checks, full scan) guide [library usage](docs/USAGE.md)

- Email scan example (single module):

```python
import asyncio
from user_scanner.core import engine
from user_scanner.email_scan.shopping import etsy

async def main():
    # Engine detects 'email_scan' path -> returns "Registered" status
    result = await engine.check(etsy, "test@gmail.com")
    json_data = result.to_json() # returns JSON output
    csv_data = result.to_csv()   # returns CSV output
    print(json_data)             # prints the json data

asyncio.run(main())
```
Output:

```json
{
  "email": "test@gmail.com",
  "category": "Shopping",
  "site_name": "Etsy",
  "status": "Registered",
  "url": "https://www.etsy.com",
  "extra": {
    "id": 98832,
    "name": "test123",
    "username": "test123",
    "gender": "private",
    "is_seller": "No",
    "has_public_page": "No",
    "stats": "0 followers | 0 following | 0 favorites",
    "privacy": "Items are Public | Shops are Public",
    "joined": "2010-09-19 05:04:06",
    "last_profile_update": "2020-07-31 01:40:24",
    "avatar": "https://i.etsystatic.com/site-assets/images/avatars/default_avatar.png?width=400"
  },
  "reason": ""
}
```
---


### Using Proxies

Validate proxies before scanning (tests each proxy against google.com):

```bash
user-scanner -u johndoe -P proxies.txt --validate-proxies # recommended
```

This will:
1. Filter out non-working proxies
2. Save working proxies to `validated_proxies.txt`
3. Use only validated proxies for scanning
---
## Support the project

If this project helps you, consider supporting its development:
[GitHub Sponsor](https://github.com/sponsors/kaifcodec)

## Sponsors

Huge thanks to our amazing sponsors who support the development of `user-scanner`!

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/soxoj">
        <img src="https://github.com/soxoj.png?size=100" width="50px;" alt="soxoj"/>
        <br />
        <sub><b>@soxoj</b></sub>
      </a>
    </td>
  </tr>
</table>

---
