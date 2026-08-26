### ☕ Support the Project

If this practical guide has saved your host from compromise, helped you configure your security baseline, or saved you hours of debugging AppArmor and Firejail profiles, you can support the author and further development of this open-source initiative.

> ⚠️  **OPSEC Warning:** Double-check the addresses before sending any funds.

| Coin | Address |
| :--- | :--- |
| <img src="https://raw.githubusercontent.com/spothq/cryptocurrency-icons/master/128/color/xmr.png" width="20" align="center"> **Monero (XMR)** | `41iZ3BCmeDHJMqoWKYqkmWBM9WNFgMmBvhgt9iYRV6DZQHD5sjc5z2ubjMtdmie7vH3KatF8Qyg1bRsbtEJ5aAYHCZYQCwF` |
| <img src="https://raw.githubusercontent.com/spothq/cryptocurrency-icons/master/128/color/btc.png" width="20" align="center"> **Bitcoin (BTC)** | `bc1q02qe2dujga6dw7d8m0m9s4ntngjq8ynrydxcwk` | 
| <img src="https://raw.githubusercontent.com/spothq/cryptocurrency-icons/master/128/color/sol.png" width="20" align="center"> **Solana (SOL)** | `H974LELMFSLw8f2M9hACc1vDxXRfHgQcBoL1Ef4AuYRw` |
| <img src="https://raw.githubusercontent.com/spothq/cryptocurrency-icons/master/128/color/xrp.png" width="20" align="center"> **Ripple (XRP)** | `rULyw4LQXiVV6ecciJPndq7SHHi2hc2tHv` |
| <img src="https://raw.githubusercontent.com/spothq/cryptocurrency-icons/master/128/color/usdt.png" width="20" align="center"> **USDT (TRC-20)** | `TKzQieJ7RjGeRHU8bi6wiuFruP9uYpuexL` |

# 🛡️ Advanced OS Hardening: Security, Privacy & Anonymity Guide

An enterprise-grade, comprehensive guide dedicated to host-level hardening, operational security (OpSec), and digital self-defense. This project is localized into 17 languages to empower journalists, human rights defenders, and infosec professionals globally.

---

### 🌐 Select Your Language

| Language | Code | Quick Access |
| :--- | :---: | :--- |
| **العربية (Arabic)** | `AR` | [📖 اقرأ باللغة العربية](ar/README.md) \| [📘 كِتَاب](ar/security-baseline-ar.md) |
| **বাংলা (Bengali)** | `BN` | [📖 বাংলায় গাইড পড়ুন](./bn/README.md) \| [📘 বই](./bn/security-baseline-bn.md) |
| **中文 (Chinese)** | `ZH` | [📖 閱讀中文版](./zh/README.md) \| [📘 書籍](./zh/security-baseline-zh.md) |
| **Deutsch** | `DE` | [📖 Auf Deutsch lesen](./de/README.md) \| [📘 Buch](./de/security-baseline-de.md) |
| **Eesti** | `ET` | [📖 Loe juhendit eesti keeles](./et/README.md) \| [📘 Raamat](./et/security-baseline-et.md) |
| **English** | `EN` | [📖 Read Guide in English](./en/README.md) \| [📘 Book](./en/security-baseline-en.md) |
| **Español** | `ES` | [📖 Leer en Español](./es/README.md) \| [📘 Libro](./es/security-baseline-es.md) |
| **Français** | `FR` | [📖 Lire en Français](./fr/README.md) \| [📘 Livre](./fr/security-baseline-fr.md) |
| **हिन्दी (Hindi)** | `HI` | [📖 हिंदी में पढ़ें](./hi/README.md) \| [📘 किताब](./hi/security-baseline-hi.md) |
| **Bahasa Indonesia (Indonesian)** | `ID` | [📖 Baca Panduan Indonesia](./id/README.md) \| [📘 Buku](./id/security-baseline-id.md) |
| **日本語 (Japanese)** | `JA` | [📖 日本語でガイドを読む](./ja/README.md) \| [📘 本](./ja/security-baseline-ja.md) |
| **한국어 (Korean)** | `KO` | [📖 한국어로 읽기](./ko/README.md) \| [📘 책](./ko/security-baseline-ko.md) |
| **فارسی (Persian)** | `FA` | [📖 به زبان فارسی بخوانید](fa/README.md) \| [📘 کتاب](fa/security-baseline-fa.md) |
| **Português (Brasil)** | `PT-BR` | [📖 Ler em Português](./pt-br/README.md) \| [📘 Livro](./pt-br/security-baseline-pt-br.md) |
| **Русский** | `RU` | [📖 Читать руководство на русском](./ru/README.md) \| [📘 Книга](./ru/security-baseline-ru.md) |
| **Türkçe (Turkish)** | `TR` | [📖 Kılavuzu Türkçe olarak okuyun](./tr/README.md) \| [📘 Kitap](./tr/security-baseline-tr.md) |
| **اردو (Urdu)** | `UR` | [📖 اردو میں گائیڈ پڑھیں](ur/README.md) \| [📘 کتاب](ur/security-baseline-ur.md) |

---

## 📌 Project Overview

This guide provides step-by-step instructions to transform a standard Linux distribution into a resilient, high-security workstation capable of mitigating advanced physical, supply-chain, and network-level threats. It focuses strictly on open-source solutions, host-level isolation, compliance verification, and radical reduction of the OS attack surface.

### Key Security Vectors Covered:

* **Hardware & Boot Hardening:** Implementing strict bootloader password protection to mitigate *Evil Maid* attacks, enforcing pre-boot security standards, and establishing secure physical configuration lines.

* **DMA & Memory Protection:** Kernel-level IOMMU programming (`iommu.passthrough=0`) to block malicious Direct Memory Access via Thunderbolt/USB4/PCIe interfaces, combined with low-level kernel tuning to eliminate memory data remanence.

* **Telemetry & Component Purging:** Sanitizing the host completely via automated Bash scripting—purging built-in Canonical telemetry, completely disabling the Snapd ecosystem, and removing vulnerable print/discovery services (Avahi/CUPS).

* **System Integrity & Security Auditing:** Deploying a cryptographic baseline for system files via AIDE (File Integrity Monitoring) and validating the overall defensive posture using automated compliance stress-tests via Lynis.

* **Sandboxing & Mandatory Access Control (MAC):** Enforcing granular application containment by deploying strict AppArmor security policies and isolation chambers using the Firejail sandbox framework.

* **Network Perimeter Isolation:** Engineering bulletproof MAC address spoofing, disabling the IPv6 stack, and building an uncompromising UFW firewall architecture with a strict Kill Switch to completely eliminate traffic leaks outside the virtual boundary of the tun0 VPN interface.

* **Browser Hardening:** Extreme browser core modification via `about:config` and deployment of specialized `user.js` files to neutralize WebRTC leaks, browser fingerprinting, and advanced cross-site tracking.

* **Hardware Token Integration:** Elevating physical access controls to the hardware level by binding display managers, interactive shells, and local KeePassXC credential vaults directly to YubiKey 5 cryptographic tokens.

* **Secure Virtualization & Crypto-Asset Protection:** Designing secure workflows for isolated guest operating systems, advanced anti-forensic optimization of VDI virtual containers (zero-filling and compression), and sandboxing desktop interfaces for hardware wallets like Ledger Live.

* **Data Sanitization & Anti-Forensics:** Irreversible localized data destruction using low-level `shred`/`wipe` routines and systematic metadata extraction/scrubbing via the MAT2 toolkit to fortify operational security (OPSEC).

---

> [!NOTE]
> Contributions are welcome! If you want to improve a translation, update technical content, or report a bug, please open an **Issue** or submit a **Pull Request**. Let's make the digital world safer together.
