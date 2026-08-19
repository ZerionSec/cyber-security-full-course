# 🌿 OSINT PARADISE

**Comprehensive Guide to OSINT Tools on GitHub**  
Installation methods for Linux • Tips for effective investigations

> Open Source Intelligence (OSINT) is crucial for gathering publicly available information. This guide covers the best OSINT tools available on GitHub, how to install them on Linux, and how to use them effectively.

---

## 🧰 Curated Resource Lists (Starting Points)

| Repository | Stars | Description |
|------------|-------|-------------|
| [jivoi/awesome-osint](https://github.com/jivoi/awesome-osint) | ~27k | The definitive list of OSINT tools & resources across 40+ categories. |
| [lockfale/OSINT-Framework](https://github.com/lockfale/OSINT-Framework) | ~11.9k | Interactive mindmap of ~700 OSINT tools. Visit [osintframework.com](https://osintframework.com) |
| [rawfilejson/awesome-osint-arsenal](https://github.com/rawfilejson/awesome-osint-arsenal) | ~1.7k | 753+ tools in 50 categories with a one-command installer. |

---

## 🚀 All-in-One / Automation Frameworks

| Tool | Description |
|------|-------------|
| **SpiderFoot** | Python automation platform with 200+ modules. Excellent for automated recon and reporting. |
| **Recon-ng** | Full-featured, modular reconnaissance framework (similar to Metasploit for OSINT). |
| **sn0int** | Semi-automatic OSINT framework & package manager. |
| **OSINT-V2** | Terminal-based Python reconnaissance toolkit. |
| **Corvid** | Self-hosted OSINT workbench with a unified search bar. |

---

## 👤 Username & Social Media OSINT

| Tool | Description |
|------|-------------|
| **Maigret** | Collects user profiles from 3000+ sites and generates detailed reports. |
| **Sherlock** | Find usernames across 400+ social networks. One of the most popular tools. |
| **blackbird** | Username/email search across 600+ platforms. |
| **Personagraph** | Identity resolution dossier for username/email/phone. |
| **E4GL30S1NT** | Modular CLI with userrecon (71+ platforms), mailfinder, and more. |
| **Nexfil** | OSINT tool for finding profiles by username. |

---

## 💻 GitHub-Specific OSINT Tools

| Tool | Description |
|------|-------------|
| **Gitxray** | Leverages GitHub REST APIs for OSINT & forensics. |
| **GitFive** | Investigates GitHub profiles (name history, email → account). |
| **ghspy / gitspyx** | Extract intelligence from any GitHub user profile. |
| **gh-fake-analyzer** | Detects suspicious activity patterns in GitHub profiles. |
| **TruffleHog / GitDorker** | Detect exposed secrets and sensitive data in repositories. |
| **Gitleaks / git-hound** | Scan for secrets, API keys, and credentials in git history. |

---

## 📧 Email, Phone & Identity OSINT

| Tool | Description |
|------|-------------|
| **theHarvester** | Gathers emails & subdomains from public sources (search engines, PGP, etc.). |
| **Holehe** | Checks if an email is registered on 120+ platforms. |
| **PhoneInfoga** | Advanced phone number scanning and information gathering. |
| **IntelOSINT** | Social media, phone, and domain OSINT toolkit. |

---

## 🌐 Domain & Network OSINT

| Tool | Description |
|------|-------------|
| **Amass** | Deep subdomain enumeration using multiple techniques (active + passive). |
| **Knockpy** | Subdomain enumeration scanner. |
| **ContrastAPI** | Security intelligence server with 49 tools. |

---

## 🐧 Installation Guide for Linux

### 1. One-Command Mega Installers

```bash
# 753+ tools, 50 categories (Kali / Debian / Ubuntu / Parrot best)
git clone https://github.com/rawfilejson/awesome-osint-arsenal && cd awesome-osint-arsenal && sudo bash install.sh
```

Or install OSINT tools only:

```bash
sudo bash osint.sh
```

Full OSINT workstation setup (Ubuntu 24.04 LTS) with Argos:

```bash
git clone https://github.com/SOsintOps/Argos.git ~/Downloads/Argos
chmod +x ~/Downloads/Argos/setup.sh && ~/Downloads/Argos/setup.sh
```

### 2. Using Package Managers (Kali / Debian / Ubuntu)

```bash
sudo apt update
sudo apt install spiderfoot recon-ng theharvester sherlock amass sn0int
```

### 3. Cloning from GitHub (Python / pip)

```bash
# Recon-ng example
git clone https://github.com/lanmaster53/recon-ng.git && cd recon-ng
pip install -r REQUIREMENTS
```

```bash
# Sherlock example
git clone https://github.com/sherlock-project/sherlock.git
cd sherlock
python3 -m pip install -r requirements.txt
python3 sherlock.py <username>
```

### 4. Go-Based Tools

```bash
go install github.com/tillson/git-hound@latest
go install github.com/gitleaks/gitleaks/v8@latest
```

### 5. Dedicated Installer Scripts

```bash
# E4GL30S1NT - modular OSINT CLI
wget https://raw.githubusercontent.com/C0MPL3XDEV/E4GL30S1NT/main/linuxinstall.sh && bash linuxinstall.sh
```

---

## 💡 Tips & Tricks for Better OSINT

- **Start with frameworks** — Use [OSINT Framework](https://osintframework.com) or SpiderFoot to plan investigations and avoid getting lost.
- **Master GitHub search** — Use advanced filters for code, repos, users, and issues. GitHub reveals tech stacks, relationships, and accidental data exposure.
- **Use GitHub API tokens** — Unauthenticated requests hit rate limits fast. Create a read-only personal access token.
- **Verify and correlate** — Always cross-reference findings across multiple tools (e.g. Maigret + Sherlock + Personagraph).
- **Automate** — Use frameworks like Recon-ng and SpiderFoot to run concurrent queries. Tools like Corvid centralize lookups.
- **Check for leaked secrets** — Regularly scan with TruffleHog, Gitleaks, or git-hound.
- **Analyze metadata** — Use ExifTool to extract GPS coordinates, device info, and authorship from images and documents.
- **Master Google Dorks** — Operators like `site:`, `filetype:`, `intitle:`, and `inurl:` uncover hidden information.
- **Stay organized** — Prefer tools with audit logging and session tracking. Keep notes of every source.
- **Stay legal & ethical** — Only collect publicly available information. Never access systems without authorization.

---

## ⚠️ Disclaimer

Always use these tools **ethically and legally**.  
Only investigate systems you own or have explicit permission to test.

This material is for **educational and research purposes only**.

---

**Related standalone repository:** [ZerionSec/osint-paradise](https://github.com/ZerionSec/osint-paradise)
