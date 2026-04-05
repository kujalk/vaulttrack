<div align="center">

# 📈 VaultTrack

### Secure, offline investment portfolio tracker for macOS and Windows

[![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows-blue?style=for-the-badge)](https://github.com/your-username/vaulttrack/releases)
[![Security](https://img.shields.io/badge/encryption-AES--256--GCM-green?style=for-the-badge)](#-security)
[![License](https://img.shields.io/badge/license-Proprietary-orange?style=for-the-badge)](#)
[![Price](https://img.shields.io/badge/price-$9%20one--time-blueviolet?style=for-the-badge)](#-download)

**Your investments. Your device. Your data.**

[⬇ Download](#-download) · [Features](#-features) · [Security](#-security) · [FAQ](#-faq)

---

<!-- Replace with a real screenshot once you have one -->
> 📸 *Screenshots coming soon — build the app and take your own!*

</div>

---

## ✨ Features

| | Feature | Description |
|---|---|---|
| 🔐 | **AES-256-GCM Encryption** | Every record encrypted individually. Password never stored anywhere. |
| 📊 | **Rich Dashboard** | Portfolio value over time, allocation donut, monthly bar chart, currency breakdown. |
| 📋 | **Reusable Templates** | Save any date's entries as a template. Apply to new dates in one click. |
| 💱 | **Auto Currency Conversion** | Live rates via open.er-api.com (free, no key). Supports manual rates with date history. |
| 📤 | **Excel Backup & Import** | Export all data to .xlsx. Import back without duplicating existing records. |
| 🌗 | **Light & Dark Theme** | Beautiful dark-navy default with a clean light mode. Preference persisted. |
| 📴 | **100% Offline** | No account, no sync, no server. Works without internet. |
| 🗓️ | **Date Snapshots** | Log portfolio on any date. Navigate history instantly. |

---

## 🔒 Security

VaultTrack uses a **MEK/KEK dual-key architecture** — the same pattern used in professional password managers and enterprise disk-encryption tools.

```
Password  ──Argon2id──►  KEK (Key Encryption Key)   [RAM only]
                              │
                         AES-256-GCM
                              ▼
                         MEK (Master Encryption Key)  [RAM only]
                              │
                   AES-256-GCM × every DB record
                              ▼
                         investments.db              [ciphertext only]
```

### What this means for you

| Property | Detail |
|---|---|
| **Password never stored** | Not even hashed — mathematically unreconstructable without the original |
| **Argon2id KDF** | 64 MB memory, 3 passes — GPU brute-force is computationally infeasible |
| **Per-record encryption** | Each JSON record has its own AES-256-GCM ciphertext with a random nonce |
| **Password change** | Only re-wraps the MEK — no bulk re-encryption, instant |
| **DB file is safe to cloud-backup** | Contains only ciphertext — safe on Dropbox, OneDrive, etc. |

> ⚠️ **No password recovery exists by design.** If you forget your master password, your data cannot be recovered. Store it in a password manager.

---

## ⬇ Download

| Platform | Link |
|---|---|
| 🍎 **macOS** (Universal) | [Download .dmg](#) |
| 🪟 **Windows** (64-bit) | [Download .exe](#) |

> **One-time purchase · $9 · No subscription · All updates included**
>
> Purchase at: **[your-store-link-here]**

### System Requirements

| | Minimum |
|---|---|
| **macOS** | macOS 12 Monterey or later |
| **Windows** | Windows 10 (64-bit) or Windows 11 |
| **RAM** | 256 MB |
| **Disk** | 50 MB (plus your data) |

---

## 🚀 Getting Started

1. **Download** the binary for your platform above
2. **Run** the installer / .exe — no additional software needed
3. On first launch, **set a master password** (this encrypts your vault — remember it!)
4. Go to **Profile → Currency Preferences** to pick your base currency and preferred currencies
5. Head to **Investments** and start adding your first entries

---

## 📊 Dashboard Explained

The dashboard always shows your **current portfolio snapshot** — not a cumulative sum across all records. This is designed for investors who log the same holdings monthly: the latest record always represents where you stand today.

| Widget | What it shows |
|---|---|
| Portfolio Value | Total value of your **most recent record** |
| Monthly Chart | Value of the **latest snapshot per month** (last 12 months) |
| Asset Allocation | Breakdown of your **most recent record's** entries |
| Currency Distribution | Currency split from your **most recent record** |

---

## 💱 Currency Conversion

- Default provider: **[open.er-api.com](https://open.er-api.com)** — free, no key required, ~1,500 req/month
- Optional premium: **[exchangerate-api.com](https://exchangerate-api.com)** — unlimited with a free/paid key
- **Manual rates**: Enter your own rates with effective dates — these always take priority over API rates
- All fetched rates are stored historically so the app works offline after the first fetch

---

## 📤 Excel Backup & Import

**Export** (Profile → Data Management → Export to Excel):
- Creates a `.xlsx` workbook with 3 sheets: `Investment Records`, `Templates`, `Manual Rates`
- Human-readable — open in Excel, Numbers, or LibreOffice to review your data
- Keep it secure: unlike the `.db` file, the Excel export is **unencrypted plaintext**

**Import** (Profile → Data Management → Import from Excel):
- Reads the same 3-sheet format
- Investment records with dates that already exist are **skipped** — no duplicates
- Templates and manual rates are always added
- Shows a summary count of what was imported

---

## ❓ FAQ

<details>
<summary><strong>What happens if I forget my password?</strong></summary>

Your data cannot be recovered. The master password is never stored anywhere — by design. Use a password manager (1Password, Bitwarden, etc.) to store it safely.

</details>

<details>
<summary><strong>Can I use this on multiple computers?</strong></summary>

Yes. Copy `auth.dat` and `investments.db` from your app-data folder to the new machine, or use the Excel export/import feature. Your password works on any copy of the files.

**Data location:**
- Windows: `%APPDATA%\VaultTrack\`
- macOS: `~/Library/Application Support/VaultTrack/`

</details>

<details>
<summary><strong>Is my database file safe to back up to cloud storage?</strong></summary>

Yes. `investments.db` contains only AES-256-GCM ciphertext — no plaintext data. It is safe to back up to Dropbox, OneDrive, iCloud, or any cloud storage.

</details>

<details>
<summary><strong>Can someone extract my data from the .exe file?</strong></summary>

No. The binary contains no user data. Even with full decompilation, an attacker still needs your `investments.db` **and** your master password. Without the password, Argon2id + AES-256-GCM cannot be brute-forced with current hardware.

</details>

<details>
<summary><strong>Does the app require internet?</strong></summary>

No. The only optional outbound request is fetching exchange rates (which you can disable, or use manual rates instead). All data is stored locally.

</details>

<details>
<summary><strong>Is this open source?</strong></summary>

The source code is proprietary. The compiled binaries are provided for purchase. The security model is fully documented above so you can audit the design.

</details>

---

## 📬 Support

Found a bug or have a question? Open an issue on this repository or email: **[your-email@domain.com]**

---

<div align="center">

**VaultTrack** · Privacy-first investment tracking · Your data stays on your device

*Built with Go + Wails + React*

</div>
