<div align="center">

# Security Baseline: A Practical Guide to Ubuntu Desktop Security

## Engineering Hardening and Operational Hygiene for Ubuntu Desktop 24.04/26.04 LTS

### Written and published by EugeXo

</div>

---

<p align="center">
  <img src="../_assets/covers/en/cover_en.png" alt="Project Banner" width="500">
</p>

---

## Table of Contents and Brief Annotations

* [Acknowledgments](#acknowledgments)
* [Securing the Format (OPSEC Disclaimer)](#securing-the-format-opsec-disclaimer)
* [From the Author: Why and For Whom Was This Book Written?](#from-the-author-why-and-for-whom-was-this-book-written)
  * [Core Philosophy:](#core-philosophy)
* [Baseline Protection: 12 Rules of Operational Hygiene](#baseline-protection-12-rules-of-operational-hygiene)
* [Understanding Anonymity, Privacy, and Security](#understanding-anonymity-privacy-and-security)
* [Installing Ubuntu 24.04/26.04 LTS](#installing-ubuntu-24042604-lts)
  * [Introduction:](#introduction)
  * [Hardware Preparation Protocol:](#hardware-preparation-protocol)
  * [Selecting the Distribution:](#selecting-the-distribution)
  * [Step-by-Step Installer Walkthrough:](#step-by-step-installer-walkthrough)
* [First Boot](#first-boot)
* [System Configuration](#system-configuration)
* [Getting Started with the Console](#getting-started-with-the-console)
  * [Initial Setup:](#initial-setup)
  * [Disabling Automounting and Optional Tweaks:](#disabling-automounting-and-optional-tweaks)
  * [Managing Console Shell History:](#managing-console-shell-history)
  * [Configuring a Secure sudo Session Timeout:](#configuring-a-secure-sudo-session-timeout)
  * [Creating the Checks Passed Verification File:](#creating-the-checks-passed-verification-file)
* [Network and VPN Configuration](#network-and-vpn-configuration)
  * [For Ethernet (Wired Connection):](#for-ethernet-wired-connection)
  * [For Wi-Fi (Wireless Connection):](#for-wi-fi-wireless-connection)
  * [NetworkManager Hardening: Suppressing Local mDNS, LLMNR, Hostname Leaks, and Securing DNS:](#networkmanager-hardening-suppressing-local-mdns-llmnr-hostname-leaks-and-securing-dns)
  * [Setting Up a VPN Connection:](#setting-up-a-vpn-connection)
  * [Purging Compromising Bluetooth Components:](#purging-compromising-bluetooth-components)
* [Security Configuration and GRUB Bootloader Hardening](#security-configuration-and-grub-bootloader-hardening)
  * [Setting a Password to Protect GRUB:](#setting-a-password-to-protect-grub)
  * [Software IOMMU Hardening: Protecting RAM Against Kernel-Level DMA Attacks:](#software-iommu-hardening-protecting-ram-against-kernel-level-dma-attacks)
* [Configuring the UFW Firewall With and Without a Kill Switch](#configuring-the-ufw-firewall-with-and-without-a-kill-switch)
  * [Setting Up the Firewall with a Kill Switch:](#setting-up-the-firewall-with-a-kill-switch)
  * [Important Addition on Managing Rule Priority:](#important-addition-on-managing-rule-priority)
  * [Alternative Configuration Setup (Without VPN / For Guest OS):](#alternative-configuration-setup-without-vpn--for-guest-os)
* [Kernel Tuning, Access Control, and Purging Unnecessary System Services](#kernel-tuning-access-control-and-purging-unnecessary-system-services)
  * [Protecting the Network Stack and Kernel Memory Subsystem:](#protecting-the-network-stack-and-kernel-memory-subsystem)
  * [Low-Level sysctl Hardening: Mitigating TCP Timestamp Fingerprinting:](#low-level-sysctl-hardening-mitigating-tcp-timestamp-fingerprinting)
  * [Blocking Rare Network Protocols and Legacy Filesystems:](#blocking-rare-network-protocols-and-legacy-filesystems)
  * [Filesystem Access Control Hardening:](#filesystem-access-control-hardening)
  * [Securely Mounting Shared Memory:](#securely-mounting-shared-memory)
  * [Configuring Wi-Fi to Default Off on Boot:](#configuring-wi-fi-to-default-off-on-boot)
  * [Cutting Off Video Streams and Audio Recording:](#cutting-off-video-streams-and-audio-recording)
  * [Removing Printing Services and Local Network Discovery Services:](#removing-printing-services-and-local-network-discovery-services)
  * [Masking Geolocation and Timezone:](#masking-geolocation-and-timezone)
* [Configuring Repositories and System Updates](#configuring-repositories-and-system-updates)
  * [Updating the System:](#updating-the-system)
  * [Deploying the NVIDIA Graphics Stack in Isolated Mode:](#deploying-the-nvidia-graphics-stack-in-isolated-mode)
* [Terminal Environments in Ubuntu:](#terminal-environments-in-ubuntu)
  * [Replacing Gnome Terminal and Ptyxis with Ghostty](#replacing-gnome-terminal-and-ptyxis-with-ghostty)
  * [Optional! Ubuntu 26.04 — Restoring Gnome Terminal and Removing Ptyxis:](#optional-ubuntu-2604--restoring-gnome-terminal-and-removing-ptyxis)
* [Removing and Blocking Snap and Telemetry](#removing-and-blocking-snap-and-telemetry)
  * [Purging Snap:](#purging-snap)
  * [Ripping Out Canonical Telemetry:](#ripping-out-canonical-telemetry)
  * [Purging the Background Firmware Tracker fwupd:](#purging-the-background-firmware-tracker-fwupd)
* [Installing Security Utilities: libpam-tmpdir, debsums, and the Btop System Monitor](#installing-security-utilities-libpam-tmpdir-debsums-and-the-btop-system-monitor)
  * [The libpam-tmpdir Security Utility](#the-libpam-tmpdir-security-utility)
  * [The debsums Utility](#the-debsums-utility)
  * [Btop: A Streamlined Resource Monitor](#btop-a-streamlined-resource-monitor)
  * [Monitoring Network Ports and Active Connections](#monitoring-network-ports-and-active-connections)
* [Creating Golden Restore Points: Deploying and Configuring Timeshift](#creating-golden-restore-points-deploying-and-configuring-timeshift)
  * [Introduction:](#introduction-1)
  * [Timeshift Mechanics in an Encrypted Environment (LUKS + GRUB):](#timeshift-mechanics-in-an-encrypted-environment-luks--grub)
  * [Securely Installing Timeshift:](#securely-installing-timeshift)
  * [Initial Configuration and Creating Snapshot #1 (Sterile Baseline):](#initial-configuration-and-creating-snapshot-1-sterile-baseline)
  * [Ongoing Control Strategy: Creating Snapshot #2 (Pre-Operational):](#ongoing-control-strategy-creating-snapshot-2-pre-operational)
  * [Emergency Rollback Protocol (System Compromised or Broken):](#emergency-rollback-protocol-system-compromised-or-broken)
* [Installing a Clean .deb Release of Firefox and Removing the Snap Stub](#installing-a-clean-deb-release-of-firefox-and-removing-the-snap-stub)
* [Installing and Hardening Privacy Settings in Mozilla Firefox](#installing-and-hardening-privacy-settings-in-mozilla-firefox)
  * [Preparing the System for Tuning:](#preparing-the-system-for-tuning)
  * [Initial GUI Privacy Configuration (Mandatory for Everyone):](#initial-gui-privacy-configuration-mandatory-for-everyone)
  * [Configuring Private DNS Providers (DNS over HTTPS):](#configuring-private-dns-providers-dns-over-https)
  * [Hardening Automation: Creating the user.js Configuration File:](#hardening-automation-creating-the-userjs-configuration-file)
  * [Deploying Ultimate Security Extensions](#deploying-ultimate-security-extensions)
* [Installing and Configuring the Portmaster Interactive Network Firewall](#installing-and-configuring-the-portmaster-interactive-network-firewall)
  * [Introduction:](#introduction-2)
  * [Preparation, Initial Kernel Initialization, and Upgrading:](#preparation-initial-kernel-initialization-and-upgrading)
* [Guaranteed Data Destruction and Sterilizing Your Digital Footprint](#guaranteed-data-destruction-and-sterilizing-your-digital-footprint)
  * [Introduction:](#introduction-3)
  * [Anatomy of a Digital Footprint: Why Deleting Files Is Useless Without Metadata Sanitization](#anatomy-of-a-digital-footprint-why-deleting-files-is-useless-without-metadata-sanitization)
  * [Installing and Sanitizing Metadata with MAT2:](#installing-and-sanitizing-metadata-with-mat2)
  * [Secure and Irreversible File and Directory Destruction:](#secure-and-irreversible-file-and-directory-destruction)
  * [Operational Parameters for the shred Utility:](#operational-parameters-for-the-shred-utility)
  * [Global Wiping of Unallocated Disk Space:](#global-wiping-of-unallocated-disk-space)
* [Steganography, Obfuscation, and Anti-Forensics Trace Hiding in Ubuntu](#steganography-obfuscation-and-anti-forensics-trace-hiding-in-ubuntu)
  * [Introduction:](#introduction-4)
  * [Linux Steganography: Concealing Files Within Media Content:](#linux-steganography-concealing-files-within-media-content)
  * [The steghide Command-Line Utility:](#the-steghide-command-line-utility)
  * [Stealth Concealment via the Advanced StegoForge Tool:](#stealth-concealment-via-the-advanced-stegoforge-tool)
  * [Archive Concatenation (Quick Hack Without Third-Party Software):](#archive-concatenation-quick-hack-without-third-party-software)
  * [Text Obfuscation: Bypassing Automated Inspection Systems (DPI):](#text-obfuscation-bypassing-automated-inspection-systems-dpi)
  * [Analyzing Hidden Threats: File Extension Spoofing (BiDi Attacks):](#analyzing-hidden-threats-file-extension-spoofing-bidi-attacks)
* [Installing and Configuring the VeraCrypt Cryptographic Suite](#installing-and-configuring-the-veracrypt-cryptographic-suite)
  * [Introduction to VeraCrypt and Installation:](#introduction-to-veracrypt-and-installation)
  * [Deep Security Tuning: RAM Key Protection (Paranoia Mode):](#deep-security-tuning-ram-key-protection-paranoia-mode)
  * [A Fundamental Security Tool: Creating Hidden Volumes:](#a-fundamental-security-tool-creating-hidden-volumes)
  * [Ultimate Hardening: Configuring PIM and Hardware Keyfiles:](#ultimate-hardening-configuring-pim-and-hardware-keyfiles)
  * [Real-World Threat Modeling: Why Paranoia Must Be Systemic:](#real-world-threat-modeling-why-paranoia-must-be-systemic)
* [Utilizing Yubico Security Keys](#utilizing-yubico-security-keys)
  * [Introduction:](#introduction-5)
  * [Installation:](#installation)
  * [Implementing a Hardware Kill Switch via Kernel udev Rules](#implementing-a-hardware-kill-switch-via-kernel-udev-rules)
* [Installing and Configuring USBGuard](#installing-and-configuring-usbguard)
  * [Introduction:](#introduction-6)
  * [Installation and Setup:](#installation-and-setup)
* [Installing the KeePassXC Local Password Manager](#installing-the-keepassxc-local-password-manager)
  * [Introduction:](#introduction-7)
  * [Vault Protection Scenarios:](#vault-protection-scenarios)
  * [Installing the Software Suite:](#installing-the-software-suite)
  * [Creating and Hardware-Securing the Database:](#creating-and-hardware-securing-the-database)
  * [Deep Hardening of Internal Security Settings:](#deep-hardening-of-internal-security-settings)
  * [Secure Data Entry via Protected Clipboard:](#secure-data-entry-via-protected-clipboard)
* [Installing and Running the Wireshark Network Analyzer](#installing-and-running-the-wireshark-network-analyzer)
  * [Introduction:](#introduction-8)
  * [Installing and Launching Wireshark:](#installing-and-launching-wireshark)
  * [Critical Security Concept: Packet Capture Subsystem Security:](#critical-security-concept-packet-capture-subsystem-security)
  * [Stealth Traffic Capture (Headless Console Mode):](#stealth-traffic-capture-headless-console-mode)
  * [Practical Wireshark Field Guide:](#practical-wireshark-field-guide)
* [Installing and Managing the AppArmor Security System](#installing-and-managing-the-apparmor-security-system)
  * [Introduction:](#introduction-9)
  * [A New Security Paradigm: Kernel Automation:](#a-new-security-paradigm-kernel-automation)
  * [Practical Hardening of the AppArmor Subsystem:](#practical-hardening-of-the-apparmor-subsystem)
* [Installing and Configuring the Firejail Isolated Sandbox](#installing-and-configuring-the-firejail-isolated-sandbox)
  * [Introduction:](#introduction-10)
  * [Installing Firejail and Preparing the Sandbox:](#installing-firejail-and-preparing-the-sandbox)
  * [Core Firejail Filtering Options (Reference):](#core-firejail-filtering-options-reference)
  * [Creating a Dedicated Hardened Firefox Profile:](#creating-a-dedicated-hardened-firefox-profile)
  * [Airtight PDF Vault: Safely Opening Files in an Isolated Offline Mode:](#airtight-pdf-vault-safely-opening-files-in-an-isolated-offline-mode)
  * [Sandboxing Image Viewer for Secure Media Inspection:](#sandboxing-image-viewer-for-secure-media-inspection)
  * [KeePassXC Sandboxing Scenario:](#keepassxc-sandboxing-scenario)
  * [Installing and Sandboxing the LibreOffice Suite:](#installing-and-sandboxing-the-libreoffice-suite)
  * [Installing and Sandboxing GNU Image Manipulation Program (GIMP):](#installing-and-sandboxing-gnu-image-manipulation-program-gimp)
  * [Installing and Sandboxing VS Codium (Development IDE):](#installing-and-sandboxing-vs-codium-development-ide)
  * [Installing and Sandboxing LM Studio Bionic Local AI:](#installing-and-sandboxing-lm-studio-bionic-local-ai)
  * [Securing Communications: Mandatory Isolation of Messengers and Crypto Infrastructure (Author's OPSEC Setup):](#securing-communications-mandatory-isolation-of-messengers-and-crypto-infrastructure-authors-opsec-setup)
  * [Installing and Sandboxing Telegram Desktop:](#installing-and-sandboxing-telegram-desktop)
  * [Host Cryptographic Foundation: Generating and OPSEC-Protecting GnuPG Keys:](#host-cryptographic-foundation-generating-and-opsec-protecting-gnupg-keys)
  * [Installing and Sandboxing the Psi+ Jabber Client:](#installing-and-sandboxing-the-psi-jabber-client)
  * [Installing and Sandboxing Thunderbird (Encrypted Email Workflow):](#installing-and-sandboxing-thunderbird-encrypted-email-workflow)
  * [Automating the Defensive Perimeter (Firecfg Utility) and Customizing System Icons:](#automating-the-defensive-perimeter-firecfg-utility-and-customizing-system-icons)
  * [Advanced Paranoia Mode: Sandboxing with Session Persistence via Overlay:](#advanced-paranoia-mode-sandboxing-with-session-persistence-via-overlay)
* [Installing Rkhunter and Hunting Rootkits](#installing-rkhunter-and-hunting-rootkits)
* [Installing and Configuring the ClamAV Antivirus Scanner](#installing-and-configuring-the-clamav-antivirus-scanner)
  * [Introduction:](#introduction-11)
  * [Installing ClamAV:](#installing-clamav)
  * [Updating Signature Databases and Bypassing Network Blocks:](#updating-signature-databases-and-bypassing-network-blocks)
  * [Structuring System Scans:](#structuring-system-scans)
  * [Multithreaded Scanning (Hardening):](#multithreaded-scanning-hardening)
* [Installing and Configuring the VirtualBox Virtualization Environment](#installing-and-configuring-the-virtualbox-virtualization-environment)
* [Shrinking and Optimizing VDI Virtual Disks](#shrinking-and-optimizing-vdi-virtual-disks)
  * [Introduction:](#introduction-12)
  * [Sanitizing a Windows Guest Virtual Machine:](#sanitizing-a-windows-guest-virtual-machine)
  * [Sanitizing a Linux Guest Virtual Machine (Ubuntu/Kali Linux):](#sanitizing-a-linux-guest-virtual-machine-ubuntukali-linux)
  * [Final Virtual Disk Compaction on the Host Machine:](#final-virtual-disk-compaction-on-the-host-machine)
* [Installing and Configuring the Docker Containerization Platform](#installing-and-configuring-the-docker-containerization-platform)
  * [Introduction:](#introduction-13)
  * [What Is the Hidden Danger of Default Docker?](#what-is-the-hidden-danger-of-default-docker)
  * [Deploying Docker in Rootless Mode:](#deploying-docker-in-rootless-mode)
  * [Taming the Network and Binding Docker to UFW:](#taming-the-network-and-binding-docker-to-ufw)
  * [Experimental Proof of Security (Verifying Non-Root Execution):](#experimental-proof-of-security-verifying-non-root-execution)
* [Installing and Configuring the AIDE File Integrity Monitoring System](#installing-and-configuring-the-aide-file-integrity-monitoring-system)
  * [Introduction:](#introduction-14)
  * [Installing and Configuring AIDE:](#installing-and-configuring-aide)
  * [Executing a Penetration Test (Validating Defense Mechanisms):](#executing-a-penetration-test-validating-defense-mechanisms)
* [Automated System Security Auditing with Lynis](#automated-system-security-auditing-with-lynis)
* [Configuring Ubuntu/Xubuntu/Lubuntu Guest Systems in VirtualBox](#configuring-ubuntuxubuntulubuntu-guest-systems-in-virtualbox)
  * [Installing Guest Additions:](#installing-guest-additions)
  * [Installing Mozilla Firefox:](#installing-mozilla-firefox)
  * [Configuring Shared Folders in VirtualBox:](#configuring-shared-folders-in-virtualbox)
  * [Installing Ledger Live in VirtualBox with Ubuntu/Xubuntu/Lubuntu](#installing-ledger-live-in-virtualbox-with-ubuntuxubuntulubuntu)
  * [Running Ledger Live on the Primary Ubuntu Host OS](#running-ledger-live-in-a-sandbox-on-the-main-ubuntu-host-system)
* [About the Author and Legal Information](#about-the-author-and-legal-information)
  * [Contact Information and Community Resources:](#contact-information-and-community-resources)

<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Acknowledgments

Keeping it simple and straight to the point, I would like to express my deepest gratitude to the people who pushed me to write this book and supported me every step of the way.

My thanks go to the regular folks in the cybersecurity division of the police force in our small yet technologically advanced Estonia, who provided the initial spark for this book.

I also extend special thanks to the InfoSec specialists from the US Secret Service Miami Field Office, who made significant practical contributions by validating several chapters. As it turned out, the security controls and methodologies outlined here perform exceptionally well in real-world field conditions.

Naturally, immense gratitude goes to my family for their phenomenal patience and moral support. Especially to my mother, who approached my work with complete understanding and took on a massive share of everyday routines, freeing up my time for research.

**I want to extend a personal note of gratitude to my friend from the UK. We were in close touch back when I was in Miami, but unfortunately, lost contact over time. I sincerely hope our paths cross again. Mate, if you or your InfoSec son happen to read these lines, please reach out — my contact details are listed at the end of the book. I reckon you know *who is who!* ;)**

Indescribable appreciation goes to my virtual assistant — **Gemini by Google**. Throughout the creation of this book, it remained an unfailing digital partner, providing invaluable assistance in structuring and translating this hardcore material.

Thanks to the sharp and versatile assistant **ChatGPT by OpenAI** for helping brainstorm technical architectures, sanity-check configs, meticulously edit specific text passages, and dial in precise technical wording.

And naturally, first and foremost, my gratitude goes to the engineers and developers at Google and OpenAI for their world-class engineering!

I could go on, but everyone involved knows who they are. I am thrilled to finally deploy this book into the wild. Guys, I truly love, value, and respect you all!

<br>

## Securing the Format (OPSEC Disclaimer)

For reasons of information security and operational common sense, all content in this manual is natively delivered as plain text using Markdown markup. The original plan to publish this book as a PDF was deliberately dropped. The PDF specification carries a massive, bloated architecture and suffers from a history of recurring security compromises. Hardening a host must begin with securely reading the instructions on how to harden it.

A plain text file represents pure data completely devoid of executable code, whereas the PDF format natively supports embedded JavaScript execution, dynamic payload elements, interactive forms, and complex custom fonts that demand deep, high-privilege system parsing. Critical Remote Code Execution (RCE) vulnerabilities in Linux PDF renderers (such as stock Evince or underlying Poppler libraries) are a proven historical fact. The Plain Text format contains no execution primitives, drastically reducing your attack surface while reading this material. This guarantees safe consumption in any operational environment.

For this exact reason, all graphical assets and diagrams have been segregated from the core text into a dedicated directory. Visual assets are structured across subdirectories, preventing automatic memory rendering while reading through the text.

> [!NOTE]
> Markdown serves as the single source of truth for this book. All secondary distributions (HTML, EPUB, etc.) are built directly from audited text sources.
> 
> Readers can consume this project in one of three ways:
> 
> * Read raw Markdown source files directly.
> * Deploy pre-compiled HTML/EPUB builds (to be implemented in future releases).
> * Compile the book directly from source, allowing custom styling, structure adjustments, custom typography, or selective chapter builds.
> 
> This architecture ensures total text transparency, effortless change auditing, and zero reliance on proprietary reading tools.

<br>

## From the Author: Why and For Whom Was This Book Written?

The modern digital landscape is becoming increasingly hostile and complex: cyber threats are escalating, telemetry and data harvesting are surging, and users are routinely forced to take the defense of their privacy and security into their own hands.

This book was authored as a hands-on field manual for building a fully audited, controlled Linux workstation where security is engineered not as a random collection of isolated apps, but as a unified system of interconnected controls. My goal is to demonstrate how to leverage accessible Linux tools to engineer an operational environment with a clear threat model: complete application isolation, strict network activity control, robust data protection, and deliberate management of your digital footprint.

**The core goal of this book is to build a workstation where every single action operates within a strictly controlled security perimeter.**

This material is provided for educational purposes and is designed for power users, Linux enthusiasts, and InfoSec professionals seeking practical defense mechanics. This guide is not a "Linux 101" tutorial and assumes a foundational grasp of the terminal, the filesystem layout, and core OS concepts. That said, any disciplined, highly motivated reader will be able to follow along and master these techniques step bystep.

All methodologies detailed here must be deployed strictly for lawful purposes: protecting your own data, elevating host defenses, and mastering the fundamentals of information security.

Deliberate data protection and responsible technology usage make the digital landscape safer for everyone.

#### Core Philosophy:

The purpose of this book is not to build a bloated encyclopedia covering every single utility, but rather to demonstrate their exact role within a unified defensive posture. Consequently, the internal mechanics and feature sets of individual components are analyzed only to the extent required to understand their core operational principles and enforce secure deployment.

Advanced feature sets, exhaustive command syntax, and specialized edge-case scenarios fall outside the scope of this manual and can be explored independently via official upstream documentation.

<br>

## Baseline Protection: 12 Rules of Operational Hygiene

*Hello World, comrade!*

Before we dive into the hardcore technical hardening of our system, let's lock down the foundation. Below are 12 ironclad rules of operational hygiene that we need to learn by heart and strictly observe. Without understanding them, even the most advanced security tools will eventually prove completely useless:

1. **Purge wireless peripherals from our secure perimeter whenever possible:** this includes Bluetooth and Wireless devices (headsets, headphones, wireless keyboards, and mice). Any wireless interface drastically inflates our attack surface and forces implicit trust in protocol stacks, proprietary firmware, and vendor implementation choices.
2. **Enforce mandatory full-disk encryption** on the system storage drive during OS installation. We make the cryptographic passphrase at least 24 random characters long (including special characters)!
3. **Perform scheduled periodic changes of our OS authentication password.** We make the user password unique and sufficiently long (at least 16 characters recommended). When using hardware security keys, the password is not replaced, but rather supplemented with an additional security factor.
4. **Activate password protection for the GRUB bootloader** to completely eliminate unauthorized access to kernel parameters and configuration editing during physical access to the PC.
5. **Implement a hardware security key** (YubiKey or legitimate equivalents) as a mandatory second factor of authentication (2FA) for logging into the system and approving superuser commands.
6. **Clean the system of any unnecessary software.** This especially applies to closed-source proprietary software. We remember the fundamental rule: the fewer third-party services, daemons, and applications in our system, the smaller our potential attack surface and total critical vulnerabilities.
7. **Keep the operating system perpetually updated.** We take it as an ironclad rule to regularly check for and install system security updates using console tools.
8. **Continuously monitor network and interface states.** We pay close attention to which remote resources background connections are establishing with and where our network traffic is going.
9. **Regularly conduct internal host audits.** We periodically (preferably 2–3 times a week) inspect the system for rootkits, malware, and check system file integrity.
10. **Never run suspicious executable files on the main system.** For safe testing, we always use an isolated `Firejail` sandbox or virtual machines.
11. **Enforce strict protection against dangerous DMA (Direct Memory Access) attacks and password-protect BIOS/UEFI:** In BIOS/UEFI settings, we forcibly set Thunderbolt/USB4 ports to maximum authorization mode (*Kernel DMA Protection*) to reduce the risk of DMA attacks via external peripherals. We set a strong BIOS/UEFI password. Additionally, we completely disable *Sleep Mode*, as encryption keys remain in RAM in plaintext during this state.
12. **Forcibly lock the session whenever leaving the workstation, even for a moment, and shut down the computer completely when away long-term.**

> [!NOTE]
> The weakest element of any security system often remains not the software, but user actions.
>
> In professional circles, there is a humorous saying: "the primary vulnerability resides between the chair and the keyboard."
>
> That is precisely why technical hardening must be paired with operational discipline: verifying files before opening them, scrubbing metadata prior to publication, monitoring network activity, and maintaining a constant awareness of our threat model.

<br>

## Understanding Anonymity, Privacy, and Security

In casual conversation, these terms are often mashed together, even though they address fundamentally different vectors.

**Anonymity** answers the question: "Can my actions be linked to my real-world identity?"
In an ideal environment, an adversary can monitor the activity itself, but has zero capability to tie it to a specific physical individual.

**Privacy** answers the question: "Do I control what information is harvested about me and who gains access to it?" 
The adversary acknowledges that the individual exists, but that individual maintains total command over what data leaks outward.

**Security** answers the question: "Can I defend my host system, environment, and physical device against unauthorized access?"
The operator maintains continuous combat readiness within their digital perimeter. The adversary might be standing right at the gates, yet lack the exploitation primitives to compromise the host and extract data.

An encrypted laptop backed by a hardened passphrase represents elevated **security**. However, if the operator willingly publishes personal identifiers online, their **privacy** remains zero. Deploying anonymization routing tools can obscure your identity, but does nothing to protect your OS against malicious payloads. A heavily secured workstation can be completely non-anonymous, while an anonymous routing link can be fundamentally insecure.

**The goal of this book is not to sell the illusion of absolute defense or complete online invisibility. The goal is to demonstrate how to engineer a system where the operator clearly understands which threat vectors are mitigated and which operational constraints remain.**

<br>

## Installing Ubuntu 24.04/26.04 LTS

#### Introduction:

In this chapter, we deploy our Linux operating system built around strict security controls. This section also covers installation onto external USB and Thunderbolt storage drives.

Before initializing the installation process, we must take several critical risk vectors into account. One of the most prevalent operational pitfalls is target drive misconfiguration during bootloader installation.

In Linux, GRUB (GRand Unified Bootloader) handles system initialization. During setup, the installer might default to placing GRUB on the wrong physical drive—often writing to the EFI System Partition (ESP) of a secondary storage device instead of our intended target. Consequently, existing host operating systems may fail to boot until bootloader recovery is performed.

To eliminate this failure mode entirely, the most reliable protocol for us is to physically disconnect all internal HDDs and SSDs unrelated to our target OS during the installation process.

On desktop hardware, this requires basic access to internal components and a screwdriver. On laptops, hardware access depends on chassis design and can be significantly more complex.

Apple hardware (particularly modern MacBooks equipped with the T2 security chip or Apple Silicon) is strictly disadvised for our deployment model due to proprietary hardware abstractions, closed boot chain constraints, and Linux kernel incompatibility.

> [!NOTE]
> We have thoroughly validated this manual on **Ubuntu 24.04 LTS Noble Numbat (24.04.4)** and **Ubuntu 26.04 LTS Resolute Raccoon (26.04.0)**.
>
> We conducted testing across **VirtualBox 7.2.x**, **VMware Workstation Pro 26H1**, as well as bare-metal hardware running integrated Intel graphics and discrete NVIDIA GPU accelerators.

#### Hardware Preparation Protocol:

* **On a Desktop PC:** We remove the side chassis panel, disconnect the system entirely from mains power, and unplug all storage drives except the single target drive designated for our Linux installation. If M.2 NVMe drives are present, we will need a precision screwdriver for removal.

* **On a Laptop:** We power down the machine completely, unplug external power adapters, and disconnect the internal battery if possible. After removing the bottom chassis cover, we disconnect or remove all storage drives except our intended target.

If we are deploying to an external USB or Thunderbolt drive, we leave only that target external storage device connected. It will serve as our primary target drive for system installation.

> [!WARNING]
> Prior to initializing OS setup, we access the BIOS/UEFI firmware interface and verify our GPU hardware configuration. On laptops equipped with hybrid graphics architecture, we enforce Hybrid Mode / Optimus. This routes our primary desktop compositor through the CPU's integrated graphics core. Doing so allows us to leverage open-source Linux kernel drivers (such as `i915`, `xe`, or `amdgpu` depending on our silicon) and eliminates immediate reliance on proprietary closed-source blobs.
>
> If supported by our platform, we configure a strong supervisor password for BIOS/UEFI and enable hardware disk locking (ATA/NVMe password protection, if supported by the SSD/HDD). This mitigates unauthorized boot order tampering and hardens our host against physical access attack vectors.
>
> We audit the status of Secure Boot. If our target installation topology fully supports it, we recommend leaving this feature enabled.
>
> **We ensure only the single drive designated for our system installation remains connected to the desktop or laptop.**
>
> We execute the Linux installation **strictly offline** — we unplug the LAN Ethernet cable and do not connect our host to any Wi-Fi wireless networks. All required packages, security updates, and tooling will be deployed post-installation, once initial base hardening is complete.

Why do we perform an offline installation?

An air-gapped offline install drastically reduces our external risk vectors during initial OS deployment:

* Zero active external network sockets exist throughout our setup phase;
* Automatic pulling of third-party dependencies or upstream updates is blocked prior to base hardening;
* Background network daemons and system services spawned during installation are kept to an absolute minimum;
* It provides us with complete deterministic control over the baseline OS image and installed components;
* Potential remote attack vectors are suppressed until host security hardening is fully enforced.

Once initial configuration and security controls are locked down, we can safely bring our network interfaces online inside a strictly controlled perimeter.

#### Selecting the Distribution:

We will execute all configurations on modern releases: **Ubuntu 24.04 LTS Noble Numbat** and **Ubuntu 26.04 LTS Resolute Raccoon**. They feature a smooth learning curve, remain lightweight, and operate reliably even on hardware constrained to 2 GB of RAM (especially when opting for minimal derivatives such as Xubuntu or Lubuntu). Furthermore, they benefit from massive backing by the global open-source ecosystem and, most importantly, ship with a robust baseline security posture straight out of the box.

We strongly advise running the installation process in English. Should unexpected errors or runtime exceptions occur, querying technical documentation, stack traces, and upstream forums becomes significantly more efficient. That said, this is an operational choice—the final localization decision rests with you. Throughout this manual, we deploy using English localization—specifically English (US).

#### Step-by-Step Installer Walkthrough:

**1.** Following language selection, we proceed to the keyboard layout configuration menu—**"Select your keyboard"**—and select **English (US)** or our preferred mapping.

**2.** In the network connectivity screen, we strictly select **"Do not connect to the internet"**.

**3.** Next, we choose **"Interactive Installation"** and select **"Default selection"**—this ensures a minimal software footprint is installed on the underlying filesystem. Should we require additional software suites like office packages later on, we will pull them directly from official software repositories. Minimizing our initial package footprint directly shrinks our exposure and mitigates potential attack vectors.

**4.** On the subsequent screen, we naturally decline the installation of proprietary third-party software blobs.

**5.** **Ubuntu 24.04:** In the **"Disk Setup"** menu, we click **"Advanced features..."**, select **"Use LVM and encryption"**, confirm our choice by clicking **"OK"**, and press **"Next"**.

**Ubuntu 26.04:** We retain the default selection **"Erase disk and install Ubuntu"** and click **"Next"**.

**6.** **Ubuntu 24.04:** The next screen prompts us for our master disk encryption passphrase. We craft (and carefully store) a robust passphrase at least 24 characters long (longer is better), incorporating the full range of keyboard inputs: uppercase and lowercase Latin characters (A-Z, a-z), numeric digits (0-9), special symbols, and space characters. We click **"Next"**.

**Ubuntu 26.04:** We select **"Encryption with passphrase"**, click **"Next"**, and enter our master disk encryption passphrase on the following screen. We craft (and carefully store) a robust passphrase at least 24 characters long (longer is better), incorporating the full range of keyboard inputs: uppercase and lowercase Latin characters (A-Z, a-z), numeric digits (0-9), special symbols, and space characters. We click **"Next"**.

**7.** Next, the **"Create your account"** provisioning screen appears. In the **"Your name"** field, we input an operational identifier (we choose a neutral string that leaks zero real-world identity markers, e.g., `user`). In the **"Computer name"** field, we define an arbitrary system hostname (e.g., `host-node`), and choose our user account name under **"Pick a username"**. In the **"Choose password"** section, we generate a complex user passphrase at least 16 characters long using uppercase and lowercase Latin characters (A-Z, a-z), digits (0-9), special symbols, and spaces. We ensure **"Require password to login"** is selected, then click **"Next"**.

**8.** The next screen displays a timezone selection map. We select any initial region (we will subsequently standardize our host timezone to UTC), then click **"Next"**.

**9.** On the final review screen, we perform an audit of all target parameters to ensure no configurations were missed, then click **"Install"**.

The installer will now begin provisioning the operating system. This process is fully automated, executes rapidly, and requires zero user intervention. Once deployment finishes, the installer will prompt us to remove the USB installation medium and execute a system reboot. At this point, initial setup is complete, and any disconnected secondary drives can be safely reconnected.

> [!IMPORTANT]
> Ubuntu 24.04/26.04 offers two fundamentally distinct frameworks for protecting data at rest: legacy passphrase-backed encryption and hardware-bound encryption with automated decryption via TPM. Both architectures deploy LUKS as the underlying disk encryption layer; they differ primarily in how the secret key is derived and supplied to unseal the volume.
> 
> We deliberately implement the classic LVM + LUKS architecture backed by a long user passphrase throughout this manual. This directly aligns with our defined threat model, where the device owner must explicitly authenticate to unlock the encrypted volume before host boot continuation.
> 
> This does not imply that TPM-bound FDE is inherently broken or insecure. It targets a different threat model and delivers specific advantages, such as automated platform integrity measurement and defense against specific early-stage boot chain attacks. However, within the scope of this book, automated disk unsealing is strictly ruled out: we mandate explicit user authentication using a long LUKS passphrase.
> 
> Thus, leveraging classic LUKS throughout this book represents a deliberate operational decision under our stated threat model, rather than a claim that TPM-based FDE is fundamentally flawed.
> 
> Our approach—manually crafting a high-entropy passphrase via LVM—remains the gold standard in information security for protecting data at rest against physical access attacks on powered-down hardware. When deploying automated unsealing via TPM, our user passphrase ceases to be the primary defensive boundary. Instead, security relies entirely on the correct execution of trusted platform modules, bootloader integrity, and vendor hardware implementations. Manually keying in a long LUKS passphrase completely eliminates this high-risk attack surface.

**Chapter Assets:** `_assets/images/1_os_install`

<br>

## First Boot

We log in to the host system by providing our disk encryption passphrase followed by our user account password. Moving forward, our user password will be required to authenticate administrative actions via `sudo`. Upon reaching the desktop interface, we are greeted by the initial setup wizard; we click **"Next"**.

In Ubuntu 26.04, the next screen presented is **"Location Services"**. By default, this toggle is set to the disabled position, so we simply click **"Next"**. (Note: Ubuntu 24.04.4 skips this screen entirely).

In Ubuntu 24.04, the installer prompts us to enable an *Ubuntu Pro* subscription—we click **"Skip"** in the top right corner. (Note: Ubuntu 26.04.0 skips this step).

On the **"Help improve Ubuntu"** prompt, we strictly select or maintain the option **"No, don't send system data"** (in Ubuntu 26.04, we ensure the "Share error reports with the Ubuntu team" toggle remains disabled as well). We click **"Next"** until reaching the final window, then complete the wizard by clicking **"Finish"**. At this stage, we suppress the outbound transmission of diagnostic telemetry to Canonical.

> [!NOTE]
> Even though we clicked **"Skip"**, Canonical still leaves active subscription check daemons running in the background. Do not worry—we will manually strip these telemetry components via the terminal in an upcoming section.

**Chapter Assets:** `_assets/images/2_first_boot`

<br>

## System Configuration

By default, the desktop displays a panel on the left known as the **"Dock"**. We click the circular OS icon at the bottom corner of the panel (**"Show Apps"**) and select **"Settings"** (alternatively, we access the settings menu via the top system bar by clicking the status area in the top-right corner and selecting the gear icon).

Inside the System Settings interface, we toggle both **"Bluetooth"** and **"Wi-Fi"** switches to the OFF position. This puts our system into "Airplane Mode" and temporarily disables wireless interfaces until we configure their permanent hardware/kernel-level block.

Next, we customize the **"Dock"** under the **"Ubuntu Desktop"** tab according to our operational preference. For instance, we relocate it to the bottom by setting **"Position on screen"** to **"Bottom"**, and adjust the **"Icon size"**. Disabling **"Panel Mode"** transforms our Dock into a compact, macOS-style launcher bar. Additionally, we strip the panel of any unnecessary default application shortcuts.

We navigate to **"Privacy & Security"**, then enter the **"Diagnostics"** / **"Telemetry"** sub-tab. Under **"Problem Reporting"**, we set the **"Send error reports to Canonical"** parameter strictly to **"Never"**.

We proceed to the adjacent **"File History & Trash"** section. Here, it is critical for us to completely disable **"File History"**. We enable **"Automatically Delete Trash Content"** and **"Automatically Delete Temporary Files"**, configuring their retention period to **"1 day"**.

> [!IMPORTANT]
> Automatic trash and cache purging serves only as basic surface hygiene. To maintain operational security, confidential files, cryptographic material, and log artifacts must always be destroyed manually via the terminal using low-level utilities like `shred` (discussed in detail later). This renders forensic recovery from physical media extremely difficult. Note that file destruction mechanics depend on media architecture: while `shred` is effective on legacy magnetic HDDs, modern SSD/NVMe flash storage requires Full Disk Encryption combined with secure cryptographic key erasure (Crypto-Erase) for absolute data destruction.

In the adjacent **"Location"** tab, we verify that the toggle is set to **"Off"**—there is zero operational justification for the operating system to track our physical coordinates.

Under **"Screen Lock"**, we adjust the **"Blank Screen Delay"** parameter. The default setting is 5 minutes; for elevated security, we reduce this to 1–2 minutes. We ensure **"Automatic Screen Lock"** is toggled ON. Within this same panel, we access **"Automatic Screen Lock Delay"** and set it to **"Screen Turns Off"**, 30 seconds, or a maximum of 1 minute (initiating a screen dimming phase precisely 30 seconds or 1 minute before lock activation). We enable both **"Lock Screen Notifications"** and **"Lock Screen on Suspend"**.

Next, in the **"Connectivity"** menu, we disable **"Connectivity Checking"**. This eliminates automated background network probes performed by the OS.

Under **"Thunderbolt"**: if we do not utilize external Thunderbolt expansion hardware, we disable the interface entirely.

In Ubuntu 26.04, a new **"Cameras"** control toggle has been introduced under **"Privacy & Security"**—we enter this menu and switch the camera access toggle to OFF.

We navigate to **"System"** -> **"Date & Time"** to configure temporal settings. If we are hardening this host for high-anonymity workflows over encrypted VPN tunnels or the Tor network, we disable **"Automatic Date & Time"**. In elevated privacy models, automated network time synchronization should be disabled and timezones set manually. Throughout this manual, UTC will serve as our standardized temporal baseline.

In the **"Keyboard"** tab, we append any required secondary input layouts. Other visual or cosmetic preferences in the system menu can be adjusted based on our personal workflow requirements.

Under **"Sound"**, we mute our input hardware by toggling off the microphone icon in **"Input Volume"**.

> [!NOTE]
> The **"Privacy & Security"** menu in Ubuntu 24.04/26.04 features a critical diagnostic panel: **"Device Security"**. This tab displays the active state of **"Secure Boot"**. A green indicator confirms that Secure Boot is actively enforced. Secure Boot validates cryptographic signatures across the early boot loader chain, guaranteeing that only trusted binaries matching UEFI security policies are executed during host initialization.
>
> If warning indicators flag an untrusted or unverified kernel, it serves as an immediate alert that baseline hardware security features are disabled in our motherboard's BIOS/UEFI. Without these hardware locks, the confidentiality of data on a powered-on or suspended host degrades rapidly, exposing live RAM to cold-boot attacks and direct memory access (DMA) key extraction.
>
> The adjacent indicator displays **"Checks Passed"** / **"Protected"**. In an upcoming chapter, we will generate a diagnostic report via the terminal to inspect these low-level security assertions directly.

**Chapter Assets:** `_assets/images/3_system_settings`

<br>

## Getting Started with the Console

#### Initial Setup:

Launching the terminal for daily work is done via the applications menu (**"Show Apps"**). For quick and convenient access to the command line, we can pin the terminal shortcut to the **"Dock"** panel.

Ubuntu is based on Debian and uses the same `.deb` package format. Software installation is carried out via the APT package manager from the Ubuntu repositories. We manage and install these packages with APT, while administrative operations are executed through `sudo` as needed.

By default, after successful authentication, `sudo` caches the session for 15 minutes. During this timeframe, subsequent commands executed via `sudo` will typically not require re-entering the password. For a system with elevated security requirements, we consider this interval excessive and will reduce it to 0–2 minutes at the end of this chapter.

When we open a terminal window, a prompt string is displayed containing the current username, system hostname, and working directory, terminating with a dollar sign (**`$`**). This icon visually indicates that the shell is running under an unprivileged user session. To perform most configuration tasks, we must prepend commands with `sudo` (e.g., `sudo apt update`).

To transition into a fully interactive `root` superuser mode, we use the `sudo -i` or `sudo -s` commands. The `sudo -i` command completely simulates a clean root login by loading its own environment variables, while `sudo -s` launches a root shell while preserving the current user's environment variables. For acquiring a temporary root session, `sudo -i` is preferred. Unlike `sudo -s`, this mode launches a login shell with a clean `root` environment, making it convenient for extended administrative tasks. For routine operations, executing standalone commands via `sudo` without maintaining a persistent root session remains our recommended approach.

After successfully entering our password, the **`$`** symbol in the prompt will change to a hash mark (**`#`**). This signifies that the system has elevated to superuser mode with full administrative privileges. From here, modifying any file—including kernel parameters—is permitted, so we proceed with extreme caution.

> [!IMPORTANT]
> Memorizing foundational Linux terminal commands will make working with our system fast and efficient.

**GNOME Terminal in Ubuntu 24.04**

GNOME Terminal in Ubuntu 24.04 makes it easy to customize visual settings directly from the GUI menu. It offers window transparency and flexible color palette options down to custom hex codes, yielding an aesthetically comfortable environment for extended command-line sessions.

Before diving into core tasks, let us tune the appearance of the terminal. In the upper-right section of the window, next to the search icon, we click the **"Burger Menu"** (three horizontal lines) and select **"Preferences"**. Under the **"Profiles"** tab, we select the default profile **"Unnamed"**. Here, we can adjust colors, fonts, window dimensions, and transparency levels according to our preferences.

The main drawback is its reliance on the older GTK3 stack and the lack of certain modern isolation and security mechanisms present in GTK4 applications.

**Ptyxis in Ubuntu 26.04**

Before standardizing on Ptyxis for daily use, let us configure it for optimal comfort. We click the **"Burger Menu"** (three horizontal lines) in the top-right corner of the window and select **"Preferences"**. This opens the **"Appearance"** menu directly, where we can select a ready-made theme preset. First, we scroll down slightly and disable the **"Use System Font"** toggle, then choose our preferred font size. To choose a color palette, we click the **"Show All Palettes"** drop-down menu at the very top of the **"Appearance"** pane and select the scheme that best fits our workflow. For deeper color and font customization, we will need to edit configuration files directly.

**Custom Profile Setup for Ptyxis** 

**1.** We open a terminal and create the directory along with our custom profile file:
```bash
mkdir -p ~/.local/share/org.gnome.Ptyxis/palettes && nano ~/.local/share/org.gnome.Ptyxis/palettes/my-homebrew.palette
```

**2.** We paste the modified lighter dark-gray/deep-blue background profile configuration:
```ini
[Palette]
Name=My Homebrew

Foreground=#00ff00
Background=#171717 or #0b1020
Color0=#000000
Color1=#990000
Color2=#00a600
Color3=#999900
Color4=#0d0dbf
Color5=#b200b2
Color6=#00a6b2
Color7=#bfbfbf
Color8=#666666
Color9=#e50000
Color10=#00d900
Color11=#e5e500
Color12=#0000ff
Color13=#e500e5
Color14=#00e5e5
Color15=#e5e5e5

BellForeground=#00ff00
BellBackground=#171717 or #0b1020
RemoteForeground=#00ff00
RemoteBackground=#171717 or #0b1020
SuperuserForeground=#00ff00
SuperuserBackground=#171717 or #0b1020
```

To save the configuration in the `nano` editor, we press the key combination **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**3.** We apply slight window transparency. A value of `0.00` represents complete transparency, while `1.00` indicates total opacity. We choose the value that best fits our preference:
```bash
gsettings set org.gnome.Ptyxis.Profile:/org/gnome/Ptyxis/Profiles/$PTYXIS_PROFILE/ opacity 0.95
```

Next, we close the terminal and launch it again. The newly created profile should now appear in the **"Palettes"** section. Via the **"Burger Menu"** (three horizontal lines), we navigate to **"Preferences"** -> **"Appearance"** -> **"Show All Palettes"**, locate the **"My Homebrew"** profile, and select it.

> [!IMPORTANT]
> It is essential to understand that when comparing Ptyxis and GNOME Terminal, Ptyxis aligns significantly better with the security model adopted in this book due to its additional environment isolation capabilities. Replacing Ptyxis with the more familiar GNOME Terminal means forfeiting some of these defensive features and constitutes a compromise within our workflow.
> 
> We will also explore Ghostty later as an alternative terminal emulator. We will cover its installation and baseline setup separately so that we can compare it directly with Ptyxis and GNOME Terminal to determine the best fit for our system.

#### Disabling Automounting and Optional Tweaks:

**1.** The first thing we will do is disable automatic media mounting (this turns off auto-mounting, but does not prevent a user or application from mounting media manually):
```bash
gsettings set org.gnome.desktop.media-handling automount false && gsettings set org.gnome.desktop.media-handling automount-open false
```

**2.** We center newly launched application windows on the screen. In our experience, this makes navigating much more convenient, especially inside virtual machines:
```bash
gsettings set org.gnome.mutter center-new-windows true
```

If for any reason this window placement does not suit our workflow, we run the same command, replacing `true` with `false`.

**3.** To avoid wasting time navigating graphical menus, we restore the familiar keyboard layout switching using the classic `Shift + Alt` shortcut via two quick system commands:
```bash
gsettings set org.gnome.desktop.input-sources xkb-options "['grp:alt_shift_toggle']" && gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Shift>Alt_L', '<Alt>Shift_L']"
```

#### Managing Console Shell History:

By default, Bash maintains command history with a limited size: older entries are eventually overwritten, and running multiple terminal instances simultaneously can lead to race conditions during history saving. Additionally, history is typically written to the disk file only upon shell exit rather than after every individual command. In the event of an abrupt system termination, recent commands might be lost, which is unacceptable for our auditing workflow.

We will configure Bash to append commands to the history log immediately and increase its retention size to prevent data loss.

**1.** We open the `.bashrc` configuration file in our home directory:
```bash
nano ~/.bashrc
```

**2.** We jump to the very end of the file using **`Alt + /`** and append the following lines:

```bash
# Unlimited history size
export HISTSIZE=-1
export HISTFILESIZE=-1

# Write commands to history immediately after pressing Enter
export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"

# Ignore consecutive duplicate entries only
export HISTCONTROL=ignoredups

# Log exact timestamp (date and time) of execution
export HISTTIMEFORMAT="%F %T "

# Append commands to the history file instead of overwriting it
shopt -s histappend
```

We save the file with **`Ctrl + O`** -> **`Enter`**, then exit using **`Ctrl + X`**.

* `HISTSIZE=-1` and `HISTFILESIZE=-1` — completely remove limits on entry counts.
* `history -a` — forcibly writes each command to disk right after execution.
* `ignoredups` — removes consecutive identical entries without hiding commands starting with a space.
* `HISTTIMEFORMAT` — records timestamps, which is critical for incident investigations.
* `shopt -s histappend` — merges logs across multiple open terminal windows.

**3.** We apply the settings to the current session without restarting the terminal:
```bash
source ~/.bashrc
```

**4.** We verify that updated logging is functioning properly:
```bash
history
```

We now have an end-to-end, loss-prevention timeline complete with exact timestamps for every command executed.

**5.** We clear the terminal screen clutter:
```bash
clear
```

**6.** Occasionally, sensitive data (such as a password or API token) might accidentally be typed into the console. Leaving these details in the log files poses a security risk. To selectively remove the last erroneous command:
```bash
history -d $(history | tail -n 1 | awk '{print $1}')
```

**7.** If we need to completely purge the current session history and overwrite the file on disk, we combine the clear and write flags:
```bash
history -c && history -w
```
The `-c` flag completely clears the in-memory history of the active session, while `-w` forces this empty state to be written to the history file, erasing prior entries.

Even with immediate, unlimited history logging configured, a standard user (or an attacker gaining session access) can still manually wipe the history file using `history -c && history -w` or simply remove it with `rm ~/.bash_history`.

Standard permission changes via `chmod -w` will not work here: revoking write access prevents the Bash shell from capturing any new commands. Instead, the file must be configured to allow *append operations only*, strictly prohibiting *overwriting or deletion*.

Linux satisfies this requirement using extended file system attributes (`chattr`).

**8.** We switch to superuser mode, as modifying extended file attributes requires root privileges:
```bash
sudo -i
```

**9.** We assign the `+a` (append-only) attribute to the history file. Using the `$SUDO_USER` variable automatically resolves our original username, even from within the root session:
```bash
chattr +a /home/$SUDO_USER/.bash_history
```

**10.** If administrative duties later require clearing or editing this file, we remove the protection attribute using:
```bash
chattr -a /home/$SUDO_USER/.bash_history
```

We re-apply the `+a` attribute immediately after maintenance is completed.

> [!IMPORTANT]
> The `append-only` attribute is not a definitive defense mechanism. A user with root privileges can remove this attribute at any point to modify or delete the history file. We treat this configuration as an additional security layer rather than an infallible logging control.

#### Configuring a Secure sudo Session Timeout:

To force a change to the password cached credentials duration in the terminal, we will create an isolated configuration file. Direct editing of the main system `/etc/sudoers` file is discouraged to prevent syntax errors that could permanently revoke administrative privileges.

**1.** We launch the `nano` text editor to create a dedicated configuration snippet:
```bash
nano /etc/sudoers.d/99_sudo_timeout
```

**2.** We insert the following line into the empty file:
```ini
Defaults timestamp_timeout=2
```

The value `2` instructs `sudo` to retain authentication credentials for two minutes. Once this interval expires, subsequent `sudo` invocations will prompt for the password again. Alternatively, setting this value to `0` forces authentication on every execution, establishing a strict security posture for our hardened host.

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, followed by **`Ctrl + X`** to exit back to the root shell.

**3.** We apply appropriate file permissions:
```bash
chmod 0440 /etc/sudoers.d/99_sudo_timeout
```

> [!WARNING]
> Before closing the active terminal or exiting root mode, verifying the syntax of our newly applied rule is imperative:
> ```bash
> visudo -c
> ```
> If the system reports `...parsed OK`, the syntax is valid and safe to apply. If a syntax error is returned, we reopen the file using `nano` immediately to fix the issue. Failing to do so before closing the shell will render the `sudo` command unusable and lock us out of administrative access!

> [!NOTE]
> **Author's Note:** The `visudo` utility validates the syntax of files associated with the `sudo` security policy engine (specifically `/etc/sudoers` and included rules inside `/etc/sudoers.d/`). When modifying other system files (such as network configs, Firefox `user.js` profiles, firewall rules, or GRUB options), calling `visudo -c` is unnecessary as it does not parse non-sudo files.

**4.** We exit superuser mode to return to our unprivileged shell:
```bash
exit
```

**5.** A helpful trick for routine operations: to immediately invalidate an active `sudo` session token without waiting for the two-minute timeout to elapse, we execute:
```bash
sudo -k
```

The `sudo -k` command instantly revokes the cached authentication timestamp, ensuring that our next `sudo` command prompts for a password right away.

#### Creating the Checks Passed Verification File:

**1.** We create a text file to review the parameters under **"Privacy & Security"** -> **"Device Security"** -> **Checks Passed**:
```bash
touch ~/Downloads/checks_passed.txt
```

**2.** We open the newly created file using the `nano` editor:
```bash
nano ~/Downloads/checks_passed.txt
```

**3.** We paste the contents copied to our clipboard into `checks_passed.txt`:
```ini
OUR COPIED CLIPBOARD VALUES
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, followed by **`Ctrl + X`** to exit.

> [!NOTE]
> Adjusting specific parameters that failed validation depends on our primary system use case. For example, **Intel GDS Mitigation: !Fail (Not Enabled)** indicates that protection against the Gather Data Sampling (GDS) vulnerability is currently inactive. This can be caused by microcode status, kernel parameters, or system settings. Enabling mitigations may impact performance in certain scenarios, so we decide based on our specific CPU architecture, workload demands, and overall threat model.
> 
> Similarly, the line **Linux Swap: !Fail (Not Encrypted)** might initially raise concerns. However, if our swap partition or file resides inside a LUKS-encrypted volume, its data on disk is fully encrypted. Therefore, this flag alone does not mean our swap contents are stored in plaintext on physical storage.
> 
> To verify our current swap layout, we run:
> ```bash
> swapon --show
> ```
> 
> If the output points to `/swap.img`, the swap exists as a standard file inside the root file system. In our environment, the root file system is placed within a LUKS-encrypted volume, meaning the swap file contents inherit full encryption protection.

**Chapter Appendix:** *_assets\images\4_start_terminal*

<br>

## Network and VPN Configuration

#### For Ethernet (Wired Connection):

Without plugging in the cable, we open system **"Settings"** and select the **"Network"** section. We locate **"Wired"** and click the **"Network Options"** gear icon. In the resulting window, on the **"Details"** tab, we immediately uncheck **"Make available to other users"** and **"Connect automatically"**.

Next, we move to the **"Identity"** tab. In the **"MAC Address"** field, we select our active network interface. Its interface name (e.g., `enp0s1`, `ens33`, or similar) will be displayed alongside—we need to remember or write it down, as it is critical for our downstream network and firewall configurations.

Let's switch to the **"IPv4"** tab. Here, we forcibly set our own custom DNS server so we don't use the DNS servers provided by our ISP. We toggle **"DNS"** from **"Automatic"** to **"Off"**, using Quad9 as an example: `9.9.9.9` (alternative: `149.112.112.112`). We enter: `9.9.9.9, 149.112.112.112` separated by a comma. This allows us to move DNS resolution outside our provider's infrastructure.

In the **"IPv6"** tab, under **"IPv6 Method"**, we strictly select **"Disable"**. After completing all these adjustments, we click **"Apply"**.

> [!IMPORTANT]
> Let's remember that disabling IPv6 in the graphical interface only protects this specific chosen network profile. To reduce the risk of a real IP address leak via IPv6 (IPv6 Leak) when working with any type of VPN, a bit later—in the chapter on fine-tuning the kernel (`sysctl.conf`)—we will forcibly disable this protocol globally at the system level.

> [!NOTE]
> **Note:** We can view the exact name of our network card using the `ip a` command.

In the **"Cloned Address"** field, we can configure address spoofing. For instance, if we specify `08:00:27:E5:CA:C1`, this network node will completely mimic a VirtualBox virtual machine. However, a much more reliable option for everyday privacy is selecting **"Random"**. The **"Random"** setting will generate a new MAC address upon every connection event. If we are deploying Ubuntu inside a virtual machine (VM), we leave **"Cloned Address"** empty!

In Ubuntu 24.04/26.04, NetworkManager profiles are stored via the Netplan backend; therefore, if we need guaranteed MAC address management, we will configure the parameter directly through NetworkManager and its configuration.

#### For Wi-Fi (Wireless Connection):

**1.** First, we check our network interface name and record it (as it will be required for subsequent configuration steps):
```bash
ip a
```

After completing this step, we jump to the section **Setup for Physical Hardware (Full Randomization)**, follow the instructions step by step, and then return back to this part of the chapter.

In **"Show Apps"**, we open **"Settings"**, go to **"Wi-Fi"**, and toggle the switch to active. Below, we will see active Wi-Fi networks or only our configured network. We click it with the mouse. In the authentication window that appears, we click **Cancel**, after which a gear icon will show up next to the network name. First, on the **"Details"** tab, we uncheck **"Make available to other users"** and **"Connect automatically"**.

Next, we switch to the **"Identity"** tab. In the **"MAC Address"** field, we select our active network interface, and in **"Cloned Address"**, we set the value to **"Random"**.

Let's move to the **"IPv4"** tab. Here, we forcibly set our own custom DNS server to avoid using ISP-provided DNS servers. We toggle **"DNS"** from **"Automatic"** to **"Off"** and enter reliable, no-log Quad9 servers: `9.9.9.9` (alternative: `149.112.112.112`).

In the **"IPv6"** tab, under **"IPv6 Method"**, we strictly select **"Disable"**.

We open the **"Security"** tab and enter eight random characters into the password field, after which the **"Apply"** button will become active. We click it to apply all settings at once. In general, entering the real password works too—a network connection won't happen anyway. But since we are paranoid, we will play it safe and enter the real password only right before our first internet access for system updates.

We disable Wi-Fi by toggling the switch to the inactive state.

* **Setup for Physical Hardware (Full Randomization)**

For physical hardware, the optimal choice is generating a completely new random MAC address upon every connection to the network. Configuration files in `conf.d` are parsed in lexicographical order, so naming a file `99-...` allows us to place our parameters after default configuration files, thereby increasing their priority.

**1.** We enter the terminal with superuser privileges:
```bash
sudo -i
```

**2.** We create a priority rules configuration file:
```bash
nano /etc/NetworkManager/conf.d/99-macrandom.conf
```

**3.** We insert the following parameter block into the opened editor to activate automatic address changing:
```ini
[device]
wifi.scan-rand-mac-address = yes

[connection]
ethernet.cloned-mac-address = random
wifi.cloned-mac-address = random
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit back to the shell.

**4.** We restart the network service to apply settings immediately:
```bash
systemctl restart NetworkManager
```
Now, upon every new connection to any network, the system will generate a new random MAC address.

**5.** After restarting the network service, we run a final verification (where we replace `enp0s1` with our actual interface name):
```bash
ip link show enp0s1
```

> [!TIP]
> To avoid typing the full interface name manually, we can use a trick: type the command and the first letter of the interface (`e` for wired connections, `w` for wireless) and press **Tab**—the system will auto-complete the name for us.

If everything worked as expected, we will see in the last output line: `link/ether "generated MAC" brd ff:ff:ff:ff:ff:ff permaddr "real MAC"`.

As a reminder, when setting up a Wi-Fi connection, we return back to the next step in the section **For Wireless Connection (Wi-Fi)**.

* **Setup for Virtual Machines (Strict Vendor Spoofing)**

In virtual environments on Ubuntu 24.04/26.04, the Netplan and NetworkManager combination blocks automatic MAC address changes via the GUI, resetting it back to the hypervisor's factory prefix (e.g., `00:0c:29:...` for VMware) upon every host reboot. This instantly de-anonymizes our virtual machine usage.

To permanently disguise our system as real bare-metal hardware while preserving full GUI functionality, we will force the Linux kernel itself to override the MAC address at the earliest boot stage using the `rc.local` system automation script.

**1.** We enter the terminal with superuser privileges:
```bash
sudo -i
```

**2.** We create a low-level hardware configuration system script:
```bash
nano /etc/rc.local
```

**3.** We insert the following block of commands into the opened editor: 
```bash
#!/bin/bash
# Seamless kernel-level strict MAC spoofing at OS startup (replace enp0s1 with your interface name)
ip link set dev enp0s1 down
ip link set dev enp0s1 address 28:80:8A:8F:32:7D
ip link set dev enp0s1 up
exit 0
```
To save the file in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit back to the shell.

> [!NOTE]
> The Linux kernel prohibits changing the MAC address of an active network card. Therefore, our script first downs the interface for a fraction of a second, replaces the address with a "legitimate" Intel one, and then instantly brings the card back active for the graphical manager to handle.
>
> Instead of the Intel address, we can enter any other valid MAC address of real physical hardware:
>
> * Example MAC address: `00:E0:4C:A1:22:33` — Spoofing as a Realtek chipset (prefix `00:E0:4C`; `FC:93:4E`; `50:3E:AA`; `00:13:70`; `00:23:CD`, etc.)
> * Example MAC address: `04:92:26:BC:55:66` — Spoofing as an ASUS laptop (prefix `04:92:26`; `04:D4:C4`; `04:D9:F5`; `08:60:6E`; `08:BF:B8`, etc.)
> * Example MAC address: `28:80:8A:8F:32:7D` — Spoofing as an Intel chipset (prefix `28:80:8A`; `28:7F:CF`; `28:7F:CF`; `28:C5:D2`; `14:85:7F`, etc.)
> * Example MAC address: `3C:50:02:DC:1E:55` — Spoofing as an Apple laptop (prefix `3C:50:02`; `60:81:10`; `A4:83:E7`; `00:1C:B3`; `00:17:F2`, etc.)
> * Example MAC address: `00:14:22:F1:A8:D3` — Spoofing as a Dell chipset (prefix `00:14:22`; `00:15:C5`; `00:21:70`; `74:86:7A`; `D0:94:66`, etc.)
>
> We can learn more about MAC address pools on the internet!

**4.** We tighten security controls **(Critical!)**. We make our script executable at the OS level, otherwise the kernel will ignore it during boot:
```bash
chmod +x /etc/rc.local
```

**5.** We send the virtual machine into a clean reboot to test the automation in action:
```bash
reboot
```

**6.** After rebooting, we open the terminal and run our final verification (where we replace `enp0s1` with our interface name):
```bash
ip link show enp0s1
```
In the command output's `link/ether` line, we should see our new hardcoded Intel/Realtek spoofed MAC address, while the actual factory VM prefix will remain permanently hidden under the `permaddr` parameter. At the same time, network GUI settings and the VPN import button will stay fully functional.

#### NetworkManager Hardening: Suppressing Local mDNS, LLMNR, Hostname Leaks, and Securing DNS:

By default, `NetworkManager` can use local name resolution mechanisms like mDNS (Multicast DNS) and LLMNR (Link-Local Multicast Name Resolution), designed for device discovery and name resolution within local networks.

On public networks—such as coffee shops, coworking spaces, or hotels—these protocols can leak our computer's hostname and presence to local peers. These requests are especially unwanted in scenarios where our VPN tunnel is not yet established or temporarily unavailable: local network traffic continues directly through the main interface during such moments.

Additionally, during automatic network configuration, DNS servers can be assigned via DHCP from the local router. Depending on network setup, this allows the use of our ISP's or access point operator's DNS infrastructure. To minimize local network queries and avoid relying on automatic parameters, we will set our own DNS servers and disable unnecessary local name resolution mechanisms.

To do this, we will create a dedicated `NetworkManager` configuration file to enforce our parameters.

**1.** We open the terminal and create our privacy file:
```bash
sudo nano /etc/NetworkManager/conf.d/99-privacy-hardening.conf
```

**2.** We insert the following configuration block bound to our interfaces:
```ini
[device-privacy]
match-device=file:/sys/class/net/e*,file:/sys/class/net/w*
# Total suppression of mDNS at the network connection level
mdns = 0
# Complete suppression of the LLMNR protocol
llmnr = 0

[connection-privacy]
match-device=file:/sys/class/net/e*, file:/sys/class/net/w*
# Protection against DHCP de-anonymization (we do not send hostnames to routers)
ipv4.dhcp-send-hostname = false
ipv6.dhcp-send-hostname = false
ipv4.dhcp-fqdn = none
ipv6.dhcp-fqdn = none
# Forced override of DNS settings from the local router
# (Protection against DNS traffic interception via rogue DHCP servers)
ipv4.ignore-auto-dns = yes
ipv6.ignore-auto-dns = yes
```
To save the file in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit back to the shell.

**3.** We restart the service to apply privacy policies immediately:
```bash
sudo systemctl restart NetworkManager
```

**4.** For Netplan, we run the command specifying our connection name (e.g., `Wired connection 1` or our Wi-Fi SSID name) and required settings:
```bash
sudo nmcli connection modify YOUR-CONNECTION-NAME ipv4.ignore-auto-dns yes
```

**5.** We set our static DNS servers (specifying our connection name):
```bash
sudo nmcli connection modify YOUR-CONNECTION-NAME ipv4.dns 9.9.9.9
```

**6.** We set permissions on the `yaml` file with NM rules:
```bash
sudo chmod 0600 /etc/netplan/01-network-manager-all.yaml
```

**7.** We apply the settings so everything works without a system reboot:
```bash
sudo netplan apply
```

**8.** We verify our configuration (`-LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported` is a positive indicator for us):
```bash
resolvectl status
```

#### Setting Up a VPN Connection:

If using a VPN connection, we follow the steps below; if no VPN is present, we skip this section.

In the same **"Network"** menu, right below **"Wired"**, we find the VPN setup section. By default, its status shows *«Not set up»*. We click the plus icon on the right and select **«Import from file...»**. We select our pre-prepared `.ovpn` configuration file (for example, from an encrypted USB drive) and import it. Base profile configuration is now complete.

> [!WARNING]
> **Warning!** Launching OpenVPN directly via the terminal in default mode does not protect against traffic leaks during an abrupt connection drop or server failure. We will configure a strict Kill Switch later using our built-in host firewall.
> 
> After successful import and VPN verification, inside the VPN connection settings under the **«IPv4»** tab, we recommend explicitly specifying private DNS resolvers belonging to our specific VPN provider (usually an internal gateway like `10.8.0.1`), or using independent secure addresses guaranteed not to log data:
> 
>* *Mullvad DNS:* `194.242.2.2` (basic) or `194.242.2.3` (with automatic ad and tracker blocking). A project by one of the most private and reputable VPN providers in the world.
>* *Quad9:* `9.9.9.9`. Servers are based in Switzerland, strictly complying with stringent European privacy laws and automatically filtering phishing and malicious sites at the DNS query level.
>* *Control D (Uncensored):* `76.76.2.0`. Completely independent and fast resolver with zero censorship, logs, or restrictions.
> 
> **Network Protocol Isolation (IPv6 Leak Prevention):**
> Even if we globally disable IPv6 traffic handling in UFW firewall settings (using `sudo sed -i 's/IPV6=yes/IPV6=no/' /etc/default/ufw`), the tunnel's virtual interface (`tun0`) may ignore this rule upon initialization. If the remote VPN server supports IPv6, the OS will attempt to route part of the traffic through it, bypassing our IPv4 Kill Switch rules.
> 
> To completely eliminate this critical leak vector, right after importing our configuration, we open our created VPN connection settings, switch to the **«IPv6»** tab, and forcibly set **«IPv6 Method»** to **«Disable»**.
> 
> **NetworkManager Architectural Security:**
> Upon a successful GUI import, the system automatically extracts all cryptographic keys and stores them in isolated system directories. The original `.ovpn` file can then be safely removed from our USB drive.

In modern Ubuntu releases, importing complex configuration files with specific routes via standard GUI can fail due to strict security policies in the built-in `network-manager-openvpn` plugin. **If the GUI throws an error, it is much more reliable for us to launch the session directly through the terminal.**

> [!IMPORTANT]
> We strictly prohibit launching OpenVPN directly from standard user directories (such as `Downloads`). Keys and configs must reside where root kernel permissions protect them; otherwise, compromising a user session (e.g., via a browser) could lead to the theft of our VPN credentials.

**Chapter Appendix:** *_assets\images\5_network_vpn*

#### Purging Compromising Bluetooth Components:

The Bluetooth wireless protocol is used extremely rarely, so for security purposes, it is far more effective to deactivate and isolate it completely rather than constantly monitoring its active broadcast status. This protocol has many known and potential zero-day (0-day) vulnerabilities, creating dangerous attack vectors for close-range remote attacks. If our computer is in a cafe, coworking space, or public place, attackers could target the kernel's Bluetooth stack to gain remote control over our device.

**1.** We block the Bluetooth transmitter at the kernel level (soft-block), preventing the chip from broadcasting radio signals:
```bash
sudo rfkill block bluetooth
```

**2.** We completely isolate the Bluetooth stack in user space, disabling automatic startup of the system service at boot, while the `--now` flag stops its active execution in host RAM immediately:
```bash
sudo systemctl disable --now bluetooth
```

**3.** We open our kernel module blacklist configuration file:
```bash
sudo nano /etc/modprobe.d/blacklist-hardening.conf
```

**4.** We add the following lines for complete kernel-level Bluetooth isolation:
```ini
blacklist bluetooth
blacklist btusb
blacklist btrtl
blacklist btbcm
blacklist btintel
install bluetooth /bin/true
install btusb /bin/true
install btintel /bin/true
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit back to the shell.

**5.** We finalize our changes and embed the new configuration into the initial boot RAM disk image:
```bash
sudo update-initramfs -u -k all
```

Once completed, the Linux kernel physically will not load drivers upon detecting the device. For the system, this chip becomes a "piece of dead silicon"—completely eliminating background software bypasses by malware or hidden rootkits.

> [!IMPORTANT]
> This closes 99.9% of attack vectors, though the chip remains powered. Absolute guarantees against advanced hardware rootkits require physically removing the card from its slot or desoldering it.

<br>

## Security Configuration and GRUB Bootloader Hardening

#### Setting a Password to Protect GRUB:

To eliminate unauthorized editing of Linux kernel parameters (preventing *Evil Maid* attacks) when physical access to the computer is present, we must set an administrative password on the GRUB bootloader. Without this defense, anyone powering on the PC can modify boot lines, pass `init=/bin/bash` to the kernel, and bypass standard authentication at the boot stage.

We open the terminal and execute the following steps in sequence:

**1.** We launch the secure hash generation utility. The system will prompt us to enter and confirm a password (we recommend using a complex password at least 16 characters long):
```bash
grub-mkpasswd-pbkdf2
```

The utility will output a long hash string starting with `grub.pbkdf2.sha512...`. We highlight and copy this entire string.

> [!NOTE]
> In Ubuntu distributions, the GRUB configuration is typically auto-generated from `/etc/default/grub` settings and scripts inside `/etc/grub.d/`. An error in any of these files can cause `update-grub` to fail when generating `grub.cfg`.
> 
> To avoid modifying default generation scripts, we will utilize a dedicated `/boot/grub/custom.cfg` file. GRUB automatically includes this file upon boot, allowing us to isolate user configurations from auto-generated setups.

**2.** We create an autonomous authorization configuration file at the lowest bootloader level:
```bash
sudo nano /boot/grub/custom.cfg
```

**3.** Inside the opened file, we insert two clean lines declaring the superuser and binding our generated hash to it (without quotes or Bash syntax):
```text
set superusers="root"
password_pbkdf2 root OUR_COPIED_HASH_FROM_STEP_1
```

To save our changes in the `nano` editor, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit back to the console.

By default, declaring a superuser in GRUB locks the bootloader entirely—the system will demand a password on every routine reboot. To ensure the operating system boots automatically while demanding a password *only* upon attempting unauthorized menu editing (pressing **`e`**) or launching the console (pressing **`c`**), we must allow unrestricted kernel booting.
 
**4.** To do this, we open the generator system template:
```bash
sudo nano /etc/grub.d/10_linux
```

**5.** We locate the line starting with `CLASS=` (usually `CLASS="--class gnu-linux --class gnu --class os"`), and append the `--unrestricted` parameter so it matches the following format:
```ini
CLASS="--class gnu-linux --class gnu --class os --unrestricted"
```
We save the file with **`Ctrl + O`** -> **`Enter`**, then exit using **`Ctrl + X`**.

**6.** We apply our settings to GRUB at the OS level:
```bash
sudo update-grub
```

**7.** We enforce strict access permissions on our created `custom.cfg` file, completely hiding the password hash from being read by standard unprivileged users on the system:
```bash
sudo chmod 0600 /boot/grub/custom.cfg
```

> [!WARNING]
> After applying these modifications, our GRUB password will not be required during standard Ubuntu boots, making it very easy to forget due to infrequent use. However, in emergency scenarios (such as filesystem errors or recovering system access), the bootloader will demand it. To eliminate the risk of losing administrative control, make sure to write this password down on paper and store it securely (e.g., in a safe) or save it inside an offline password manager vault (such as KeePassXC). We will cover installing and configuring this software in detail in upcoming chapters.

#### Software IOMMU Hardening: Protecting RAM Against Kernel-Level DMA Attacks:

Since we established the necessity of defending against dangerous DMA (*Direct Memory Access*) attacks early on, relying solely on disabling Sleep Mode or trusting BIOS/UEFI settings is entirely insufficient. On many consumer laptops and motherboards, vendors deliberately hide or cut hardware port authorization features for Thunderbolt and USB4 interfaces. 

To guarantee uncompromised defense, we must forcibly activate and tune the **IOMMU** subsystem at the GRUB kernel bootloader level. This forces the central processing unit to hardware-isolate RAM address spaces, completely blocking external devices from gaining direct access to host RAM without operating system mediation.

> [!NOTE]
> To maintain operational hygiene, we place Linux kernel hardware initialization parameters into a dedicated system drop-in directory. This protects our low-level flags from accidental overwrite by package managers during routine system updates.

We open the terminal on our primary host system and execute the following steps in sequence:

**1.** We create our independent kernel security configuration file inside the drop-in directory:
```bash
sudo nano /etc/default/grub.d/99_security_baseline.cfg
```

**2.** Inside the opened file, we insert a single operational line containing memory isolation initialization flags matching our physical CPU architecture.

* **For Intel Processors:**
```ini
GRUB_CMDLINE_LINUX_DEFAULT="${GRUB_CMDLINE_LINUX_DEFAULT} intel_iommu=on iommu=pt"
```

* **For AMD Processors:**
```ini
GRUB_CMDLINE_LINUX_DEFAULT="${GRUB_CMDLINE_LINUX_DEFAULT} amd_iommu=on iommu=pt"
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

* **`intel_iommu=on / amd_iommu=on`** — forcibly initializes the IOMMU driver at the CPU architecture level upon system boot.
* **`iommu=pt`** (*Pass-Through*) — enables pass-through mode for internal host devices (e.g., integrated graphics), mapping direct address translations only for legitimate built-in buses. This delivers maximum performance and baseline stability by default.

> [!WARNING]
> If we are porting settings from this book to our bare-metal hardware (rather than a virtual machine), replacing `iommu=pt` (trusted pass-through mode) with `iommu=force` is our best choice. 
> This strict flag prevents the Linux kernel from automatically putting newly connected external devices (especially via Thunderbolt/USB4/PCIe protocols) into trusted mode. The kernel forcibly applies DMA address translation tables to every interface without exception.
> **We perform a safe test on physical hardware first:** We reboot, enter the GRUB menu, and press **`e`** (entering our `root` login and GRUB password defined previously). In the kernel parameters line, we change `iommu=pt` to `iommu=force`. We press **`Ctrl + X`** to boot. If our system reaches the desktop without graphic freezes, and Wi-Fi and sound operate normally, our hardware is fully compatible with strict hardening. Only then do we commit this parameter permanently!
> On VirtualBox and VMware testbeds, the strict isolation flag `force` can cause GNOME desktop deadlocks by blocking the virtual display adapter (VMSVGA).

We save our changes in `nano` via **`Ctrl + O`** -> **`Enter`**, then **`Ctrl + X`**.

**3.** We update the bootloader configuration in the operating system so the kernel compiles and applies our new low-level instructions:
```bash
sudo update-grub
```

**4.** We force a computer reboot to apply hardware memory isolation:
```bash
sudo systemctl reboot -i
```

**5.** Following reboot, we open the terminal and execute verification. We inspect the kernel ring buffer logs via `dmesg` with `sudo` privileges to confirm defense deployment across RAM:
```bash
sudo dmesg | grep -E "iommu|IOMMU|dmar"
```

> [!IMPORTANT]
> Prior to OS boot, we enter BIOS/UEFI and set **Intel VT-d** (for Intel CPUs) or **AMD-Vi / IOMMU** (for AMD CPUs) to **Enabled**. If omitted, the kernel will ignore our boot parameters and log an error.

> [!TIP]
> If terminal output displays lines such as *"DMAR: IOMMU enabled"*, *"DMAR: Intel-IOMMU"*, or confirms hardware translation map initialization, our PC is now hardware-protected against direct RAM extraction via malicious DMA hardware cards!

> [!NOTE]
> **Optional Tuning for Ubuntu 26.04:** If `unattended-upgrades` introduces excessive delays during system shutdown or reboot (interfering with routine `sudo reboot`), we can override its `TimeoutStopSec` using a systemd drop-in without modifying the original package unit file.
> 
> We create the directory and override configuration file:
> ```bash
> sudo mkdir -p /etc/systemd/system/unattended-upgrades.service.d && sudo nano /etc/systemd/system/unattended-upgrades.service.d/override.conf
> ```
> 
> We define a 1-minute timeout value inside:
> ```ini
> [Service]
> TimeoutStopSec=60
> ```
> 
> We reload the systemd daemon:
> ```bash
> sudo systemctl daemon-reload
> ```
> 
> We verify our modification (it should return `TimeoutStopUSec=1min`):
> ```bash
> systemctl show unattended-upgrades.service -p TimeoutStopUSec
> ```

<br>

## Configuring the UFW Firewall With and Without a Kill Switch

#### Setting Up the Firewall with a Kill Switch:

In Ubuntu, before connecting to the internet, we must configure the firewall via the terminal. We execute the following steps sequentially:

First, we disable all IPv6 traffic processing in system firewall settings to eliminate hidden data leaks.

**1.** We set the firewall to active mode. It will now start automatically upon every operating system boot:
```bash
sudo ufw enable
```

**2.** We disable IPv6 protocol support inside the UFW subsystem configuration file:
```bash
sudo sed -i 's/IPV6=yes/IPV6=no/' /etc/default/ufw
```

**3.** We verify operating status. The firewall is running, but currently using default rules:
```bash
sudo ufw status verbose
```

**4.** We completely deny all incoming traffic and any external connection attempts to our PC:
```bash
sudo ufw default deny incoming
```

**5.** We block all outgoing traffic. This turns the firewall into a strict Kill Switch: it completely cuts off data leaks across all ports, temporarily disabling internet access on the machine:
```bash
sudo ufw default deny outgoing
```

**6.** We block any packet forwarding through our system:
```bash
sudo ufw default deny forward
```

**7.** We allow outgoing traffic strictly to the IP address and port of our specific VPN server (selecting `udp` or `tcp` according to our `.ovpn` file). We replace the placeholders `VPN_IP` and `PORT` with our real technical details:
```bash
sudo ufw allow out to VPN_IP port PORT proto udp
```

> [!IMPORTANT]
> If our VPN provider uses a domain name in its configuration (e.g., `server.mullvad.net`), we must determine its numerical IP address and enter that instead, otherwise the firewall will block domain resolution and the VPN tunnel will fail to establish.

**8.** We allow outgoing DNS traffic (port 53) strictly through the secured VPN interface, which is typically named `tun0`. If our VPN uses a different interface name, we specify that instead:
```bash
sudo ufw allow out on tun0 to any port 53 proto udp
```

**9.** We open the outbound HTTP port (80), routing traffic exclusively into the VPN tunnel:
```bash
sudo ufw allow out on tun0 to any port 80 proto tcp
```

**10.** We open the outbound secured HTTPS port (443) through the VPN interface:
```bash
sudo ufw allow out on tun0 to any port 443 proto tcp
```

**11.** We list all created rules alongside their unique ID numbers. This makes managing them straightforward:
```bash
sudo ufw status numbered
```

**12.** We enable network activity logging. Available modes include `low`, `medium`, `high`, and `full`. The `medium` value provides an ideal balance for monitoring anomalies without cluttering the disk with logs:
```bash
sudo ufw logging medium
```

To allow proper operation of local services and isolated development environments (e.g., VS Code, Portmaster, or LM Studio), we must add rules for the loopback interface (`localhost`):

**13.** We allow all inbound local connections within the host:
```bash
sudo ufw allow in on lo to any
```

**14.** We allow all outbound local connections within the host:
```bash
sudo ufw allow out on lo to any
```

**15.** We open port 853 across physical and virtual interfaces for the secure DNS-over-TLS protocol (relevant when using Portmaster):
```bash
sudo ufw allow out to any port 853 proto tcp
```

**16.** We allow fast tunnel connections (QUIC/UDP) for traffic filtering systems inside the VPN:
```bash
sudo ufw allow out on tun0 from any to any proto udp
```

**17.** We perform a final check on firewall status. Baseline firewall setup is successfully complete:
```bash
sudo ufw status verbose
```

**18.** We open the UFW sysctl configuration file using the `nano` editor:
```bash
sudo nano /etc/ufw/sysctl.conf
```

**19.** Near the end of the file, we locate the martian logging lines and change their values from zero to one:
```ini
net/ipv4/conf/all/log_martians=1
net/ipv4/conf/default/log_martians=1
```

To save our configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, then **`Ctrl + X`** to exit.

**20.** We reload UFW to apply our updated firewall rules:
```bash
sudo ufw reload
```

**21.** We call the built-in reference manual for the utility (highly recommended reading):
```bash
man ufw
```

#### Important Addition on Managing Rule Priority:

Occasionally, we may need to block a specific malicious IP address or an entire subnet. For instance, while analyzing traffic in Wireshark, we might notice the system repeatedly attempting to communicate with IP addresses `84.17.56.74` and `84.17.56.91` over port 80. We can choose to block them individually or block the entire subnet.

It is critically important to understand UFW rule logic: rules are processed strictly from top to bottom. If we append a block rule to the end of the list, it will sit below our general allow rule for port 80 (Rule #9), causing the firewall to ignore it and pass the packet. For a block rule to take effect, we must forcibly insert it at the top of the list using `insert N`, where `N` represents the position number at the start of the table:

**1.** We enforce a strict connection block to a specific IP on port 80. The rule takes first priority and is processed before all others:
```bash
sudo ufw insert 1 deny out to 84.17.56.74 port 80
```

**2.** We block outbound traffic to the entire `84.17.56.0/24` subnet on port 80:
```bash
sudo ufw insert 1 deny out to 84.17.56.0/24 port 80
```

**3.** We reload and apply the updated firewall rules:
```bash
sudo ufw reload
```

If we need to remove an incorrect rule, we use its unique ID number. Note that deleting a rule automatically shifts the remaining table rules upward, altering their position numbers. Therefore, we must re-issue the numbered list command before deleting subsequent rules:

**4.** We display the current rule list with updated position numbers:
```bash
sudo ufw status numbered
```

**5.** Example of deleting a rule currently assigned position number 5:
```bash
sudo ufw delete 5
```

#### Alternative Configuration Setup (Without VPN / For Guest OS):

If configuring the system without a VPN tunnel (such as inside an isolated Guest OS in VirtualBox, where host traffic is already secure), port forwarding commands will use the `any` target parameter instead. The complete sequence is as follows:

**1.** We set the firewall to active mode:
```bash
sudo ufw enable
```

**2.** We disable IPv6 protocol support inside the UFW subsystem configuration file:
```bash
sudo sed -i 's/IPV6=yes/IPV6=no/' /etc/default/ufw
```

**3.** We completely deny all incoming traffic:
```bash
sudo ufw default deny incoming
```

**4.** We block all outgoing traffic:
```bash
sudo ufw default deny outgoing
```

**5.** We block any packet forwarding:
```bash
sudo ufw default deny forward
```

**6.** We allow outbound DNS traffic (port 53) to all servers via UDP:
```bash
sudo ufw allow out to any port 53 proto udp
```

**7.** We open standard outbound HTTP traffic (port 80) to all destinations:
```bash
sudo ufw allow out to any port 80 proto tcp
```

**8.** We open secure outbound HTTPS traffic (port 443) to all destinations:
```bash
sudo ufw allow out to any port 443 proto tcp
```

**9.** We allow all inbound local connections on the loopback interface `lo`:
```bash
sudo ufw allow in on lo to any
```

**10.** We allow all outbound local connections on the loopback interface `lo`:
```bash
sudo ufw allow out on lo to any
```

**11.** We open outbound port 853 to all servers for secure DNS-over-TLS protocol:
```bash
sudo ufw allow out to any port 853 proto tcp
```

**12.** We enable medium-level network activity logging:
```bash
sudo ufw logging medium
```

**13.** We check final status for our configured firewall:
```bash
sudo ufw status verbose
```

**14.** We open the UFW sysctl configuration file using `nano`:
```bash
sudo nano /etc/ufw/sysctl.conf
```

**15.** Near the end of the file, we locate the martian logging lines and change their values from zero to one:
```ini
net/ipv4/conf/all/log_martians=1
net/ipv4/conf/default/log_martians=1
```

To save our configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, then **`Ctrl + X`** to exit.

**16.** We reload UFW to apply our updated firewall rules:
```bash
sudo ufw reload
```

> [!IMPORTANT]
> Starting with Ubuntu 22.04, the classic `iptables` subsystem is deprecated and replaced by the modern, high-performance `nftables` engine. UFW now acts as a user-friendly frontend interface over `nftables`. To inspect raw kernel network rules directly, we use the updated command instead of `sudo iptables -L`:
> ```bash
> sudo nft list ruleset
> ```

**17.** We test our local port:
```bash
ssh localhost
```

The output should clearly display *"Connection refused"*. This confirms that the remote access service is inactive, ports are closed, and our system is operating normally.

<br>

## Kernel Tuning, Access Control, and Purging Unnecessary System Services

#### Protecting the Network Stack and Kernel Memory Subsystem:

Prior to connecting to global networks, we must execute several critically important modifications to the operating system kernel, baseline file permissions, and verify the activity of the SSH remote access service.

We protect the network stack and kernel memory subsystem. To achieve this, we create a dedicated, isolated configuration file inside the `sysctl.d` directory. All configurations must be performed with superuser privileges:

**1.** We switch to interactive superuser mode (`root`):
```bash
sudo -i
```

**2.** We create and open a new configuration file using the `nano` text editor:
```bash
nano /etc/sysctl.d/99-security-hardening.conf
```

Inside the empty file, we add the following low-level kernel security parameters:
```ini
# Protection against buffer overflow vulnerabilities (enabling ASLR)
kernel.randomize_va_space = 2

# Protection against IP Spoofing via Reverse Path Filtering
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1

# Disable IP Source Routing
net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.default.accept_source_route = 0

# Ignore malicious ICMP broadcast requests and bogus error responses
net.ipv4.icmp_echo_ignore_broadcasts = 1
net.ipv4.icmp_ignore_bogus_error_messages = 1

# Log packets with invalid (spoofed) source addresses (Martian Packets)
net.ipv4.conf.all.log_martians = 1
net.ipv4.conf.default.log_martians = 1

# Completely disable the IPv6 protocol at the kernel level to minimize attack vectors
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

# Protection against SYN-Flood DoS attacks
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_synack_retries = 3

# Disable sending ICMP redirects (system is not a router)
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0

# Prevent writing to unsafe FIFO files in shared directories
fs.protected_fifos = 2

# Prevent writing to regular files owned by others in sticky shared directories
fs.protected_regular = 2

# Append process PID to core dumps so malware cannot overwrite existing logs
kernel.core_uses_pid = 1

# Hide kernel pointer addresses in /proc/kallsyms even from root to block offset calculations for exploits
kernel.kptr_restrict = 2

# Restrict reading the kernel log buffer to privileged users
kernel.dmesg_restrict = 1

# Restrict unprivileged users from using the kernel performance subsystem (perf) for side-channel attacks
kernel.perf_event_paranoid = 3

# Disable SysRq magic key combinations to block physical reboot or core memory dump attacks
kernel.sysrq = 0

# Strengthen ptrace restrictions to protect processes from unauthorized tracing
kernel.yama.ptrace_scope = 2

# Block unprivileged users from passing raw BPF programs to the kernel and enable constant JIT blinding
kernel.unprivileged_bpf_disabled = 1
net.core.bpf_jit_harden = 2
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**3.** We exit superuser mode and return to standard user privileges:
```bash
exit
```

**4.** Since we do not use remote desktop services, we explicitly disable the service:
```bash
sudo systemctl disable --now gnome-remote-desktop.service
```
**5.** We disable the service handling modem communications and mobile networks:
```bash
sudo systemctl disable --now ModemManager.service
```

#### Low-Level sysctl Hardening: Defense Against TCP Timestamp Fingerprinting:

Even with a strict UFW firewall active and operating system markers hidden, the Linux kernel can still reveal itself at the network layer through TCP packet parameters. One of the most dangerous passive deanonymization vectors is **TCP Timestamp Fingerprinting (RFC 1323)**.

When establishing a network connection (SYN packet), the Linux kernel includes a timestamp (`TSval`) inside the TCP header by default. This counter increments at a fixed frequency (often based on kernel system jiffies).

By analyzing this parameter (for example, through passive traffic sniffing or Nmap scanners), a remote server or Internet Service Provider can:

* Calculate the exact **uptime** of our operating system since its last boot.
* Perform session correlation: if we switch VPN servers or IP addresses while the uptime and TCP tick frequency remain identical, the remote party immediately identifies the traffic as originating from the same physical computer.
* Identify hidden devices operating behind a NAT router.

To eliminate this vector, we must forcibly disable timestamp generation across the kernel network stack.

**1.** We open our previously created kernel protection configuration file:
```bash
sudo nano /etc/sysctl.d/99-security-hardening.conf
```
**2.** We navigate to the end of the file and append the following parameters:
```ini
# Disable TCP timestamps to protect against fingerprinting and uptime tracking
net.ipv4.tcp_timestamps = 0

# Defense against replay attacks (RFC 1323) when timestamps are disabled
net.ipv4.tcp_tw_reuse = 0
```
To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

> [!IMPORTANT]
> **Author's Note:** Disabling `tcp_timestamps` effectively masks the system by removing unique time fingerprints. However, on gigabit links and under extremely high network load, this can theoretically cause a minor reduction in throughput because the kernel loses access to PAWS (Protect Against Wrapped Sequence numbers). For a secure, isolated host, this compromise is fully justified and necessary.

To apply all added network stack and kernel parameters immediately without rebooting the system, we execute:

**3.** We reload all system kernel configuration files without restarting the PC:
```bash
sudo sysctl --system
```
> [!TIP]
> **Validation Check:** We examine the command output carefully. At the very end of the parameter application list, we should see lines from our created `99-security-hardening.conf` file successfully overriding default values from prior files.

#### Blocking Rare Network Protocols and Legacy Filesystems:

We block the kernel from loading rare network protocols and unused legacy filesystems to eliminate attack vectors exploiting vulnerabilities in their binary modules:

**1**. We open the kernel module blacklist configuration file created earlier:
```bash
sudo nano /etc/modprobe.d/blacklist-hardening.conf
```

**2**. We insert the following configuration lines:
```ini
blacklist dccp
blacklist sctp
blacklist rds
blacklist tipc
blacklist hfs
blacklist hfsplus
blacklist jffs2
blacklist freevxfs
blacklist cramfs
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**3.** We update the initial RAM filesystem image to embed our new configuration into the early boot stage:
```bash
sudo update-initramfs -u -k all
```

#### Filesystem Access Control Hardening:

By default in Ubuntu distributions, newly created files receive a permission mask of `UMASK 022`. This allows other unprivileged system users (as well as potentially compromised background system daemons) to freely read new files. We modify this global policy to make it strictly restrictive:

**1.** We open the global user account parameters configuration file:
```bash
sudo nano /etc/login.defs
```

Inside the file, we locate the `UMASK 022` and `USERGROUPS_ENAB yes` entries and forcibly change their values to `UMASK 077` and `USERGROUPS_ENAB no`. If the `UMASK 022` line is absent, we append `UMASK 077` to the end of the file.

To save changes in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

This guarantees that any new files or directories created by programs or users in the future will be accessible strictly by their owner by default (`600` permissions for files and `700` for directories).

Next, we restrict access to our current home directory from third-party inspection:

**2.** We set strict access permissions on our personal home folder:
```bash
chmod 0700 /home/$USER
```

**3.** We fix permissions for custom sudoers rule directories:
```bash
sudo chmod 750 /etc/sudoers.d && sudo chmod 640 /etc/sudoers.d/* 2>/dev/null || true
```

#### Securely Mounting Shared Memory:

We now configure secure mounting options for virtual shared memory (`shared memory`), which is frequently targeted by attackers for executing fileless malware:

**1.** We open the host filesystem mount table:
```bash
sudo nano /etc/fstab
```

> [!WARNING]
> Applying the `noexec` option to the `/dev/shm` shared memory partition is a classic security recommendation to prevent execution of malicious code directly from RAM. However, in modern distributions, this memory region is vital for web browsers (Firefox, Chromium), which rely on it for process IPC interactions and fast UI rendering.
> 
> Enforcing `noexec` on `/dev/shm` causes Chromium-based browsers to crash immediately upon launch with an *"Aw, Snap!"* error. Firefox will open and allow browsing simple web pages, but its internal tab sandbox isolation mechanisms will drop into restricted mode. Complex web content—such as hardware-accelerated video streams, WebAssembly (WASM), or WebGL graphics—will trigger tab crashes.
> 
> Reverting to the outdated **Xorg (X11)** display server to bypass this issue is not recommended. While Xorg operates alongside `noexec`, its legacy architecture completely lacks window isolation. Any unprivileged application running under Xorg can log keystrokes (keylogging) across other windows, capture screenshots, and simulate input, undermining overall host security.

If full work with media content or local LLMs is planned on the target PC, we use **Option 2A** with `rw,nosuid,nodev` flags. Code execution security should be addressed at higher layers via AppArmor profiles, container isolation, and strict execution controls.

We navigate to the end of the file and append one of the chosen configuration lines:

**Balanced Mode (Recommended for Daily Desktop Use):**

**2A.** This option maintains full stability for modern web browsers while rendering streaming video or executing WebAssembly scripts, preserving internal Inter-Process Communication (IPC). The system remains protected against mounting arbitrary block devices and UID/GID spoofing:
```ini
tmpfs /dev/shm tmpfs rw,nosuid,nodev 0 0
```

**Paranoid Mode (Maximum Isolation):**

**2B.** Suitable for CLI servers or Desktop systems running strictly constrained workloads (terminal workflows, text editors, local administration, Docker/VMware environments) with no need for heavy dynamic web content. The `noexec` flag blocks code execution from memory, neutralizing fileless malware vectors:
```ini
tmpfs /dev/shm tmpfs defaults,noexec,nosuid,nodev 0 0
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

> [!NOTE]
> Unlike Chromium-based browsers that crash instantly at startup under `noexec`, Firefox will launch and function across basic websites. However, processing complex content will trigger tab failures when rendering WebAssembly (WASM) or WebGL graphics, forcing internal sandbox isolation mechanisms into a fallback mode.

#### Configuring Wi-Fi to Default Off on Boot:

To guarantee wireless network interfaces do not transmit hidden probes at boot, we block them via system daemons. This prevents probe request leaks and accidental exposure of the factory MAC address in public spaces:

**1.** We open the service configuration file in `nano`:
```bash
sudo nano /etc/systemd/system/rfkill-block-early.service
```
**2.** We insert the blocking parameters:
```ini
[Unit]
Description=Block WiFi radio at kernel level before NetworkManager starts
DefaultDependencies=no
Before=NetworkManager.service network-pre.target
Wants=network-pre.target

[Service]
Type=oneshot
ExecStart=/usr/sbin/rfkill block wifi
ExecStart=/usr/sbin/rfkill block wwan
RemainAfterExit=yes

[Install]
WantedBy=sysinit.target
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**3.** We create a synchronization unit for NetworkManager:
```bash
sudo nano /etc/systemd/system/wifi-off.service
```

**4.** We define the following rules:
```ini
[Unit]
Description=Keep NM WiFi/WWAN state disabled after it starts
After=NetworkManager.service
Wants=NetworkManager.service

[Service]
Type=oneshot
ExecStart=/usr/bin/nmcli radio wifi off
ExecStart=/usr/bin/nmcli radio wwan off
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**5.** We reload systemd daemons:
```bash
sudo systemctl daemon-reload
```

**6.** We enable both early RfKill execution and Wi-Fi disabling units:
```bash
sudo systemctl enable rfkill-block-early.service && sudo systemctl enable wifi-off.service
```

**7.** We reboot the system:
```bash
sudo systemctl reboot -i
```

The system will preserve this state in kernel configurations, ensuring radio modules remain blocked in RFkill by default during subsequent boots.

> [!WARNING]
> This configuration addresses 99.9% of practical operational scenarios, reducing risk to a negligible window not exploitable by standard software.
> The only method guaranteeing zero leakage risk is cutting physical power to the radio. This is achieved via BIOS/UEFI settings (Hardware Disable) or physical hardware switches on legacy hardware. Keypad combinations like Fn+F2, Fn+F5, or Fn+F8 trigger software signals via ACPI events captured by the kernel (visible via `sudo journalctl -f`), after which the OS disables the transmitter programmatically. If a system is compromised at the rootkit level, software locks can be bypassed.

#### Cutting Off Video Streams and Audio Recording:

Physical camera covers protect against visual surveillance, but built-in microphones can continue recording ambient room audio in the background.

**1.** We open our module hardening configuration file:
```bash
sudo nano /etc/modprobe.d/blacklist-hardening.conf
```

**2.** We block kernel drivers for USB video class devices (UVC) and Intel/Realtek sound subsystems:
```ini
blacklist uvcvideo
install uvcvideo /bin/true
blacklist snd_hda_intel
blacklist snd_hda_codec_realtek
install snd_hda_intel /bin/true
install snd_hda_codec_realtek /bin/true
```
To save the configuration in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**3.** We apply changes by rebuilding the initramfs boot image:
```bash
sudo update-initramfs -u -k all
```

> [!NOTE]
> The `uvcvideo` module handles integrated webcams, while `snd_hda_intel` and `snd_hda_codec_realtek` initialize sound cards and microphones. The host is now functionally isolated from audio and video capture within the OS.

**4.** If speakers and microphones are required for recording voice notes, working with media, or watching video, we adjust the configuration file accordingly. We keep the webcam blocked while commenting out audio chip entries using `# ` (a hash followed by a space) so the kernel initializes speakers and microphones:
```ini
blacklist uvcvideo
install uvcvideo /bin/true
# blacklist snd_hda_intel
# blacklist snd_hda_codec_realtek
# install snd_hda_intel /bin/true
# install snd_hda_codec_realtek /bin/true
```
To save changes in `nano`, we press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**5**. We rebuild the early boot image to commit the perimeter updates:
```bash
sudo update-initramfs -u -k all
```

> [!IMPORTANT]
> Microphones should not remain active continuously. To toggle input quickly, most laptops feature dedicated key combinations (typically Fn+F4 with a struck-through microphone icon). If unavailable, use desktop controls: open **Settings**, navigate to **Sound**, and under **Input**, click the microphone icon beside **Input Volume** to mute it. Clicking it again restores input.

#### Removing Printing Services and Local Network Discovery Services:

Next, we disable the `avahi-daemon` background service. This daemon automatically discovers local network resources via mDNS, broadcasting the host name as `hostname.local` over open UDP port 5353 and TCP port 32768. Active open ports on public networks expose devices to reconnaissance and targeting:

**1.** We remove Avahi completely, purging residual configuration files:
```bash
sudo apt purge avahi-daemon -y && sudo apt autoremove -y
```

Next, we disable and remove `cups`, which manages background discovery of network printers and print queues. Unless printing capability is explicitly required, this subsystem should be purged:

**2.** We stop and disable the printer discovery service:
```bash
sudo systemctl disable --now cups-browsed
```

**3.** We remove CUPS daemons and printing packages:
```bash
sudo apt purge cups cups-daemon cups-browsed hplip hplip-data -y
```

**4.** We clean up orphaned dependencies:
```bash
sudo apt autoremove --purge -y
```

**5.** We enforce desktop print subsystem lockdown via GNOME settings. This prevents background device search threads, saves RAM, and blocks multicast requests directed to `239.255.255.250:3702`:
```bash
gsettings set org.gnome.desktop.lockdown disable-printing true
```

**6.** We disable multicast on the network interface level to prevent kernel IGMP broadcasts to `224.0.0.22` (replace `enp0s1` with your interface name):
```bash
sudo ip link set dev enp0s1 multicast off
```

#### Masking Geolocation and Timezone:

We purge the `Geoclue` location service to prevent background geographical tracking:

**1.** We stop and mask the geolocation service, blocking initialization via D-Bus:
```bash
sudo systemctl stop geoclue.service && sudo systemctl mask geoclue.service
```

Finally, we adjust system clocks to a neutral timezone to eliminate regional digital footprints:

**2.** We set system time to UTC:
```bash
sudo timedatectl set-timezone UTC
```

We confirm timezone application:

**3.** We display system clock status:
```bash
timedatectl
```
The output should explicitly confirm `Time zone: UTC (UTC, +0000)`.

Before concluding, verify that the host is protected against remote SSH port scanning and unauthorized connection attempts.

<br>

## Configuring Repositories and System Updates

Starting with version 24.04, `/etc/apt/sources.list` has completely migrated to `/etc/apt/sources.list.d/ubuntu.sources`. In Ubuntu 26.04, the graphical "Software & Updates" application is absent, so we will utilize the console verification method.

**1.** We open the system update repository configuration file using the `nano` text editor:
```bash
sudo nano /etc/apt/sources.list.d/ubuntu.sources
```

**2.** We edit the configuration by removing the `multiverse` and `restricted` component branches:
```ini
Types: deb
URIs: [http://archive.ubuntu.com/ubuntu/](http://archive.ubuntu.com/ubuntu/)
Suites: resolute resolute-updates resolute-backports
Components: main universe
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: [http://security.ubuntu.com/ubuntu/](http://security.ubuntu.com/ubuntu/)
Suites: resolute-security
Components: main universe
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

For Ubuntu 24.04, it is still possible to use the GUI. Therefore, we can configure repositories via the graphical menu.

We navigate to the **"Show Apps"** menu, open **"Software & Updates"**, and inside the **"Ubuntu Software"** tab (*Downloadable from the Internet*), we uncheck **"Software restricted by copyright or legal issues (multiverse)"** and, if we are **not using** an NVIDIA/AMD graphics card, **"Proprietary drivers for devices (restricted)"**. From an information security perspective, these repositories are not open-source, and only their developers know what proprietary code might be covertly bundled inside.

To significantly increase host privacy, under the **"Download from:"** field, we recommend selecting **"Main server"**. This completely eliminates potential geographic deanonymization resulting from update requests sent to regional mirrors and protects against traffic analysis by local ISPs.

We click **"Close"**, and then in the pop-up dialog box, we select **"Reload"** so the operating system fully refreshes the local package cache. With this optimization, basic graphical security configuration is successfully completed!

<br>

#### Updating the System:

Now that the initial operating system security configuration is complete, it is time to perform a full system update. It is time to connect to a physical network: we plug in an Ethernet cable or enable the Wi-Fi adapter (although it is strongly recommended to completely abandon wireless networks wherever technically possible in favor of a classic wired connection).

> [!WARNING]
> **If we use a VPN!** Since a strict Kill Switch was configured in the UFW firewall in the previous chapter, the internet on the host will not work immediately after connecting the cable or Wi-Fi. We must forcibly establish an encrypted VPN connection; otherwise, the firewall will block absolutely all outgoing packets.
> 
> We can activate the tunnel in two ways:
> 
> * **Graphical method (simplest):** We click on the system status menu in the upper right corner of the screen (the GNOME panel containing the battery, sound, and network icons). In the drop-down menu, we select **"Wired"** and connect to the network, and then we select **"VPN"** and click to connect as well.
> * **Via terminal (if the GUI throws an error):** We open the console and forcibly bring up the tunnel directly via the OpenVPN binary using the following command:
> ```bash
> sudo openvpn --config /path_to_file/profile.ovpn
> ```

**1.** We update the local repository index, and then download and install fresh security patches and system module updates:
```bash
sudo apt update && sudo apt upgrade --with-new-pkgs -y
```

> [!NOTE]
> Message: `Summary: Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading:` number of uninstalled packages (for example, 5)
> 
> Most likely, when running `apt list --upgradable`, the terminal will display: `Not upgrading yet due to phasing`. This means the update is distributed in stages (phased update). This is standard Ubuntu functionality, not a package manager error. **For test systems**, the update can be forcibly installed:
> 
> ```bash
> sudo apt -o APT::Get::Always-Include-Phased-Updates=true full-upgrade
> ```

**2.** We completely clean the operating system of old unused packages, residual dependencies, and remove all downloaded program caches from the disk to save space:
```bash
sudo apt autoremove --purge -y && sudo apt clean
```

**3.** We reboot the computer to finalize the application of all kernel updates and background system services:
```bash
sudo systemctl reboot -i
```

#### Deploying the NVIDIA Graphics Stack in Isolated Mode:

This subsection is necessary exclusively in two cases: when deploying a local AI lab to work with neural networks (LM Studio) or if hardware graphics acceleration is critically required for heavy workloads. When the system is built purely for text-based OPSEC (confidential email, secure messengers, basic browsing), we skip this step.

If the hardware power of the graphics card is indeed required, we implement a temporary gateway tactic: we activate the repository, fetch the components, lock their versions at the kernel level, and then completely remove this branch from the system. As a result, the graphics stack will operate at full capacity, while the operating system returns to a state of complete "packet silence".

**1.** We temporarily activate the official proprietary component repository `restricted` and update the package indices:
```bash
sudo add-apt-repository restricted -y && sudo apt update
```

**2.** We run the utility to automatically install the current stable driver branch for our kernel:
```bash
sudo ubuntu-drivers install
```
If in Ubuntu 24.04 the console displays a message stating that all drivers are already installed (`All the available drivers are already installed.`), we launch **"Software & Updates"** and navigate to the **"Additional Drivers"** tab. There, we must select the driver currently relevant, for example, *Using NVIDIA driver metapackage from nvidia-driver-580 (proprietary)*. After that, we click **"Apply Changes"**, and once the driver installation finishes, we click **"Restart..."**.

Upon rebooting in Ubuntu 24.04, we perform a mandatory verification on the user password login screen: in the lower right corner, we check the gear icon status. If it displays Ubuntu on Xorg instead of Wayland, we switch it back to secure Wayland. After that, we enter the password and log into the system.

**3.** We freeze the current versions of all installed NVIDIA packages in the system. This prevents the `apt` manager from modifying them, completely eliminating the risk of breaking the graphics session after removing the repository:
```bash
dpkg -l | grep nvidia | cut -d' ' -f3 | xargs -r sudo apt-mark hold
```

**4.** Now we completely remove the `restricted` branch from the system:
```bash
sudo add-apt-repository --remove restricted -y && sudo apt update
```

In the future, if we need to update the drivers, we replace `hold` with `unhold` and re-enable the `restricted` repository.

> [!NOTE]
> By applying the `apt-mark hold` command, we sealed the driver in its current stable state. Now we can rest assured: routine distribution updates will no longer affect or break our graphics stack, and complete removal of the `restricted` repository guarantees that the system will never connect to third-party proprietary servers again!

**5.** We send the host machine to a mandatory reboot to initialize the locked driver modules at the Linux kernel level:
```bash
sudo systemctl reboot -i
```

> [!IMPORTANT]
> **Only for Ubuntu 24.04**. The Wayland display server provides window isolation at the display server level, completely blocking viruses and malware from keylogging and clipboard spying. However, the Ubuntu display manager (`gdm3`), at the slightest suspicion of instability in fresh NVIDIA drivers or the Ubuntu 24.04 kernel, has a hidden trigger for a forced and silent fallback to the insecure X11 (Xorg) protocol.
> 
> If after another reboot it drops to X11 during the check below, we use an alternative method via GRUB and a dummy override file.
> 
> **Without enabling the internet**, immediately after rebooting, we open the host terminal and check the current state of the graphical environment:
> ```bash
> echo $XDG_SESSION_TYPE
> ```
> * If the command returns `wayland`, the perimeter is relatively secure, and we can proceed further with the chapter.
> * If `x11` lights up in the console, the display server is blocked by the system. It is strictly forbidden to continue configuration until the Wayland contour is forcibly restored!
>
> **Algorithm for forced Wayland resuscitation in Ubuntu 24.04 for NVIDIA graphics cards:**
> 
> **1.** We open the system bootloader configuration file in a text editor:
> ```bash
> sudo nano /etc/default/grub
> ```
> **2.** We navigate to the line `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` and append the KMS kernel mode setting flag `nvidia-drm.modeset=1` inside the quotes:
> ```ini
> GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvidia-drm.modeset=1"
> ```
> We save the configuration file with key combination **"Ctrl + O"** → **"Enter"**, then **"Ctrl + X"** to exit back to the console.
> 
> **3.** We write the changes to the boot sector of the host machine:
> ```bash
> sudo update-grub
> ```
> **4.** We blind the Ubuntu system udev blocker, which forcibly disables Wayland when proprietary drivers are detected. To do this, we override its rules with an empty dummy file:
> ```bash
> sudo ln -sf /dev/null /etc/udev/rules.d/61-gdm.rules
> ```
> **5.** We send the host machine to a mandatory reboot:
> ```bash
> sudo reboot
> ```

**Chapter Asset:** *_assets\images\6_software_updater*

## Terminal Environments in Ubuntu:

#### Replacing GNOME Terminal and Ptyxis with Ghostty

We install the highly discussed Ghostty terminal, written in the Zig programming language. The author of the project is Mitchell Hashimoto, a well-known figure in IT circles.

**Installation for Ubuntu 24.04 LTS Noble Numbat users:**

**1.** Just in case, we check the removal in simulation mode to ensure we do not touch critical packages:
```bash
apt -s purge gnome-terminal
```

**2.** We install Ghostty:
```bash
sudo add-apt-repository ppa:maksberg/ghostty-ubuntu && sudo apt update && sudo apt install ghostty
```

**3.** We remove GNOME Terminal:
```bash
sudo apt purge gnome-terminal
```

**4.** We perform a simulation of removing residual packages:
```bash
apt -s autoremove
```

If no extraneous system packages are detected, we proceed with the final cleanup.

**5.** We remove residual Terminal leftovers:
```bash
sudo apt autoremove
```

* **Installation for Ubuntu 26.04 LTS Resolute Raccoon users:**

**1.** Just in case, we check the removal in simulation mode to ensure we do not touch critical packages:
```bash
apt -s purge ptyxis
```

Most likely, the command will flag `apport-gtk*` and `ptyxis*` for removal, which suits us completely. The `apport-gtk*` utility is responsible for sending crash reports in Ubuntu. When a program crashes, a window appears reporting an abnormal application termination and offering to send a report, so we remove it without much regret.

**2.** We install Ghostty:
```bash
sudo apt update && sudo apt install ghostty
```

All further actions are executed directly inside the Ghostty window.

**3.** We remove Ptyxis:
```bash
sudo apt purge ptyxis
```

**4.** We perform a simulation of removing residual packages:
```bash
apt -s autoremove
```

If no extraneous system packages are detected, we proceed with the final cleanup.

**5.** We remove residual Ptyxis leftovers:
```bash
sudo apt autoremove
```

**Ghostty Configuration Option for Ubuntu 24.04/26.04:**

We can edit the configuration inside the Ghostty settings via the **burger menu** by selecting **Open Configuration**. In the opened `config.ghostty` file, we insert the following lines:

```ini
# Font family and font size
font-family = "Ubuntu Mono Semi-Bold"
font-size = 16

# Font color (hacker green primary text)
foreground = #00ff00

# Window background color (deep dark blue)
background = #0a1128

# Window opacity (0.0 completely transparent, 1.0 fully opaque)
background-opacity = 0.95

# Background blur radius behind the window (0 disabled)
background-blur-radius = 20

# Window dimensions in characters and lines
window-width = 96
window-height = 24
```

#### Optional! Ubuntu 26.04 — Restoring Gnome Terminal and Removing Ptyxis:

Once again, I repeat that **I do not recommend** this option, as it carries certain security risks and serves purely as an alternative choice. If suspicious code that turns out to be malicious is accidentally executed inside it, the entire system will be compromised with nearly 100% probability. Therefore, in such cases, strict usage of the `firejail` sandbox is recommended.

**1.** Just in case, we check the removal in simulation mode to ensure we do not touch critical packages:
```bash
apt -s purge ptyxis
```

Most likely, the command will flag `apport-gtk*` and `ptyxis*` for removal, which suits us completely. The `apport-gtk*` utility is responsible for sending crash reports in Ubuntu. When a program crashes, a window appears reporting an abnormal application termination and offering to send a report, so we remove it without much regret.

**2.** We install GNOME Terminal:
```bash
sudo apt install gnome-terminal
```

All further actions are executed directly inside the Terminal window.

**3.** We remove Ptyxis:
```bash
sudo apt purge ptyxis
```

**4.** We perform a simulation of removing residual packages:
```bash
apt -s autoremove
```

If no extraneous system packages are detected, we proceed with the final cleanup.

**5.** We remove residual Ptyxis leftovers:
```bash
sudo apt autoremove
```

We verify the package list before actual deletion. If system components whose purpose is unknown to us are present among them, we abort the operation; otherwise, we execute the full removal command in the terminal — `sudo apt autoremove`.

**6.** We remove residual Ptyxis leftovers:
```bash
sudo apt autoremove
```

<br>

## Removing and Blocking Snap and Telemetry

#### Purging Snap:

Now we proceed to completely purge the operating system of the Snapd subsystem, which is capable of silently downloading and updating proprietary packages in bypass of the host's established privacy settings:

**1.** We completely cut out the `Snapd` daemon and its associated structures from the operating system:
```bash
sudo apt purge snapd -y
```

To prevent the package manager from accidentally installing this daemon back via dependencies in the future when updating application software, we lock its installation via APT Pinning hard priority rules:

**2.** We create a dedicated permanent lock configuration file:
```bash
sudo nano /etc/apt/preferences.d/nosnap.pref
```

**3.** In the empty file that opens, we insert the following lines:
```ini
Package: snapd
Pin: release a=*
Pin-Priority: -10
```

To save the configuration in the `nano` editor, we press **`Ctrl + O`** -> **`Enter`**, then **`Ctrl + X`** to exit back to the console.

> [!IMPORTANT]
> First, in newer Ubuntu versions, the standard graphical app store *App Center* relies entirely on the Snap backend. After removing the daemon, it will physically cease to launch. For our system, this is a huge plus, as we completely eliminate an unnecessary attack vector, while installing all required legitimate software via the clean console package manager `apt`. If we ever urgently need a graphical manager for manual installation of `.deb` packages, we can deploy the classic Synaptic utility with the command: `sudo apt install synaptic`.
> 
> Second, the standard Firefox browser in modern Ubuntu is now provided by Canonical strictly as a Snap container. The `purge snapd` command will completely remove Firefox from the operating system! To avoid being cut off from the outside world, before cutting out Snap, we must install a clean official `.deb` version of Firefox from the developer repository (Mozilla PPA). We will do this immediately once we finish initial host kernel isolation and apply the first system updates!

#### Ripping Out Canonical Telemetry:

It is time to apply our comprehensive automated Bash script for the total removal of built-in telemetry and the prevention of latent technical metrics transmission to Canonical servers. We create this script in the user Downloads folder:

**1.** We navigate to the active user's Downloads folder:
```bash
cd ~/Downloads
```

**2.** We initialize the creation of an empty script file:
```bash
touch telemetryoff.sh
```

**3.** We open the script using the `nano` editor:
```bash
nano telemetryoff.sh
```

> [!WARNING]
> It is absolutely not recommended to copy automated script code directly from e-book interfaces (PDF/EPUB/FB2) to avoid hidden encoding errors, space substitution, and accidental insertion of invisible formatting control characters! Type the lines or transfer them using plain text editors. Always carefully inspect the code!

**4.** We open the created file via the nano text editor and insert the following monolithic telemetry cleanup script code:
```bash
#!/bin/bash
# Ubuntu 24.04/26.04 Telemetry & Pro Hardening Script (Ultimate Edition)

# Designed for Ubuntu Desktop and its flavors (Xubuntu, Lubuntu)

# Superuser privileges check

if [ "$EUID" -ne 0 ]; then
 echo "[-] Error: Please run this script as root: sudo $0"
 exit 1
fi

echo "[+] Aggressively stopping and masking telemetry services..."
systemctl stop apport.service whoopsie.service ubuntu-advantage.service pro-client.service 2>/dev/null
systemctl disable apport.service whoopsie.service ubuntu-advantage.service pro-client.service 2>/dev/null

systemctl mask apport.service whoopsie.service ubuntu-advantage.service pro-client.service 2>/dev/null

echo "[+] Disabling kernel crash reporting..."

if [ -f /etc/default/apport ]; then
 sed -i 's/enabled=1/enabled=0/g' /etc/default/apport
fi

echo "[+] Removing telemetry and advertising packages safely (preserving desktop GUI)..."
# We lock the desktop environment in "manually installed" status so apt does not remove the desktop
apt-mark manual ubuntu-desktop xubuntu-desktop lubuntu-desktop gdm3 lightdm 2>/dev/null

# We remove classic telemetry software and the intrusive Ubuntu Pro/ESM client
apt purge ubuntu-report whoopsie popularity-contest ubuntu-pro-client ubuntu-advantage-tools -y

# Safe removal of apport without cascading GUI removal

apt purge apport -y --allow-remove-essential 2>/dev/null || apt remove apport -y

# We clean system trigger caches for ESM updates that communicated with Canonical

rm -f /etc/apt/apt.conf.d/20ubuntu-pro-esm 2>/dev/null

# We automatically clean orphaned dependencies while verifying GUI integrity
apt autoremove -y

echo "[+] Configuring APT Pinning (Permanent Lock)..."
cat << 'EOF' > /etc/apt/preferences.d/no-telemetry.pref
Package: ubuntu-report
Pin: release a=*
Pin-Priority: -10

Package: whoopsie
Pin: release a=*
Pin-Priority: -10

Package: apport
Pin: release a=*
Pin-Priority: -10

Package: popularity-contest
Pin: release a=*
Pin-Priority: -10

Package: ubuntu-pro-client
Pin: release a=*
Pin-Priority: -10

Package: ubuntu-advantage-tools
Pin: release a=*
Pin-Priority: -10
EOF

echo "[+] Telemetry and Ubuntu Pro hardening completed successfully!"
```

To save the file in the nano editor, we press **`Ctrl + O`** -> **`Enter`**, then **`Ctrl + X`** to exit back to the console.

**5.** We set strict file access permissions: reading, editing, and executing the script will be available exclusively to its direct owner:
```bash
chmod 0700 telemetryoff.sh
```

**6.** We run the script as a superuser and wait for the host optimization to complete successfully. After execution, the script can be removed:
```bash
sudo ./telemetryoff.sh
```

**7.** We reboot the system:
```bash
sudo reboot
```

> [!TIP]
> If we want to run the script immediately without prior permission modification via `chmod +x`, we can invoke the Bash interpreter directly:
> ```bash
> sudo bash telemetryoff.sh
> ```
> *Note: if the file was edited in Windows, we must first sanitize line endings using `sed -i 's/\r$//' telemetryoff.sh`.*

After execution, the `telemetryoff.sh` script can be deleted from the `Downloads` folder either via the Trash or using `rm ~/Downloads/telemetryoff.sh`.

**8.** We clean up residual leftovers of the kernel crash reporting tool:
```bash
sudo systemctl stop apport.service && sudo systemctl disable --now kerneloops.service
```

#### Purging the Background Firmware Tracker fwupd:

Even after completely cleaning Canonical system telemetry, the hidden `fwupd` (Firmware Updater) daemon remains active by default in the operating system. Every time a network connection is established, it silently sends requests to the global CDN server `cdn.fwupd.org`, transmitting unique hardware UUID identifiers of the motherboard, CPU, and NVMe drives under the pretext of checking for BIOS/UEFI updates.

We decline uncontrolled background leaks of host hardware hashes. All critical low-level firmware updates will be performed strictly manually and offline, while the daemon's network activity is completely cut off at the operating system kernel level.

**1.** We stop active services and automatic update timers:
```bash
sudo systemctl stop fwupd fwupd-refresh.service fwupd-refresh.timer
```

**2.** We forcibly mask (freeze) unit configuration files in `systemd`. This strictly blocks any possibility of accidental, background, or forced restarting by the operating system during the installation of other packages:
```bash
sudo systemctl mask fwupd fwupd-refresh.service fwupd-refresh.timer
```

> [!NOTE]
> After applying masking, the background `fwupd` process is completely unloaded from RAM and loses the ability to generate network sockets on its own. Hidden connections to external `cdn.fwupd.org` servers are permanently terminated.

**Chapter Asset:** *_assets\images\7_systemcut_telemetry*

<br>

## Installing Security Utilities: libpam-tmpdir, debsums, and the Btop System Monitor

#### The libpam-tmpdir Security Utility:

To eliminate one of the oldest architectural vulnerabilities in Linux, we need to isolate shared temporary directories to which all processes in the system have access by default. We integrate a dedicated module into the authentication kernel, which will create a personal, protected memory pocket for each application.

**1.** We install the low-level application temporary directory isolation module (`libpam-tmpdir`):
```bash
sudo apt install libpam-tmpdir -y
```

> [!NOTE]
> By default in Linux, absolutely all launched programs, messengers, system daemons, and scripts use the shared system folder `/tmp` to store their temporary data. From a security standpoint, this is a massive open corridor. Any malware, hidden tracker, or unprivileged process inside the system can inspect the contents of `/tmp`, spy on temporary files of neighboring applications, attempt to tamper with them, or execute a *Symlink Attack* (substitution via symbolic links).

#### The debsums Utility:

The `debsums` utility is a tool for those who like to keep a finger on the pulse of the system and verify every single cog. The name stands for Debian checksums.

When we install any application via the package manager (`apt`), a special file containing reference checksums (typically MD5 or SHA) for every file delivered by that package is downloaded into the system alongside the program itself. Next, `debsums` takes these reference values and begins comparing them with the actual files residing on our hard drive. If anyone (or any virus/rootkit) covertly modifies a system file (for example, replacing the system utility `/bin/ls` or `/usr/bin/ssh` with an infected version), the checksum will fail to match. The utility will immediately return a `FAILED` status.

**1.** We install the checksum verification utility:
```bash
sudo apt install debsums -y
```

**2.** We run a global verification across all system packages:
```bash
sudo debsums -s
```

#### Btop: A Streamlined Resource Monitor:

A modern console task manager designed to replace the standard `top` system monitor. The utility features a far more user-friendly, informative, and interactive graphical interface deployed right inside the terminal.

**1.** We install the utility from the official repository:
```bash
sudo apt install btop -y
```

**2.** We launch the resource monitor:
```bash
btop
```

The help menu for shortcut keys inside the utility is brought up by pressing **H** (*Help*). A quick exit from the program is performed by pressing **Q** (*Quit*).

<br>

#### Monitoring Network Ports and Active Connections:

Continuous control over network activity is a core operational hygiene skill. We must clearly understand exactly which internal processes open sockets and where network traffic is currently being transmitted.

**1.** We run an audit of open network ports. The command clearly shows which background services and daemons are currently "listening" on ports on the machine in anticipation of external connections:
```bash
sudo ss -tupnl
```

**2.** We output an expanded table of current network activity. The command displays absolutely all active network sessions, including established outgoing connections (*ESTABLISHED*). With its help, we can instantly determine which remote IP addresses traffic is heading to right now:
```bash
sudo ss -tupna
```

The `ss` utility provides an instant static snapshot of network activity. However, advanced malware or hidden backdoors can act more subtly: they open a network connection for fractions of a second, exfiltrate an encrypted payload of sensitive data, and instantly close the port. Because of this, catching them manually by regularly running a console command is practically impossible.

For continuous security monitoring of network sockets in real time, it is recommended to combine the capabilities of `ss` with the built-in system automation utility `watch`, adding the change-highlighting flag `-d`:

**3.** We launch continuous real-time socket monitoring:
```bash
sudo watch -n 1 -d 'ss -tupna'
```

This combination will automatically refresh the terminal screen every second (`-n 1`), while the `-d` flag will physically highlight on the display any new, suddenly opening outgoing or incoming network connections, allowing us to visually capture even the shortest background network activity.

To return back to the console, we press **`Ctrl + Z`**.

<br>

## CCreating Golden Restore Points: Deploying and Configuring Timeshift

#### Introduction:

We have completed the initial kernel hardening, permission isolation, and strict firewall configuration with flying colors. Our system now represents a clean, secure, but currently fully isolated host from the outside world. Before we initiate our first major connection to the network and pull down system updates, we must freeze this "sterile" state.

Why is this necessary? Engineering security teaches us to prepare for the worst-case scenario: when installing large update packages, upgrading the kernel, or subsequently building heavy virtual containers, something might go wrong. To avoid spending hours reinstalling the OS from scratch and re-configuring all our manual hardening steps in the event of an emergency, we will create instant system snapshots with the ability to roll back in a few clicks.

The powerful system utility `Timeshift` will help us achieve this. It operates on the principle of backup restore points, protecting system files and settings exclusively while leaving personal data in the home directory untouched (which completely rules out the loss of working documents during a rollback).

#### Timeshift Mechanics in an Encrypted Environment (LUKS + GRUB):

Since during the installation phase we deployed the system on top of an encrypted LVM pool and protected the `GRUB` bootloader with a password, we must observe two strict security rules:

1. **No third-party software from Live-USB:** We will configure `Timeshift` and execute point rollbacks strictly from within our booted, decrypted operating system. Using third-party emergency flash drives is unacceptable in our OPSEC concept, as they operate by bypassing our authentication mechanisms.
2. **Boot sector control:** Our encrypted drive and password-protected `GRUB` will remain completely safe, as `Timeshift` snapshots copy the state of files inside logical volumes without touching the low-level LUKS encryption structure. However, during restoration, the system may rewrite the `GRUB` menu configuration, so our kernel editing password will remain active and will not be reset.

#### Securely Installing Timeshift:

We sequentially execute commands in the terminal as the superuser. We bring up our encrypted tunnel, after which we initialize the installation from the official Ubuntu repository:

**1.** We enter interactive superuser (root) mode:
```bash
sudo -i
```

**2.** We immediately update the local package index and install a clean .deb version of Timeshift directly over a secure connection:
```bash
apt update && apt install timeshift -y
```

**3.** We exit superuser mode back into the regular user session:
```bash
exit
```

The utility has been successfully deployed on board the host, while our protective network perimeter did not remain open to the outside world for even a second.

#### Initial Configuration and Creating Snapshot #1 (Sterile Baseline):

Launching `Timeshift` requires superuser privileges.

**4.** We launch the program:
```bash
sudo timeshift-gtk
```

We can use the graphical interface of the application by launching it via the **"Show Apps"** menu (the system will prompt for the administrator password); however, if we begin using a Yubikey in the future, we will have to abandon this method in favor of the console interface.

Upon first launch, the Setup Wizard will open. We immediately click **"Finish"** without changing anything.

We navigate to the **"Settings"** section of the program and select:

* **Snapshot Type ("Type"):** Select strictly **"RSYNC"** mode. Since we are using a standard file system on top of LVM encryption, this mode will create reliable copies using system hard links without wasting extra disk space on unmodified files.
* **Storage Location ("Location"):** The system will automatically highlight our system's encrypted LVM partition (e.g., `dm-1` or `dm-0` under our root group name). Select it. Copies will be stored on the same disk inside an isolated system directory `/timeshift`, protected by our root privileges.
* **Schedule Levels ("Schedule"):** Uncheck all boxes for automatic timers **(Daily, Boot, Weekly, Monthly)**. In our operational hygiene paradigm, background daemons must not perform disk operations on their own, create hidden CPU load, or degrade drive lifespan. We will create all snapshots strictly manually, keeping full control over the process.
* **User Folders ("Users"):** This tab configures home directory behavior during a system rollback. By default, for a regular user (`user /home/user`), the parameter is set to **"Exclude All Files"** — leave it unchanged so that the utility does not overwrite our personal databases and passwords. For the root folder (`root /root`), switch the setting to **"Include All Files"**.
* **Directory Filters ("Filters"):** Switch to the adjacent tab. After enabling the administrator folder in the backup in the previous step, make sure that in the global filters list, the line `/root/**` is now highlighted with a green marker (Include). If a duplicate line with an exclusion sign (red marker) is still present there, simply select it with the mouse and click the **"Remove"** button at the bottom of the window. The administrator folder must be backed up and restored alongside the OS kernel. The `home/$USER/**` folder is copied at your discretion.
* **"Misc":** Here, we set the date and time format to our preference.
* Click the **"OK"** button. The initial binding is successfully completed.

Now, in the main application window, click the **"Create"** button. The program will initiate the scanning process and build our first snapshot. In the snapshot comments field *Comments (click to edit)*, make sure to enter: `BUILD_01_STERILE_HARDENING`.

> [!WARNING]
> In **"Settings"**, pay close attention to the **"root /root"** line. By default, exclusion mode is active for it as well. In our security paradigm, this is a vulnerability: if the host is compromised, malicious scripts or backdoors injected by an attacker into the administrator directory would persist in the system after a rollback.
> Forcibly toggle the radio button for the **"root /root"** line to the rightmost position — **"Include All Files"**.

> [!IMPORTANT]
> This is our primary recovery point ("Sterile Benchmark"). It freezes all low-level kernel hardening, ideal `sysctl` parameters, the modified `UMASK 077` mask, and the hard removal of factory Canonical telemetry. All of this is secured before application software, third-party repositories, browsers, and user tools are installed in the system. If anything goes wrong during subsequent customization or software experiments, we can instantly revert to this baseline protected configuration.

#### Ongoing Control Strategy: Creating Snapshot #2 (Pre-Operational):

Now that we have a solid safety net in the form of the first snapshot, we can move forward: applying daily system updates via `apt upgrade`, removing remaining telemetry meta-packages, and restoring a clean `.deb` version of the Firefox browser to the system.

However, before proceeding to the chapter on deep host auditing using the `Lynis` utility and building isolated sandboxes or virtual containers with lightweight Xubuntu/Lubuntu inside VirtualBox, we are obligated to create **Snapshot #2**.

The procedure is identical: before running heavy virtualization software or deep audits, we open `Timeshift` and manually create a second restore point. In the comments, specify: `BUILD_02_BEFORE_LYNIS`.

#### Emergency Rollback Protocol (System Compromised or Broken):

If during experiments with isolated containers or due to an accidental syntax error in low-level configuration files we lose system stability, we execute a safe rollback from within the running operating system:

* Open the Timeshift graphical interface via the menu (**"Show Apps"**).
* Select the required snapshot from the list (for example, the benchmark `BUILD_01_STERILE_HARDENING`).
* Click the **"Restore"** button.
* In the target partition selection window **"Target Devices"**, the program will ask to confirm the mount paths for root (`/`) and the boot partition (`/boot/efi`). Strictly leave the default values: **"Keep on Root Device"**.
* Click **"Next"**. The utility will perform an express change analysis, display a list of files that will be overwritten or removed, and send the host into an automatic reboot.

During rebooting, Timeshift will overwrite modified system files in interactive text mode, restoring them to our benchmark state.

> [!NOTE]
> Please note that thanks to hardware and software LUKS encryption, when the PC boots after a rollback, the system will prompt for our disk master password as usual. The GRUB bootloader will remain securely locked by the hash created earlier, as Timeshift operates exclusively inside the decrypted logical volume and is physically incapable of resetting, wiping, or modifying external disk defense layers.

We are protected on all sides. Moving on to the next operational hygiene stage!

**Chapter Asset:** *_assets\images\8_timeshift*

<br>

## Installing a Clean .deb Release of Firefox and Removing the Snap Stub:

Since we successfully updated the system over a secure VPN connection in the previous step, it is time to restore our main working tool — the Firefox web browser. As we already know, when the Snapd subsystem was completely removed, the standard browser was uninstalled, leaving behind hidden configuration leftovers. The `firefox` package in the standard Ubuntu repository is a mere stub (a transit script) that forcibly reintroduces telemetry and the Snapd daemon back into the system.

Before installing a pure, independent version of the browser directly from the developers at Mozilla Team, we must completely clean out residual junk from the home directory and strictly block automatic package substitution mechanisms.

Sequentially execute the following steps in the terminal as a regular user:

**1.** We completely delete hidden residual directories, cache, and old profiles of the Snap version of the browser in the home folder:
```bash
rm -rf ~/snap/firefox ~/.mozilla/firefox
```

**2.** We import the official PPA repository of the Mozilla development team into the operating system:
```bash
sudo add-apt-repository ppa:mozillateam/ppa -y
```

**3.** The `firefox` package in Ubuntu repositories is a Snap stub by default. To bypass this restriction and force the package manager to pull down a clean binary directly from the Mozilla Team PPA, we create a strict priority configuration file:
```bash
sudo tee /etc/apt/preferences.d/mozilla-firefox <<EOF
Package: firefox*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001

Package: firefox*
Pin: release o=Ubuntu
Pin-Priority: -10
EOF
```
To save the file in the nano editor, we press **`Ctrl + O`** -> **`Enter`**, then **`Ctrl + X`** to exit back to the console.

**4.** We update the local system package index taking into account the newly created priority rules:
```bash
sudo apt update
```

**5.** We launch the installation of a clean, Snap-independent desktop version of Firefox:
```bash
sudo apt install firefox -y
```

> [!IMPORTANT]
> The next configuration step is split into two options depending on the operating system version: **Ubuntu 24.04 LTS Noble Numbat** vs. the newer **Ubuntu 26.04 LTS Resolute Raccoon**. Select and execute only the single command strictly corresponding to your distribution.

* **For Ubuntu 24.04 LTS Noble Numbat users:**
**6a.** We activate a hidden system rule that permits Ubuntu's automatic background update service to download critical security patches for Firefox directly from the Mozilla Team repository:
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:noble";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

* **For Ubuntu 26.04 LTS Resolute Raccoon users:**
**6b.** We activate an analogous system rule for the 26.04 distribution package base:
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:resolute";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

> [!WARNING]
> Without performing step 7a/7b, the browser will update only during a manual call to `apt upgrade`, which significantly increases the risk of remaining unprotected against fresh zero-day (0-day) vulnerabilities.

**7.** We conduct a final verification. If the command outputs the browser version without mentioning Snap, the installation has completed successfully:
```bash
firefox --version
```
> [!IMPORTANT]
> Installing the browser via the official PPA from the Mozilla Team grants us two serious advantages:
>
> **Full compatibility with third-party sandboxes:** The executable binary is now physically located at the classic system path `/usr/bin/firefox`. This allows us to enforce strict Mandatory Access Control via `AppArmor` and isolate it inside a `Firejail` container without any conflicts — something that would be technically impossible with a Snap version locked inside Canonical's proprietary backend.
> **Absence of hidden installer telemetry:** The build is compiled directly from open-source Mozilla code, contains no Canonical transit scripts, and does not attempt to activate background telemetry services.

<br>

## IInstalling and Hardening Privacy Settings in Mozilla Firefox

#### Preparing the System for Tuning:

The built-in Firefox web browser requires strict hardening. We installed it exclusively as a clean `.deb` package. Now, we will forcibly shut down Mozilla's hidden internal telemetry, block cross-site tracking, and completely zero out host de-anonymization vectors.

> [!WARNING]
> **Initial browser launch and all configuration steps must occur strictly under full radio silence — WITHOUT internet access!**
> To prevent critical OPSEX scenarios, clicking the Firefox icon while the system is online is strictly forbidden. Upon the very first launch, an unhardened Firefox will instantly spew primary telemetry packets across the network, verify our IP location, and establish connections with Mozilla servers. To eliminate data leaks entirely, we are obligated to temporarily isolate the system.

We can achieve this using the simplest methods available:

* **Graphical method (Simplest):** We click the network connections icon in the system tray and toggle the wired connection (or Wi-Fi) switch to **"Off"**.
* **Console method (For terminal):** We completely kill the operating system's network stack with a single universal command:
```bash
nmcli networking off
```

Now the host is in a completely sterile vacuum. We safely launch Firefox and proceed to step-by-step tuning.

> [!TIP]
> This guide utilizes the ironic author-coined term — "OPSEX".
> It describes a situation where a complex defense architecture loses all effectiveness due to simple human error.
>
> For example, one can meticulously configure an anonymous environment, yet accidentally hit the web through an unhardened browser, or transmit a file without stripping hidden metadata.
>
> OPSEX serves as a reminder that security is defined not only by technical controls, but by everyday user operational hygiene.
> Therefore, it is critical to continuously analyze personal data-handling habits alongside security tools.
>
> *The term OPSEX was originally formulated by the author of this guide (EugeXo) as a concept to describe the human factor in operational security.*

#### Initial GUI Privacy Configuration (Mandatory for Everyone):

We launch the browser and enter the following direct path into the address bar: `about:preferences#privacy`. Sequentially, we tweak the settings:

* **«Enhanced Tracking Protection» Block:** We open the **«Advanced settings»** sub-item and switch the toggle to strict **«Strict»** mode. Then we click **«Reload All Tabs»**. This action automatically activates Dynamic First-Party Isolation (*dFPI*), preventing ad trackers from spying on our movements across the web.
* **«Browsing Data» Block:** We make sure to check **«Clear cookies and site data every time you close Firefox»**.
* **«DNS over HTTPS» Block:** Modern browsers can execute covert background DNS queries. To kill this vector, we scroll down to **«Advanced settings»**, set the provider selection to **«Custom»**, and manually specify the URL of a secure, non-logging DoH server.
* **«Connection and software security» Block:** At the very bottom of the page, we locate **«HTTPS-Only Mode»**, access its additional parameters, and switch the toggle to **«Enable HTTPS-Only Mode in all windows»**. This enforces encryption on any unprotected HTTP traffic.
* **«Search» Section:** We navigate to this section in the left sidebar menu and change the default search engine, replacing Google's telemetry engine with private, non-logging **DuckDuckGo**.
* **«Permissions and data» Section:** We scroll down to **«Firefox Data Collection and Use»** and forcibly uncheck all telemetry options. The browser will no longer send technical reports or stability metrics to Mozilla.

#### Configuring Private DNS Providers (DNS over HTTPS):

We can select any secure, non-logging DoH server from the list below:

> [!NOTE]
> **1. Mullvad DNS (From the creators of Mullvad VPN)**
> A Swedish service focused on radical privacy. They collect no logs and require no email during registration. Their DNS infrastructure is fully self-owned and operates without third-party intermediaries.
> * Clean DNS (No blocking): `https://dns.mullvad.net/dns-query`
> * Ad & Tracker Blocking (Adblock + Trackers): `https://adblock.dns.mullvad.net/dns-query`
> * Maximum Protection (Ads + Trackers + Malicious Sites): `https://base.dns.mullvad.net/dns-query`
>
> **2. Quad9 (Non-profit Cybersecurity Alliance)**
> Built with support from IBM Security and global data protection experts. Based in Switzerland, it operates under strict privacy laws and utilizes Anycast technology for instant query response.
> * Secured (Primary, includes DNSSEC validation): `https://dns.quad9.net/dns-query`
> * Unfiltered (Clean DNS): `https://dns10.quad9.net/dns-query`
>
> **3. Control D (From the creators of Windscribe VPN)**
> One of the best modern services. They strictly refuse to keep logs and use Anycast technology to route requests to the nearest server.
> * Clean DNS (No blocking): `https://freedns.controld.com/p0`
> * Ad, Tracker & Phishing Blocking: `https://freedns.controld.com/p1`
> * Maximum Block (Ads + Malware + New Domains): `https://freedns.controld.com/p2`
>
> **4. NextDNS (Cloud-based Pi-hole alternative)**
> A privacy-first service functioning as a powerful protective shield. Creating a free account allows flexible blocklist customization.
> * Standard Protection (Ads + Trackers + Malware): `https://dns.nextdns.io`
> * Clean DNS (Privacy only, no filters): `https://unfiltered.nextdns.io`
>
> **5. AdGuard DNS (Ad-blocking focused)**
> A battle-tested service from renowned ad-block developers. It strips banners, trackers, and analytical scripts at the DNS request phase.
> * Base Protection (Ads + Trackers): `https://dns.adguard-dns.com/dns-query`
> * Unfiltered (Clean non-logging DNS): `https://unfiltered.adguard-dns.com/dns-query`
>
> **6. Cloudflare (1.1.1.1 — World's Fastest)**
> Operates a massive global network ensuring minimal latency when loading sites. From a privacy perspective, the company promises to purge all request logs within 24 hours.
> * Clean DNS (Ultra-fast): `https://cloudflare-dns.com/dns-query`
> * Malware Protection (Safe Browsing alternative): `https://security.cloudflare-dns.com/dns-query`

#### Hardening Automation: Creating the user.js Configuration File:

To avoid manually entering dozens of radical parameters through the `about:config` interface, we can build a single automated text file named `user.js`. All preferences are declared there using the system format `user_pref("parameter", value);`.

We need to place this file directly into the hidden folder of the currently active Firefox profile in Ubuntu. On every startup, the browser will automatically parse this file and enforce all our hardened preferences. Inside the `about:config` engineering menu, these parameters will be highlighted in bold, locking out accidental manual changes.

To locate the exact profile path, create the `user.js` file there, populate it with configuration payloads, and strictly limit access permissions, execute the following steps in the terminal as a standard user:

**1.** We navigate to the profile directory (in a clean and current `.deb` release of Firefox, the default profile almost always ends with `.default-release`) and create an empty configuration file:
```bash
cd ~/.config/mozilla/firefox/*-release/ && touch user.js
```

> [!NOTE]
> If we choose to write an automation script for multiple deployment targets and want `user.js` guaranteed to land in the active working profile (regardless of its directory name or folder count), we deploy the lower snippet utilizing the `PROFILE_DIR` variable instead.
> ```bash
> PROFILE_DIR=$(awk -F= '/^\[Install/ {p=1} p && /^Default=/ {print $2; exit}' ~/.config/mozilla/firefox/profiles.ini) && cd "$HOME/.config/mozilla/firefox/$PROFILE_DIR" && touch user.js
> ```

**2.** We open the newly created user.js in the `nano` editor:
```bash
nano user.js
```

**3.** We copy this security configuration array and paste it in its entirety:
```javascript
// ============================================================================
// HARDENING CONFIG FOR MOZILLA FIREFOX (USER.JS)
// UNCOMPROMISING PRIVACY AND SECURITY HARDENING
// ============================================================================

// 1. BASE CONFIDENTIALITY AND ISOLATION
// Enable global tracking protection against ad ecosystems. Additionally force the browser to route temporary downloads strictly to `/tmp` in RAM (preventing disk artifacts post-session), and completely purge *Private Attribution* — Mozilla's hidden commercial ad-click tracking mechanism
user_pref("privacy.trackingprotection.enabled", true);
user_pref("privacy.trackingprotection.socialtracking.enabled", true);
user_pref("privacy.partition.network_state.ocsp_cache", true);
user_pref("privacy.providers.fingerprinting", true);
user_pref("privacy.providers.trackingprotection", true);
user_pref("dom.private-attribution.submission.enabled", false); // Purge hidden Mozilla click collection
user_pref("browser.download.start_downloads_in_tmp_dir", true); // Route downloads strictly to volatile memory (/tmp)
user_pref("browser.helperApps.deleteTempFileOnExit", true); // Wipe download cache on exit
user_pref("security.sandbox.content.level", 4); // Lock content sandbox on Linux (maximum process isolation level)
user_pref("browser.startup.page", 0);
user_pref("browser.newtabpage.enabled", false);
user_pref("browser.startup.homepage", "about:blank");

// 2. REMOVAL AND BLOCKING OF THE POCKET SERVICE
// Mozilla hardcoded the commercial Pocket content service into the Firefox core. We disable it completely at the kernel level to eliminate hidden background queries to its servers
user_pref("extensions.pocket.enabled", false);
user_pref("extensions.pocket.api", "");
user_pref("extensions.pocket.oAuthConsumerKey", "");
user_pref("extensions.pocket.site", "");

// 3. BLOCKING IP LEAKS VIA WebRTC
// The WebRTC protocol is enabled by default for in-browser calls (Telegram, Discord). However, it harbors a critical architectural vulnerability: when requesting ICE candidates for direct peer-to-peer communication, it can leak our real physical IP address outward, bypassing an active VPN tunnel. We eliminate this vector
user_pref("media.peerconnection.enabled", false);
user_pref("media.peerconnection.use_document_iceservers", false);
user_pref("media.peerconnection.video", false);
user_pref("media.peerconnection.identity.timeout", 1);

// 4. DISABLING WEBGL (GRAPHICS FINGERPRINTING PROTECTION)
// WebGL technology allows websites to utilize GPU compute power to render complex 3D graphics. Tracker scripts leverage this module to extract a unique digital footprint (*WebGL Fingerprint*) of our graphics card, identifying specific computer hardware with 100% precision. We disable hardware rendering
user_pref("webgl.disabled", true);
user_pref("webgl.enable-debug-renderer-info", false);

// 5. BLOCKING GEOLOCATION COLLECTION AND TRANSMISSION
// We block any attempts by the browser and external websites to determine our physical real-world location via geographic coordinates, surrounding Wi-Fi networks, or host system services
user_pref("geo.enabled", false);
user_pref("geo.provider.use_geoclue", false);
user_pref("geo.provider.network.url", "");
user_pref("geo.provider.msgeolocate", false);

// 6. BLOCKING ASYNCHRONOUS REQUESTS (BEACONS/PINGS)
// Many commercial resources employ covert background beacons to transmit analytics packets regarding user clicks and cursor telemetry — data that continues streaming in the background even after closing the tab. We sever this telemetry
user_pref("beacon.enabled", false);
user_pref("browser.send_pings", false);
user_pref("browser.send_pings.require_same_host", true);

// 7. DISABLING PERFORMANCE METRICS AND TIMERS
// Anti-fraud scripts can exploit high-precision CPU performance timers to execute side-channel telemetry attacks designed to covertly fingerprint hardware. We clamp timer resolution
user_pref("dom.enable_performance_navigation_timing", false);

// 8. BLOCKING BACKGROUND NETWORK PREFETCHING (PREDICTION)
// Firefox attempts to predict links a user might click, proactively establishing hidden parallel speculative connections in the background. This leads to unauthorized DNS leaks and unnecessary network chatter. We kill speculative prefetching completely
user_pref("network.predictor.enabled", false);
user_pref("network.predictor.enable-hover", false);
user_pref("network.prefetch-next", false);
user_pref("network.dns.disablePrefetch", true);
user_pref("network.dns.disablePrefetchFromHTTPS", true);
user_pref("network.http.speculative-parallel-limit", 0);

// 9. PURGING ADD-ON RECOMMENDATIONS AND CACHE
// We kill covert background queries to Mozilla servers that remotely audit our installed plugins, check transaction histories, and attempt to push "recommended" sponsored software in the add-on management panel
user_pref("extensions.getAddons.cache.enabled", false);
user_pref("extensions.htmlaboutaddons.recommendations.enabled", false);
user_pref("browser.discovery.enabled", false);
user_pref("browser.shopping.experience2023.enabled", false);

// 10. DISABLING ACCESS TO PHYSICAL HARDWARE SENSORS
// Websites have no legitimate right to query the physical telemetry of our PC or laptop, such as ambient light sensors, gyroscopes, accelerometers, or proximity sensors
user_pref("device.sensors.enabled", false);
user_pref("device.sensors.ambientLight.enabled", false);
user_pref("device.sensors.motion.enabled", false);
user_pref("device.sensors.orientation.enabled", false);
user_pref("device.sensors.proximity.enabled", false);

// 11. ULTIMATE FINGERPRINTING RESISTANCE AND NETWORK HIDING (TOR MECHANISM)
// We render our browser footprint completely generic by leveraging hardened defensive implementations from the Tor Project. The browser will forcibly hide local network connection statuses and block extensions from accessing system managers
user_pref("privacy.resistFingerprinting", true);
user_pref("privacy.resistFingerprinting.block_mozAddonManager", true);
user_pref("dom.netinfo.enabled", false);

// 12. DISABLING PERIPHERALS, VR, AND SPEECH APIs
// We block sites from querying attached hardware devices (e.g., gamepads), capturing silent screen grabs via media interfaces, intercepting desktop streaming, and initiating speech recognition modules
user_pref("dom.gamepad.enabled", false);
user_pref("dom.imagecapture.enabled", false);
user_pref("dom.presentation.enabled", false);
user_pref("media.getusermedia.screensharing.enabled", false);
user_pref("media.navigator.enabled", false);
user_pref("media.navigator.permission.disabled", true);
user_pref("media.video_stats.enabled", false);
user_pref("dom.vr.enabled", false);
user_pref("dom.xr.enabled", false);
user_pref("media.webspeech.recognition.enable", false);
user_pref("media.webspeech.synth.enabled", false);

// 13. TOTAL PURGE OF SYSTEM TELEMETRY AND CRASH REPORTING (BREAKPAD)
// We completely sever the browser's architectural ability to transmit background crash logs, technical metrics, error logs, and stability telemetry to Mozilla servers or third-party collection endpoints (Breakpad)
user_pref("toolkit.telemetry.unified", false);
user_pref("toolkit.telemetry.enabled", false);
user_pref("toolkit.telemetry.archive.enabled", false);
user_pref("toolkit.telemetry.server", "");
user_pref("datareporting.healthreport.uploadEnabled", false);
user_pref("datareporting.policy.dataSubmissionEnabled", false);
user_pref("browser.tabs.crashReporting.sendReport", false);
user_pref("toolkit.crashreporter.enabled", false);
user_pref("breakpad.reportURL", "");
user_pref("security.ssl.errorReporting.automatic", false);
user_pref("network.allow-experiments", false);
user_pref("toolkit.telemetry.cachedClientID", "");
user_pref("toolkit.telemetry.cachedProfileGroupID", "");
user_pref("browser.newtabpage.activity-stream.feeds.telemetry", false);
user_pref("browser.newtabpage.activity-stream.telemetry", false);
user_pref("browser.newtabpage.activity-stream.telemetry.privatePing.enabled", false);
user_pref("browser.search.serpEventTelemetryCategorization.enabled", false);
user_pref("identity.fxaccounts.telemetry.clientAssociationPing.enabled", false);
user_pref("nimbus.telemetry.targetingContextEnabled", false);
user_pref("toolkit.coverage.endpoint.base", "");
user_pref("toolkit.telemetry.shutdownPingSender.enabled", false);
user_pref("toolkit.telemetry.newProfilePing.enabled", false);
user_pref("network.captive-portal-service.enabled", false);
user_pref("captivedetect.canonicalURL", "");

// 14. WIPING REGIONAL TRAILS AND ISOLATING SEARCH
// We prevent search algorithms from tailoring query results based on our host's current IP address or geographic location, enforcing a neutral region and disabling background geo-lookup queries
user_pref("browser.search.geoSpecificDefaults", false);
user_pref("browser.search.geoSpecificDefaults.url", "");
user_pref("browser.search.geoip.url", "");
user_pref("browser.search.region", "US");
user_pref("browser.search.suggest.enabled", false);
user_pref("browser.search.update", false);

// 15. DISABLING PUSH NOTIFICATIONS AND CAPTIVE PORTALS
// We block web resource push messaging (a common vector for targeted phishing attacks) and eliminate background network pings generated by public network captive portal detection mechanisms
user_pref("dom.push.enabled", false);
user_pref("dom.push.connection.enabled", false);
user_pref("dom.push.serverURL", "");
user_pref("network.captive-portal-service.enabled", false);

// 16. DNS HARDENING, SNI ENCRYPTION, AND CRITICAL DoH MODE (MODE 3)
// We strictly encrypt network transit and target hostname resolution. ISPs or network interception nodes will fail to observe target domains thanks to Encrypted Client Hello (*ECH*) SNI protections and strict isolated DNS-over-HTTPS Mode 3
user_pref("network.dns.disableIPv6", true);
user_pref("network.dns.echconfig.enabled", true);
user_pref("network.trr.mode", 3);
user_pref("network.trr.custom_uri", "https://dns10.quad9.net/dns-query"); // Or any designated DoH endpoint from our whitelist!
user_pref("network.proxy.socks_remote_dns", true);

// 17. PURGING GOOGLE SAFE BROWSING HASH LEAKS AND DRM MODULES
// The integrated *Safe Browsing* mechanism continuously streams visited site data and file hashes back to Google infrastructure. We disable this telemetry, while overriding the default stub that blocks downloads when Safe Browsing is disabled. Additionally, we purge closed-source binary DRM modules
user_pref("browser.safebrowsing.malware.enabled", false);
user_pref("browser.safebrowsing.phishing.enabled", false);
user_pref("browser.safebrowsing.downloads.enabled", false);
user_pref("browser.safebrowsing.downloads.remote.enabled", false);
user_pref("browser.safebrowsing.downloads.remote.block_as_unencrypted", false);
user_pref("browser.safebrowsing.downloads.remote.url", "");
user_pref("media.eme.enabled", false);
user_pref("browser.eme.ui.enabled", false);
user_pref("browser.safebrowsing.provider.google4.dataSharing.enabled", false);
user_pref("browser.safebrowsing.provider.google4.updateURL", "");
user_pref("browser.safebrowsing.provider.google4.gethashURL", "");
user_pref("browser.safebrowsing.provider.mozilla.updateURL", "");
user_pref("browser.safebrowsing.provider.mozilla.gethashURL", "");

// 18. ROUTING ALL CACHE EXCLUSIVELY TO RAM (PROTECTING SSD LIFESPAN & OPSEC)
// By default, Firefox writes gigabytes of temporary cache directly to physical disk. Even on encrypted LUKS partitions, this degrades NVMe/SSD endurance and leaves physical traces until shutdown. We lock the entire cache space into volatile RAM up to 512 MB, ensuring it vanishes upon closing the process
user_pref("browser.cache.disk.enabled", false);
user_pref("browser.cache.memory.enabled", true);
user_pref("browser.cache.memory.capacity", 524288);

// 19. HARDENED KERNEL-LEVEL PROCESS ISOLATION (FISSION)
// We force-enable modern *Site Isolation* technology. This isolates every open tab and third-party iframe (e.g., ad banners) into discrete OS-level sandboxed processes, providing hardware-level mitigation against *Spectre/Meltdown* side-channel threats and blocking cross-tab session hijacking
user_pref("fission.autostart", true);
user_pref("dom.ipc.processCount", 8);

// 20. PLUGGING MICRO LEAKS (CLIPBOARD, URL STRIPPING, FONT ISOLATION)
// We block covert metadata leakage to third-party endpoints. We restrict web scripts from intercepting or tampering with clipboard contents, enforce strict URL tracking parameter stripping, and prevent trackers from querying installed host system fonts (*Font Fingerprinting*)
user_pref("privacy.query_stripping.enabled", true);
user_pref("privacy.query_stripping.enabled.pbmode", true);
user_pref("layout.css.font-visibility", 1);
user_pref("network.http.referer.XOriginPolicy", 2);

// 21. CLOSING STRUCTURAL NETWORK VECTORS (DISABLING OCSP TELEMETRY)
// We disable background OCSP certificate verification queries that silently transmit validation telemetry to third-party servers without explicit user authorization
user_pref("security.tls.enable_post_handshake_auth", false);
user_pref("security.OCSP.enabled", 0);
user_pref("security.OCSP.require", false);

// 22. DISABLING COVERT EXPERIMENTS (MOZILLA STUDIES/NORMANDY)
// We block the browser from participating in background experiments that allow remote configuration pushes. We purge all telemetry pathways feeding usage data to analytics endpoints
user_pref("app.shield.optoutstudies.enabled", false);
user_pref("app.normandy.enabled", false);
user_pref("app.normandy.api_url", "");

// 23. SMOOTH SCROLLING HARDENING
// We tune render performance settings to eliminate frame stutter when navigating complex web assets, enabling hardware smooth scrolling while setting baseline line-scroll increments for consistent reading dynamics
user_pref("general.smoothScroll", true);
user_pref("mousewheel.min_line_scroll_amount", 20);

// 24. ENABLING WEBRENDER ACCELERATION (GPU OFFLOADING)
// We offload page rendering tasks from the main CPU to GPU execution pipelines. This significantly reduces host system overhead when processing heavy script execution or graphics loads
user_pref("gfx.webrender.all", false);
user_pref("gfx.webrender.software", true);

// 25. PURGING SPONSORED ADS AND CONTENT FROM NEW TAB PAGE
// We completely cut all sponsored tiles, ad blocks, and news feeds from the start page layout, while clearing telemetry endpoint targets to prevent search activity leakage
user_pref("browser.newtabpage.activity-stream.telemetry.structuredIngestion.endpoint", "");
user_pref("browser.newtabpage.activity-stream.showSponsored", false);
user_pref("browser.newtabpage.activity-stream.showSponsoredTopSites", false);
user_pref("browser.newtabpage.activity-stream.feeds.discoverystreamfeed", false);
user_pref("browser.newtabpage.activity-stream.feeds.section.topstories", false);

// 26. CANVAS AND ANTIFINGERPRINTING PROTECTION
// We activate native digital footprint masking mechanics. The engine injects dynamic noise when sites attempt covert Canvas rendering, while spoofing system markers to defeat hardware profiling without breaking web layouts
user_pref("privacy.fingerprintingProtection", true);
user_pref("privacy.fingerprintingProtection.pbmode", true);
user_pref("privacy.trackingprotection.fingerprinting.enabled", true);

// 27. TOTAL COOKIE ISOLATION (TOTAL COOKIE PROTECTION/dFPI)
// We eliminate cross-site tracking vectors by placing each domain's cookies into its own isolated jar. Third-party ad scripts lose the technical ability to read foreign cookie IDs while maintaining functional authentication states across trusted portals
user_pref("privacy.firstparty.isolate", false); // We leave old rigid Tor FPI disabled to avoid site breakage
user_pref("network.cookie.cookieBehavior", 5);  // Enable Dynamic First-Party Isolation (Total Cookie Protection)
user_pref("network.cookie.cookieBehavior.pbmode", 5); // Mirror cookie isolation within private browsing mode

// 28. WIDEVINE PLUGIN DOWNLOAD PREVENTION
// In addition to disabling DRM execution, we kill background downloads of the Widevine plugin binary itself
user_pref("media.gmp-widevinecdm.enabled", false);
user_pref("media.gmp-widevinecdm.visible", false);
user_pref("media.gmp-provider.enabled", false); // Disables GMP provider globally
user_pref("media.gmp.storage.version.observed", 0);

// 29. BLOCKING CODEC MANAGER SERVERS
// Prevent Firefox from probing Mozilla infrastructure for codec updates or binary module blobs
user_pref("media.gmp-manager.url", "");
user_pref("media.gmp-manager.buildID", "");
user_pref("media.gmp-manager.updateEnabled", false);
```

To save the configuration in `nano`, we hit **«Ctrl + O»** → **«Enter»**, and then **«Ctrl + X»** to exit back to the terminal prompt.

If a malicious script or internal Firefox update trigger attempts to edit `user.js` to restore WebRTC or re-enable telemetry, we block access by enforcing read-only permissions at the Linux kernel level immediately following file creation:

**4.** We set read-only permissions for the file owner inside the current profile directory:
```bash
chmod 0400 user.js
```

We effectively lock write access to this configuration file for any unprivileged process. Now, even if a user accidentally modifies a preference via the browser UI, the Gecko engine will re-read the locked `user.js` on the next reboot and forcibly restore our custom security baseline.

> [!NOTE]
> If we need to remove `user.js` in the future to reset settings, we first restore write permissions before deleting it:
> ```bash
> chmod 600 ~/.config/mozilla/firefox/*-release/user.js && rm ~/.config/mozilla/firefox/*-release/user.js
> ```

We have thoroughly mapped out hardened Firefox parameters to guarantee zero unauthorized data leakage to external networks. Without executing these manual interventions, any modern browser acts as a continuous telemetry siphon tracking user movements across the web.

**5.** Once all telemetry routines, trackers, and architectural attack surfaces are purged from the browser core, we shut down the application and bring our system back online. We toggle the network switch in the system tray back on, or run the final bring-up command in the terminal (replacing `enp0s1` with your actual interface name):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

Now, instead of a tracking platform, we command a completely anonymous, encrypted, hardened terminal. Operating under uncompromising OPSEC, we can safely re-enter the web perimeter and proceed to extension deployment!

> [!IMPORTANT]
> If, after applying `about:config` hardening, verification test suites (Browserleaks/CreepJS) continue to show a static hash for our font footprint — do not panic. This is the primary indicator that our defenses are fully operational. By restricting font visibility to level `1`, we obscured our host's unique 1xx local font stack, forcing the browser to present a generic baseline web font package. Because the input telemetry metrics are static and uniform, the site-generated hash freezes, permanently preventing anti-fraud engines from tracking unique host system artifacts. We have successfully blended into the crowd of anonymous users.
> 
> Some legacy hardening manuals recommend completely disabling document fonts via `browser.display.use_document_fonts = 0`. We reject this approach. That directive forcibly blocks all CSS fonts, breaking modern UI rendering and turning web icon fonts into broken square glyphs. Furthermore, completely disabling document fonts instantly flags our profile as a critical anomaly to remote threat engine scanners. Our chosen parameter, `layout.css.font-visibility = 1`, preserves complete web page functionality while isolating host local fonts from signature scanners.
> 
> During privacy verification runs, we will observe a specific architectural behavior: the system font hash remains static, while the Canvas Fingerprint shifts dynamically on every page reload. This represents the target baseline behavior of Firefox's native security core (`privacy.resistFingerprinting`). The Gecko engine deploys a dual-layer strategy: it blinds trackers to local host fonts by normalizing them to a standardized baseline, while injecting cryptographic pixel noise on the fly into Canvas streams. This noise is generated natively within the browser source code, rendering our traffic mathematically indistinguishable from millions of operational Tor Browser instances.
> 
> **Keep in mind that Firefox configurations evolve across software releases — parameters functional today may require adjustments after upstream updates!**

#### Deploying Ultimate Security Extensions:

Since our previously activated parameter `privacy.resistFingerprinting` (RFP) already flawlessly spoofs and masks all critical fingerprints directly at the Gecko engine source level, we only need to integrate two foundational extensions from the official Mozilla Add-ons store:

* **uBlock Origin** (developed by Raymond Hill) — `https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/`. The industry's leading blocker for ads, covert mining scripts, tracking telemetry, and malicious phishing domains. Delivers top-tier execution performance with near-zero RAM overhead.
* **NoScript Security Suite** (developed by Giorgio Maone) — `https://addons.mozilla.org/en-US/firefox/addon/noscript/`. The ultimate mandatory access control system for JavaScript execution. It empowers users to dynamically authorize or block script execution across web assets in real time, guaranteeing absolute protection against zero-day browser exploits. **Run strictly in STRICT mode!**

> [!IMPORTANT]
> Enabling `privacy.resistFingerprinting = true` forcibly sets the browser's internal timezone to neutral UTC (concealing our real geographic region), locks browser window dimensions to standard fixed resolutions (introducing distinct gray padding borders — *Letterboxing* — when maximized), and reports a generic default graphics interface to external endpoints.
> 
> However, if JavaScript remains fully execution-enabled on a target domain, sophisticated anti-fraud telemetry scripts can still observe subtle rendering micro-delays to infer underlying hardware profiles.
> 
> The **NoScript** extension permanently seals this attack vector: with JavaScript execution blocked on a target domain, the site is physically incapable of deploying fingerprinting collection scripts. To maintain maximum operational anonymity, disable JS execution via the NoScript dashboard across all untrusted endpoints, enabling it temporarily and granularly only on trusted, essential web assets.
> 
> Blocking JavaScript execution will cause heavy, highly interactive modern sites to render incorrectly or lose dynamic functions — a natural and fully justified trade-off for ultimate privacy enforcement.

**Chapter Asset:** *_assets\images\9_firefox*

<br>

## Installing and Configuring the Portmaster Interactive Network Firewall

#### Introduction:

Portmaster is a powerful next-generation interactive firewall designed for deep real-time network traffic analysis. The utility packs a rich array of low-level filtering mechanics and granular security policies.

Unlike legacy solutions such as OpenSnitch, Portmaster enforces an out-of-the-box permissive "Allow" posture. It permits host binaries outbound network access by default. Traffic gets dropped only after an operator explicitly blacklists a target application or tightens the engine's global security parameters.

#### Preparation, Initial Kernel Initialization, and Upgrading:

To deploy the current release of Portmaster without triggering kernel cascades, UFW routing conflicts, or excessive CPU lockups, we execute my custom two-stage offline upgrade tactic.

**1.** We launch our hardened Firefox instance and navigate to the official portal at `[https://safing.io](https://safing.io)`. We download the complete offline installer for Portmaster v2 as a `.deb` package (tailored for Debian/Ubuntu environments). Once the download finishes, we kill the Firefox process entirely.
```text
https://updates.safing.io/latest/linux_amd64/packages/Portmaster_2.2.1_amd64.deb \\ Direct link valid as of August 26, 2026 (release date: July 17, 2026).
```

**2.** We spawn a terminal session on the host. We fetch the official stable legacy `.deb` package from Safing's update mirrors to instantiate baseline directory structures:
```bash
wget https://updates.safing.io/latest/linux_amd64/packages/portmaster-installer.deb
```

**3.** We unpack the fetched package via `apt`. The package manager automatically resolves and pulls the critical low-level kernel dependency `libnetfilter-queue1`:
```bash
sudo apt install ./portmaster-installer.deb -y
```

**4.** As soon as unpacking finishes, we forcibly cut the OS network stack. This is mandatory for safely provisioning internal control sockets:
```bash
nmcli networking off
```

We launch the Portmaster GUI through the desktop application menu (*"Show Apps"*). On initial launch, the interface triggers a critical notice: **The Portmaster Core is not running**. We hit **"START CORE SERVICE"** and enter our `root` administrative credentials in the authentication modal.

On the **Portmaster Protects Your Privacy** onboarding screen, we hit the blue **"Quick Setup"** button. On the subsequent **Trackers Are Blocked System-Wide** pane, we click **"Next"**.

Under **Secure DNS For All Connections**, we locate the **Customize** dropdown. We pick a trusted Swiss DNS endpoint from the built-in preset list (for instance, **Set Quad9**), collapse the menu, and hit **"Next"**. On the final **Learn More As You Explore** pane, we hit **"Finish"**.

In the left vertical navigation bar, we click the gear icon (**Settings**). We navigate to **Privacy Filter** and pinpoint the **Default Network Action** subsection. We switch the dropdown value from the default **Allow** state to **Prompt**. The firewall will now intercept all outbound traffic streams and request explicit operator authorization per outbound connection request.

**5.** We briefly bring the network interface back up so Portmaster can pull missing auxiliary libraries and rule sets (remembering to specify our actual network interface name):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

**6.** As soon as initialization completes and the firewall status indicator turns solid green, we kill the host network stack once again:
```bash
nmcli networking off
```

> [!IMPORTANT]
> The architectural brilliance of this tactic lies in tricking Safing's Go runtime initialization pipeline. Attempting a raw, direct deployment of Portmaster v2 onto a machine enforcing a strict UFW Kill Switch locks up its engine due to an empty local database cache. It constantly tries to register eBPF hooks while colliding with UFW drop rules, entering a dead loop that maxes out CPU cores at 100% due to permanent sync faults.
>
> Our two-stage offline deployment permanently bypasses this bug:
>* The legacy base version (1.6.10) safely builds the target directory layout, configuration structure, and initial database skeleton inside `/opt/safing/portmaster/` offline without triggering conflicts with UFW.
>* When we subsequently apply the standalone v2 (2.2.1) package over the legacy deployment, the new engine detects the existing database layout. It attaches to the initialized base and operates alongside UFW, maintaining low CPU utilization (0–2%). Both defensive layers function in parallel without compromising the host Kill Switch configuration!

**7.** Maintaining complete radio silence with the network stack dropped, we switch to the terminal and navigate to the directory containing our downloaded offline package:
```bash
cd ~/Downloads/
```

**8.** We deploy the offline Portmaster v2 build over the legacy base. APT automatically halts background daemons, updates binary executables, and rewrites `systemd` units without attempting to query external endpoints:
```bash
sudo apt install ./Portmaster_*.deb -y
```

**9.** To cleanly initialize the updated eBPF driver inside the Linux kernel, we trigger a system reboot:
```bash
sudo reboot now
```
> [!NOTE]
> **Critical Note:** Upon landing on the desktop session, the firewall GUI will request authorization to establish an internal connection to the loopback interface (`localhost 127.0.0.1`). Hit **Allow** to confirm the prompt.

**10.** To ensure compatibility with Firefox, we temporarily unlock the write permissions on its configuration payload to modify its DNS resolver behavior:
```bash
chmod 600 ~/.config/mozilla/firefox/*-release/user.js
```

**11.** We open `user.js` in the `nano` terminal editor:
```bash
nano ~/.config/mozilla/firefox/*-release/user.js
```

**12.** We locate section **16. DNS HARDENING, SNI ENCRYPTION, AND CRITICAL DoH MODE**. We adjust the low-level parameter `network.trr.mode` from value `3` (isolated mode) back to default **`0`**:
```javascript
user_pref("network.trr.mode", 0);
```
> [!NOTE]
> **Author's Infosec Analysis:** Flipping this parameter to `0` completely kills Firefox's standalone DoH engine. The browser stops trying to punch through the network with isolated encrypted queries, which Portmaster v2 flags as potential telemetry leaks and drops by default. Firefox now hands DNS requests directly to the host OS, where Portmaster's eBPF hooks immediately intercept, filter, and encrypt them host-wide.

To save changes in `nano`, hit **"Ctrl + O"** → **"Enter"**, then **"Ctrl + X"** to exit back to the shell prompt.

**13.** We re-apply strict read-only permissions on `user.js` to protect it against unauthorized tampering by extensions, browser updates, or malware:
```bash
chmod 0400 ~/.config/mozilla/firefox/*-release/user.js
```

**14.** To keep our filesystem clean, we purge the residual `.deb` installer artifacts from our local folder:
```bash
rm ~/Downloads/Portmaster_*.deb && rm ~/portmaster-installer.deb
```

**15.** We restore the system network stack to operational status. To ensure the link comes up cleanly (since automatic connection toggles may be disabled in Ubuntu network settings), we run NetworkManager to force-activate our target interface in a single command chain (replacing `enp0s1` with your actual interface identifier):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

> [!TIP]
> Daily-driver, trusted applications (such as our hardened Firefox build) can be assigned permanent outbound network access authorization. 
> 
> To configure persistent rules, launch Firefox. Look up at the top GNOME system status panel (next to the clock, keyboard layout, and network tray) and click the Portmaster indicator icon. In the compact status menu, hit **Open App**. 
> 
> This opens the interactive network activity monitor, displaying the active Firefox browser process in the left application column. Click it, navigate to the internal **Settings** tab, scroll down to **Privacy Filter** → **Default Network Action**, and switch the strict default **Prompt** rule to **Allow**.
> 
> Using this operational workflow, we can grant permanent access permissions, toggle "Prompt on demand" mode, or block any system service, Docker container, or user utility in our OS directly from the system tray in a single click.

**Chapter Asset:** *_assets\images\10_portmaster*

<br>

## Guaranteed Data Destruction and Sterilizing Your Digital Footprint

#### Introduction:

We will break down step-by-step how the `shred` and `wipe` utilities physically overwrite data bytes on storage media, defending our host against forensic analysis if a device is physically compromised. However, defensive engineering goes beyond local disk perimeters. We must enforce a strict operational security baseline: **every file leaving your host and entering external networks must be completely sterile**.

#### Anatomy of a Digital Footprint: Why Deleting Files Is Useless Without Metadata Sanitization:

Most operators commit a fatal mistake: assuming a text document, a screenshot of firewall rules, or a rendered image contains only what is visible to the eye. This assumption is dangerous.

Every file acts as a "Trojan Horse", carrying a hidden payload of operational telemetry known as **metadata** (EXIF tags in imagery, document attributes in PDF and Office files). Publishing a file online, transmitting it via messaging channels, or pushing it to GitHub voluntarily leaks critical host intelligence to trackers and adversary nodes:

* **Timestamps:** Precise creation and modification timestamps down to the second. Threat analysts leverage these metrics to calculate host time zones and map operational uptime schedules.
* **Software Footprint:** Unique application identifiers (UUIDs), build numbers, and text or graphics editor signatures. This enables an adversary to profile installed host software for known vulnerabilities.
* **Host Telemetry:** Metadata entries frequently log system username identifiers, hostname descriptors, and active OS kernel builds.
* **Geospatial Telemetry:** Photos captured via smartphones or GPS-enabled sensors embed exact geospatial coordinates within the file structure.

For OSINT researchers and target acquisition teams, metadata scraping is the lowest-hanging fruit for host deanonymization. You can deploy a hardened Ubuntu workstation wrapped in an encrypted VPN and UFW Kill Switch, but releasing a single unsterilized screenshot immediately links your online persona to your real-world digital fingerprint.

> [!IMPORTANT]
> The `shred` and `wipe` mechanics detailed below handle file **destruction** on local storage volumes. However, they provide zero protection if an unsterilized payload has already reached a remote server!
> 
> Before initiating any upload or transfer command, every file must undergo a full sanitization pass. In Linux environments, the industry standard for metadata removal is `mat2` (Metadata Anonymisation Toolkit 2). Rather than simply clearing tags, `mat2` strips and reconstructs file containers from scratch to output a clean duplicate free of historical artifacts.

#### Installing and Sanitizing Metadata with MAT2:

`mat2` is written in Python, executes entirely on the local host, and requires zero external API queries (which would introduce severe operational risks).

**1.** We install the standalone `mat2` CLI binary from the official Ubuntu repositories:
```bash
sudo apt install mat2 -y
```

**2.** Prior to sanitizing a file, we can inspect its underlying metadata parameters to identify embedded host artifacts. We command the utility to parse and log all hidden tags (e.g., within a local screenshot):
```bash
mat2 --show screenshot.png
```
The terminal outputs a detailed telemetry audit: ranging from graphics engine builds to exact screenshot timestamp markers.

Next, we proceed with data sanitization. By default, `mat2` enforces a safe operational posture — it preserves the target source asset and generates a sterile duplicate bearing the `.cleaned` file suffix.

**3.** We sanitize an isolated document or image asset:
```bash
mat2 screenshot.png
```
This generates `screenshot.cleaned.png` in the local working directory. This sterile payload is safe for network transmission. If the source asset is no longer required, we immediately burn it via `shred` (commands detailed below).

**4.** To sanitize an entire folder of reports, screenshot captures, or log archives prior to deployment, we invoke batch processing mode across the target directory:
```bash
mat2 /PATH-TO-FOLDER/*
```

**5.** For high-security environments where unsterilized source files must not persist on disk even temporarily, we enforce inline sanitization by passing the `-inplace` flag (overwriting the target assets in place):
```bash
mat2 --inplace screenshot.png
```
**6.** We execute inline metadata sanitization across all files within a target directory structure:
```bash
mat2 --inplace /PATH-TO-FOLDER/*
```

> [!IMPORTANT]
> Passing the `--inplace` parameter permanently destroys the original source metadata. If original creation timestamps are required for local archival records, operate strictly in default mode to produce `.cleaned` asset duplicates.

With our files sanitized of digital host signatures, operational telemetry leaks are blocked. But how do we handle residual working assets, draft buffers, and temp files remaining on our encrypted LVM volumes? We now deploy physical data destruction tools to purge residual blocks from the filesystem.

#### Secure and Irreversible File and Directory Destruction:

For irreversible data wiping of confidential directories and files, we deploy the specialized `wipe` CLI tool, which overwrites targeted sectors using multi-pass wiping algorithms. Alternatively, Linux distributions include the native `shred` utility out of the box; `shred` reliably sanitizes raw files but cannot natively traverse directory structures.

> [!IMPORTANT]
> **Critical Operational Note on Solid State Drives (SSDs):** 
> On modern SSD storage media, utilities like `shred` and `wipe` do not guarantee 100% block-level physical data destruction at the flash cell layer. Wear Leveling algorithms on the storage controller dynamically reassign write operations across physical NAND flash addresses to manage drive endurance. Furthermore, executing high-pass legacy overwrites (such as 35-pass Gutmann patterns) unnecessarily degrades the drive's total bytes written (TBW) lifecycle.
> 
> Because our Ubuntu host is fully encrypted at the kernel layer using LUKS, executing 1–3 overwrite passes is technically sufficient for secure asset destruction on an SSD. Once file metadata pointers within an encrypted volume are overwritten, recovering underlying blocks outside the active LUKS container becomes mathematically impossible — residual flash cell fragments remain inaccessible as encrypted noise.

We open a terminal session and execute the following deployment sequence:

**1.** We install the destructive data purging utility `wipe`:
```bash
sudo apt install wipe -y
```

**2.** We recursively purge a target folder along with its complete file tree (replace the `FOLDERNAME` placeholder with your target directory path):
```bash
wipe -rfi FOLDERNAME
```

The `-r` flag enforces recursive directory traversal, `-f` suppresses interactive confirmation prompts, and `-i` activates verbose progress telemetry to report sector overwriting status.

**3.** We execute destructive sanitization across all files in the current working directory (**Deploy with extreme caution!**):
```bash
sudo shred -v -u -z -n 3 *
```

> [!WARNING]
> **Warning!** Using the wild-card glob operator `*` in Linux introduces potential execution risks. The `*` character is expanded directly by the host shell. If the target directory contains nested subdirectories, `shred` fails on those paths, throws a system error: *"shred: failed to open for writing: Is a directory"*, and may abort execution of subsequent targets.
> 
> To ensure execution safety, we combine `shred` with the `find` utility:

**4.** We safely isolate and destroy files exclusively on the top level of the current directory without triggering errors on subfolder structures:
```bash
find . -maxdepth 1 -type f -exec shred -v -u -z -n 3 {} \;
```

**5.** We securely destroy a specific isolated file target (replace the `FILENAME` placeholder with the exact filename, maintaining case sensitivity and file extension):
```bash
shred -v -u -z -n 3 FILENAME
```

#### Operational Parameters for the shred Utility:

* **`-v`** (*verbose*) — Displays real-time progress metrics in the terminal console.
* **`-u`** (*unlink*) — Automatically unlinks and deletes the target file entry after completing overwrite operations.
* **`-z`** (*zero*) — Executes a final overwrite pass using pure zeroes to mask data destruction footprints.
* **`-n 3`** — Specifies the exact number of overwrite passes (setting `3` passes provides an optimal balance of security and SSD longevity).

> [!IMPORTANT]
> By default, Ubuntu formats storage volumes using the Ext4 filesystem with data journaling enabled (`data=ordered`). Consequently, file metadata and payload blocks pass through a hidden system journal (`journal`) prior to being committed to primary storage sectors. Tools like `shred` and `wipe` overwrite target payload addresses on disk but cannot reach transient copies stored in Ext4 journal buffers (as explicitly documented in `man shred`).
> 
> Full-disk LUKS encryption mitigates this issue because the underlying Ext4 journal resides within the encrypted LUKS container. However, when sanitizing files on unencrypted external Ext4 drives, note that residual data blocks may linger within the drive's system journal.

#### Global Wiping of Unallocated Disk Space:

If an operating system has been in service for an extended period and confidential files were deleted via standard file manager methods (such as moving items to **Trash** via the **Delete** key), unallocated space across the drive may hold un-overwritten data blocks. To purge previously deleted file artifacts across an SSD simultaneously, we deploy the `secure-delete` tool suite:

**1.** We install the `secure-delete` utility suite:
```bash
sudo apt install secure-delete -y
```

**2.** We execute a complete wiping pass across unallocated space on the host root system partition:
```bash
sudo sfill -v -z -l /
```

> [!NOTE]
> Passing the `-l` (*low security*) flag reduces the pass count to two overwrites. This preserves SSD write endurance while populating free storage blocks, system journals, temp folders, and log structures with random data and trailing zeroes.

<br>

## Steganography, Obfuscation, and Anti-Forensics Trace Hiding in Ubuntu

#### Introduction:

Once metadata has been sanitized using `mat2` and transient artifacts permanently destroyed via `shred` or `wipe`, our focus shifts to the next operational goal: transmitting or storing critical intelligence while keeping the mere existence of the data completely covert.

Under aggressive state censorship and pervasive network surveillance, deploying raw cryptographic payloads often triggers monitoring systems, as encrypted files appear as suspicious "digital noise." To counter this, we deploy steganography (embedding data inside benign cover objects) and obfuscation (scrambling information structures).

#### Linux Steganography: Concealing Files Within Media Content:

Steganography allows us to embed deep inside an innocent container file (such as a photo or an audio track). The cover asset retains full functional integrity, opens seamlessly in native media players, and remains visually indistinguishable from the original source.

> [!IMPORTANT]
> Our cover file must be an authentic, high-quality asset of adequate size. Injecting hidden payload data into undersized containers creates anomalous file size-to-resolution ratios that attract forensic scrutiny.

#### The steghide Command-Line Utility:

We start with a classic toolchain component. `steghide` is a lightweight CLI utility available directly from the official Ubuntu repositories. It integrates seamlessly into our bash scripts (for example, to quietly exfiltrate security logs). The utility supports payload embedding within JPEG, BMP, WAV, and AU containers, relying on resilient AES-256 encryption by default.

**1.** We install the package in a single command:
```bash
sudo apt update && sudo apt install steghide -y
```

**2.** We embed our secret file `secret.txt` inside a target image `photo.jpg`:
```bash
steghide embed -cf photo.jpg -ef secret.txt
```
**3.** We purge the remaining `secret.txt` source payload left outside our steganographic container:
```bash
shred -v -u -z -n 3 secret.txt
```

The system will prompt for a strong passphrase. The output `photo.jpg` file remains visually identical to its pre-processed state.

**4.** To extract hidden payload contents from the container, we execute:
```bash
steghide extract -sf photo.jpg
```

We supply the secret passphrase configured during the embedding phase, and the utility instantly unpacks the source file back to disk.

> [!IMPORTANT]
> The `steghide` utility operates strictly on legacy formats: **JPEG, BMP, WAV, and AU**. Attempting to pass modern formats like **PNG** or **MP3** will result in an operational error. This stems from underlying compression mechanics:
> * PNG uses lossless compression. The embedding techniques used by `steghide` break PNG optimization structures, causing abnormal file size growth that flags covert channel activity.
> * MP3 employs lossy compression. The MP3 compression pipeline treats covert bit modifications within the audio stream as unwanted noise, stripping payload data during playback or transcoding.

#### Stealth Concealment via the Advanced StegoForge Tool:

StegoForge is a versatile dual-use framework built for both Red and Blue Team operations. It enables operators to embed data covertly into media files and inspect suspicious containers using integrated detection modules.

Unlike legacy utilities limited to basic image embedding, this framework provides multi-container support:

* Images: Data injection via classic LSB, adaptive LSB, and JPEG DCT coefficient manipulation. Supports PNG, JPG/JPEG, BMP, and additional formats.
* Audio: Payload encoding into spectrograms or psychoacoustic masking within PCM streams (frequencies imperceptible to the human ear). Supports WAV, FLAC, MP3, and more.
* Video: Motion vector modification within MP4 and WebM streams. Supports AVI, MKV, MOV, and related codecs.
* Documents: Payload embedding within XML structures, incremental PDF update objects, font-spacing tweaks, and invisible glyphs. Supports DOCX, PDF, PPTX, and other office formats.
* Network Packets: Covert data encapsulation within unused header fields of network protocols (e.g., TCP/IP) embedded in PCAP trace files.

The framework is engineered to bypass 11 advanced stegananalysis detection engines integrated into its testing suite. These include statistical evaluation (Chi-square testing, RS analysis), signature scanning routines, and deep neural networks (ONNX-formatted CNN models) trained to detect spatial file anomalies. To remain undetected by all 11 evaluation engines, the framework leverages adaptive embedding algorithms. Instead of sequential bit modification, payload data is distributed across dynamic regions of the container. Data is written exclusively to high-entropy areas (such as noisy image regions or high-motion video frames) where modifications introduce minimal variance to the overall statistical footprint. If the container's histogram remains neutral, statistical and neural engines return a status of "Payload not detected".

Data security does not rely solely on hiding the steganographic algorithm. Should a container be identified, adversaries encounter robust cryptographic layers:

* Encryption: All target payloads are encrypted prior to embedding using symmetric AES-256 in GCM mode, guaranteeing confidentiality alongside cryptographic authentication.
* Key Derivation: User passphrases are processed into cryptographic keys using the memory-hard Argon2 function, mitigating brute-force attacks.
* Plausible Deniability: StegoForge supports dual-key generation for a single container. Supplying a false key extracts harmless bait text, while the authentic operational key unlocks the true hidden payload.

**1.** We fetch the application binary from `github.com`:
```bash
wget https://github.com/Nour833/StegoForge/releases/download/v1.1.5/stegoforge-linux-x86_64
```

**2.** We create a local binary directory, relocate the executable, assign execution permissions, and export the directory path to our shell environment:
```bash
mkdir -p ~/.local/bin && mv ~/stegoforge-linux-x86_64 ~/.local/bin/stegoforge && chmod +x ~/.local/bin/stegoforge && grep -qxF 'export PATH="$HOME/.local/bin:$PATH"' ~/.bashrc || echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

**3.** We launch the utility:
```bash
stegoforge
```

Upon launching `stegoforge`, an interactive console menu initializes:

* 1 — Encode ........ Hide an encrypted payload inside a target container asset.
* 2 — Decode ........ Extract and decrypt a hidden payload.
* 3 — Detect ........ Audit a target file for hidden data.
* 4 — CTF Mode ...... Run all integrated detection engines and generate a forensic report.
* 5 — Capacity ...... Calculate maximum payload capacity for a target container.
* 6 — Web UI ........ Launch a local browser-based graphical interface.
* 7 — Survival ...... Test payload resilience against platform re-encoding or conversion.
* 8 — Dead Drop ..... Tools for dead drop exchanges and key management.
* 9 — Update ........ Check GitHub for recent releases and apply updates.
* d — Diff .......... Compare original and modified assets, including pixel heatmap rendering.
* b — Batch ......... Execute automated payload embedding across a directory of containers.
* q — Quit .......... Exit the StegoForge interface.

For operators deploying StegoForge for the first time, use this functional workflow reference:

* Need to hide a payload file → 1 Encode
* Need to extract a hidden file → 2 Decode
* Need to audit a suspicious file → 3 Detect
* Need to execute forensic analysis → 4 CTF Mode
* Need to assess storage capacity → 5 Capacity
* Bypassing the terminal interface → 6 Web UI
* Need to inspect visual differences → d Diff
* Need to process batch files → b Batch

> [!TIP]
> To streamline complex StegoForge workflows, we recommend deploying the built-in Web UI. It provides a clean graphical interface for primary operations, eliminating the need to memorize CLI parameters. The Web UI runs strictly on the loopback interface, binding exclusively to `[http://127.0.0.1:5000/](http://127.0.0.1:5000/)`.
> 
> To launch the web panel, open a terminal and execute:
> ```bash
> stegoforge
> ```
> 
> In the menu, select option six (6 — Web UI). Once initialized, navigate to `[http://127.0.0.1:5000/](http://127.0.0.1:5000/)` in your local browser.

#### Archive Concatenation (Quick Hack Without Third-Party Software):

This technique leverages fundamental differences in binary file structures. Most image viewers parse data starting from the file header (beginning of the file), whereas archive tools parse data starting from the end of the file container. We can concatenate both file formats into a single asset using native terminal commands.

**1.** We bundle our target documents into an encrypted ZIP archive:
```bash
zip -e secret.zip secret.txt
```

**2.** We merge the cover image and the encrypted archive into a unified file using `cat`:
```bash
cat cat.jpg secret.zip > final_photo.jpg
```

* **Hardening Verification:** Opening `final_photo.jpg` via standard desktop image viewers renders the original cover photo normally.
* **Payload Extraction:** Right-click the file ➔ *Open With "Archive Manager"* (or run `unzip final_photo.jpg` in terminal). The extraction tool bypasses leading image bytes and reads the archive structure from the end of the container file!

#### Text Obfuscation: Bypassing Automated Inspection Systems (DPI):

Automated traffic monitoring systems and Deep Packet Inspection (DPI) engines continuously scan network streams, message traffic, and uploaded files for forbidden keywords or static signatures. Altering underlying text encoding structures enables operators to bypass signature matching filters.

* **Homoglyph Substitution:** Replacing standard ASCII characters with visually identical Unicode glyphs breaks automated pattern matching. For instance, Cyrillic `С` and Latin `C` render identically to human operators but possess different byte representations. To automated scanners, `Secret` (using Latin `C`) and `Secret` (using Cyrillic `С`) represent distinct strings, allowing text payloads to pass through signature filters.
* **Zero-Width Characters:** Inserting zero-width spaces (`U+200B`) splits words into distinct byte fragments for automated tools while maintaining unified visual rendering on user displays.

#### Analyzing Hidden Threats: File Extension Spoofing (BiDi Attacks):

Defenders and operators working in high-risk environments must understand how Unicode manipulation can be weaponized by adversaries to mask malicious files.

One prevalent technique utilizes a hidden Unicode control character: **U+202E (RLO — Right-to-Left Override)**. This character forces display engines to render all subsequent text characters in reverse order (right to left).

When injected into executable filenames, the UI flips trailing extension strings, concealing the true binary type:
* **Actual path on the filesystem (as parsed by the kernel):** `document_[U+202E]fdp.exe`
* **Visual string displayed by graphical file managers:** `document_exe.pdf`

To the OS kernel, the file remains an executable binary (`.exe`), though human operators perceive it as a benign document (`.pdf`).

**1.** We simulate string rendering containing the inverted control character:
```bash
echo -e "File_name_\u202Efdp.exe"
```
The terminal output executes the direction flip, displaying the misleading string: `File_name_exe.pdf`.

**2.** To expose hidden Unicode manipulation, we invoke `cat` with the `-v` flag (displaying non-printable and hidden control characters):
```bash
echo -e "File_name_\u202Efdp.exe" | cat -v
```
*The raw output reveals the underlying control sequence (`^[[~` or its hex representation), exposing the string manipulation.*

> [!WARNING]
> Never trust visual file extensions displayed in GUI file managers for assets received from untrusted sources. Open a terminal session and verify underlying file headers using our native system tool `file`:
> ```bash
> file name_of_file
> ```
> The `file` utility inspects deep binary signatures and magic numbers that cannot be forged through surface filename modifications. If an executable Linux ELF binary or Windows PE payload is masked as a standard document, `file` accurately identifies the underlying file structure.

<br>

## Installing and Configuring the VeraCrypt Cryptographic Suite

#### Introduction to VeraCrypt and Installation:

VeraCrypt is a powerful tool for creating isolated encrypted containers and performing full-drive encryption on external USB drives and hard disks. The software provides total resistance to cryptanalysis and was engineered specifically for security-conscious professionals and privacy enthusiasts.

**Installation via Community PPA Repository:**

If receiving automatic software updates alongside operating system updates is preferred, a popular third-party security repository can be deployed:

**1.** We integrate the third-party encryption repository into the operating system:
```bash
sudo add-apt-repository ppa:unit193/encryption -y
```

> [!IMPORTANT]
> This PPA repository is maintained by independent community developers. Upon the release of fresh Ubuntu versions, a compiled package for the specific codename of the current distribution may be absent, causing the installation command to fail with a *«Package not found»* error.
> 
> If this occurs, completely purge this PPA from the system using `sudo add-apt-repository --remove ppa:unit193/encryption -y` and strictly execute **Option A (Native Method)**.

**2.** We install `VeraCrypt` from the connected repository:
```bash
sudo apt install veracrypt -y
```

**3.** We launch the application:
```bash
veracrypt
```

**Official Distribution Installation (Native Method):**

To completely eliminate outdated dependency conflicts on modern Ubuntu 24.04 and 26.04 LTS installations, we recommend deploying the official stable build directly from the developers at IDRIX:

* Open the browser and navigate to the official project site: `[https://veracrypt.fr](https://veracrypt.fr)`.
* Download the current installation package for Ubuntu (`.deb` file for `amd64` architecture, e.g., `veracrypt-x.x.x-Ubuntu-amd64.deb`).
* Open the terminal directly in the `~/Downloads` directory and execute the installation using the following sequential commands:

**1.** We update the local system package index:
```bash
sudo apt update
```

**2.** We execute the installation of the downloaded `.deb` package (the `apt` utility will automatically pull all required system dependencies):
```bash
sudo apt install ./veracrypt-*.deb -y
```

**3.** We launch the graphical interface of the encryption platform:
```bash
veracrypt
```

#### Deep Security Tuning: RAM Key Protection (Paranoia Mode):

By default, when mounting encrypted volumes, VeraCrypt retains master decryption keys in system RAM in plaintext. If an adversary gains physical access to an active host, they could attempt to extract these keys via low-level Cold Boot attacks (freezing and reading memory chips) or hardware DMA interfaces.

To completely neutralize this vector of compromise, navigate inside the VeraCrypt GUI to **Settings** ➔ **Preferences** (**Security** tab) and force-enable the available protection option:

* **«Wipe cached passwords on exit»** *(Enforce wiping password and keyfile caches from RAM upon exiting the program)*.

> [!NOTE]
> Unlike bloated Windows builds, the native VeraCrypt release for Linux lacks redundant RAM Encryption and extended caching toggles. This is due to the underlying mechanics of the Linux kernel: the operating system hardware-isolates the runtime memory of unprivileged users (`user`) via mandatory virtual memory controls, preventing unauthorized memory dumping without root privileges. Enabling the single cache-wipe option on exit provides complete offline protection for our master keys.

#### A Fundamental Security Tool: Creating Hidden Volumes:

For operating under high-threat environments, severe censorship, or the risk of coerced device inspection at borders, the mechanism of Plausible Deniability is critical. VeraCrypt enables operators to deploy a Hidden Volume.

The core operational concept functions as follows: a single standard encrypted container file is created, but configured with two distinct, independent passphrases:
* **Outer Volume:** Protected by the first passphrase. Neutral files are stored here, presenting an entirely plausible and benign presence on the computer (family archives, public documents, non-sensitive literature).
* **Hidden Volume:** Resides within the free space of the outer volume and is protected by a second, secret passphrase. It is mathematically encrypted such that its blocks are indistinguishable from random digital noise (empty space). No forensic tool can prove the existence of a secondary hidden partition within the container.

If forced to reveal a password under coercion or inspection, the first (decoy) passphrase is provided. VeraCrypt opens the outer volume normally, presenting neutral decoy files to inspectors. Proving the existence of the hidden volume is technically impossible, as the container visually appears completely filled with legitimate files and random unallocated block remnants. Genuine confidential data, keys, and private documents are decrypted exclusively by entering the second passphrase in a secure setting.

> [!IMPORTANT]
> By default, whenever data within a container is modified, the operating system updates the file modification timestamp on disk. If we covertly access the hidden volume and update files inside, the container headers update while the outer decoy file date remains old, instantly signaling to forensic analysts that a hidden volume was accessed.
> 
> To completely eliminate this forensic artifact, open **Settings → Preferences** in the VeraCrypt main menu and force-enable **«Preserve modification timestamp of file containers»**. This forces the utility to freeze the container file creation date, keeping the hidden volume indistinguishable from random encrypted data.

#### Ultimate Hardening: Configuring PIM and Hardware Keyfiles:

To protect high-value containers against advanced cryptanalysis and targeted brute-force campaigns (using GPU clusters), a standard text passphrase is insufficient. We leverage internal VeraCrypt mechanisms to establish maximum protection.

By default, VeraCrypt applies a fixed, high number of cryptographic hash iterations during volume header derivation. This significantly slows down offline password recovery attempts while adding a slight delay during volume mounting.

The **PIM** (Personal Iteration Multiplier) parameter allows operators to manually specify a custom iteration count during volume creation.

> [!TIP]
> **Operational Security Strategy:** Setting a high PIM reduces adversary brute-force efficiency to zero — computational clusters would require millennia to attempt even simple passphrases. The trade-off is a slightly longer mount delay on the operator's host.
> 
> If the volume's security relies on an extremely long and complex passphrase (exceeding 30–40 random characters), the PIM value can be intentionally reduced (below a 4-digit number) to ensure near-instantaneous volume mounting without sacrificing security.

Multiple keyfiles (any image, audio file, document, or randomly generated binary file) can be bound to the container. Mounting the volume requires providing both the correct text passphrase and the exact path to these keyfiles. Without the keyfiles, decrypting the volume remains mathematically impossible, even if the passphrase is compromised.

> [!WARNING]
> **Critical Rule for Keyfile Forensics Protection:**
> Never store keyfiles on the internal drive of the host machine. Keyfiles must be hosted exclusively on external portable media — such as a standard SD card equipped with a hardware Write-Protect switch.

Before inserting the SD card into the host system card reader to mount a container, always set the physical **Lock** slider to the write-protected position.

Why is this necessary? Computer forensics suites meticulously audit file access timestamps (`atime`) on seized storage media. If the drive operates in standard read-write mode, opening the container causes the host operating system to automatically update the keyfile metadata, leaving a fresh access timestamp behind.

During forensic examination of an SD card where only a few files out of thousands share access timestamps matching suspected activity windows, analysts can rapidly isolate which files served as VeraCrypt keyfiles. Physically locking the SD card write switch guarantees the memory controller cannot alter a single byte of metadata, completely obscuring access history.

**Chapter Asset:** *_assets\images\11_veracrypt*

## Real-World Threat Modeling: Why Paranoia Must Be Systemic:

To permanently reinforce our operational procedures across artifact sanitization, steganography, encryption, and hidden `VeraCrypt` containers, let us analyze a classic scenario from the real-world practice of independent investigators and activists operating under harsh authoritarian and military regimes.

Consider a targeted journalist under heavy surveillance by local intelligence services. He reviewed our deployment guide and executed everything technically flawlessly: deployed Ubuntu on top of an encrypted LUKS pool, stashed his operational archives inside a hidden, dual-header `VeraCrypt` container, locked down the network stack behind a firewall Kill Switch, and accesses the network strictly through chains of encrypted VPN tunnels. From a host protection standpoint, his machine is an impenetrable digital fortress. If raid teams breach his location and seize the physical hardware, it won't yield a single byte of data.

However, our journalist makes a single fatal operational mistake. He mounts the hidden container, extracts an exposure text document or a fresh screenshot of a classified site, and uploads it publicly, sends it via a messenger, or publishes it on an independent media mirror — assuming his VPN routing and drive encryption grant total immunity.

A few hours later, a tactical team knocks on his door.

**How did this happen, and why did the fortress collapse?**

The adversary didn't need to crack his LUKS partition or attempt key recovery against VeraCrypt. They simply downloaded his published file and conducted basic OSINT metadata analysis. Embedded inside the asset were:

* Hidden application artifacts: username, workstation hostname, local file paths, edit history, and other internal document format fields.
* Precise hidden EXIF save timestamps, which intelligence agencies instantly cross-referenced against ISP logs and network activity timing at a specific gateway.
* Embedded GPS coordinates and camera sensor serial numbers (in the case of a photograph).

This tragic case proves that local disk encryption and network anonymity are completely neutralized if the transmitted payload itself broadcasts host digital signatures to the outside world. This is precisely why we must secure the security perimeter holistically.

Operational hygiene leaves no room for compromise. Stay vigilant and control every byte!

<br>

## Using Yubico Security Keys

#### Introduction:

A vital aspect of ensuring privacy and local host security is integrating hardware authentication factors — physical security keys connected via the computer's USB ports (both Type-A and Type-C form factors).

The most ubiquitous and time-tested hardware keys in the cybersecurity industry are manufactured by Yubico. For our operational requirements, any model with hardware support for the FIDO U2F standard is fully compatible (which includes virtually the entire product line). The most accessible entry option is the basic *Yubico Security Key*. More advanced hardware builds belong to the *YubiKey 5* series (including FIPS-validated editions). From the standpoint of PAM subsystem configuration logic, the specific hardware model makes no difference.

#### Installation:

First, we install the requisite libraries and utilities for interacting with the U2F standard:

**1.** We download and deploy the PAM module and current key generation tools:
```bash
sudo apt update && sudo apt install libpam-u2f pamu2fcfg -y
```

**2.** We enter interactive superuser mode (root shell) to execute system-level configurations:
```bash
sudo -i
```

**3.** We create an isolated directory within the system tree to securely store hardware identifiers:
```bash
mkdir -p /etc/Yubico
```

**4.** We bind the hardware key to the current user account using the `$SUDO_USER` variable:
```bash
pamu2fcfg -u $SUDO_USER > /etc/Yubico/u2f_keys
```
*Upon executing command #4, the utility will poll the hardware bus for 15 seconds. If the key is not yet inserted, the terminal may output: "No U2F device available, please insert one now...". At this moment, immediately insert the YubiKey into a USB port and tap the flashing golden contact area on the key itself.*

**5.** We set access permissions on the generated keyfile, permitting read access for the system while prohibiting any modifications:
```bash
chmod 644 /etc/Yubico/u2f_keys
```
Now we configure the core PAM subsystem to request the physical key for all administrative terminal commands, session switches, system logins, and graphical authentication prompts:

**6.** We open the operating system's general authentication configuration file:
```bash
nano /etc/pam.d/common-auth
```

**7.** Inside the file, at the very top **strictly above the first line of commented text**, we prepend the following security rule:
```ini
auth required pam_u2f.so authfile=/etc/Yubico/u2f_keys originuser cue
```

To save the configuration in the `nano` editor, press key combination **«Ctrl + O»** ➔ **«Enter»**, and then **«Ctrl + X»** to exit back to the console shell.

Before closing the active console session, we must verify the entire authentication pipeline in a parallel window to avoid inadvertently locking out the system!

**8.** Without closing the active terminal window, open a parallel window and test the authentication pipeline:
```bash
sudo -i
```

If configured correctly, the system will prompt *Please touch the authenticator*, and our YubiKey will start blinking, requiring a physical touch to drop into a root shell.

Following successful verification, all terminal sessions can be safely closed — our security perimeter is now fully hardened across all access vectors!

> [!WARNING]
> Relying on a single physical token with a strict `required` policy in PAM carries severe operational risk. If that sole YubiKey is lost, physically damaged, or suffers connector wear, access to the operating system will be permanently compromised. We strongly recommend immediately binding a secondary (backup) security key to the profile and storing it in a secure safe.
> 
> To enroll a backup device, remove the primary key, insert the backup token into the USB port, re-enter superuser mode:
> ```bash
> sudo -i
> ```
> 
> and append the backup key hash into our configuration file:
> ```bash
> pamu2fcfg -u $SUDO_USER >> /etc/Yubico/u2f_keys
> ```
> Utilizing the append redirection operator `>>` is critically important! It cleanly appends the secondary device identifier as a new line at the bottom of the existing configuration without overwriting valid primary key data.

#### Implementing a Hardware Kill Switch via Kernel udev Rules:

To achieve ultimate host fortification, we establish a hardware circuit breaker at the Linux kernel level using the `udev` subsystem. Upon emergency withdrawal of the token from the USB port, the system instantly locks the active Ubuntu session, forcibly isolating active runtime environments and purging master keys from memory.

**1.** We create a custom rules configuration file for host USB devices:
```bash
sudo nano /etc/udev/rules.d/80-yubikey-kill.rules
```

**2.** We insert the following execution rule. To ensure the hardware Kill Switch triggers instantly across all token variants (flagship YubiKey 5 devices as well as streamlined Yubico Security Keys) while ignoring false software interface resets, we bind the low-level HID path removal trigger (`0003:1050`) to a dynamic USB bus check via `lsusb`. The session lock command triggers exclusively when the physical hardware disappears from the host ports:
```ini
ACTION=="remove", DEVPATH=="*/0003:1050:*", RUN+="/bin/sh -c '/usr/bin/lsusb -d 1050: || /usr/bin/loginctl lock-sessions'"
```

Save the file in `nano` via **«Ctrl + O»** ➔ **«Enter»**, then **«Ctrl + X»** to exit.

**3.** We reload udev rules at runtime to force the Linux kernel to immediately arm the new trigger:
```bash
sudo udevadm control --reload-rules && sudo udevadm trigger
```

> [!NOTE]
> In the event of a physical breach, raid scenario, attempt to snatch an active laptop, or sudden unauthorized entry into the workspace, a single swift movement pulling the Yubico token from the USB port is all that is required. Within milliseconds, the kernel `udev` subsystem intercepts the interrupt and commands `loginctl` to lock down the active session.

> [!WARNING]
> Because two-factor authentication is configured via PAM, graphical privilege escalation prompts may fail. Should this occur, launch utilities manually from the console (for example: `sudo timeshift-gtk`).

<br>

## Installing and Configuring USBGuard

#### Introduction:

To prevent unauthorized USB devices from connecting to an active Ubuntu host, deploying USBGuard serves as a crucial preventive measure.

Consider a human rights defender operating in an authoritarian country. He is fully aware of digital security risks and has prepared his workstation in advance: deployed Ubuntu on an encrypted LUKS partition, configured a VPN, firewall, YubiKey, and other security primitives. He is convinced that the primary threat stems from network-borne vectors and remote exploitation attempts.

One day, a trusted associate pays him a visit. While the defender steps away for literally a few seconds to brew coffee, the associate seizes the moment to insert a pre-configured USB flash drive into the host. The operating system automatically enumerates and accepts the new USB device, triggering malicious software installation.

Shortly after, confidential documents and sensitive assets are compromised.

**Why did security fail?**

Because physical access to an active system was omitted from the threat model. Disk encryption primarily protects assets while the computer is powered off, a VPN secures the network channel, and a YubiKey resolves hardware authentication tasks. None of these mechanisms independently answer the core question: **which USB devices should the operating system trust by default?**

If connecting an unknown USB device is permitted automatically, an adversary requires only brief physical access to an unlocked host to achieve full compromise.

This exact scenario is what USBGuard addresses. Its objective is to enforce an explicit whitelist of authorized USB devices while denying all non-whitelisted hardware under the core security principle of **«deny everything not explicitly allowed»**.

Furthermore, modifying the persistent policy must remain a strictly administrative operation. An unprivileged user sitting at the workstation must not be capable of simply plugging in an unknown device and approving it via a GUI prompt.

While this does not render the system invulnerable nor eliminate every physical access vector, it effectively seals one of the most accessible attack vectors: weaponizing an unattended active host by inserting unauthorized USB hardware.

Below, we cover the installation and configuration of USBGuard to establish a minimal policy where only explicitly authorized devices are trusted by the OS kernel.

#### Installation and Setup:

**1.** We install USBGuard:
```bash
sudo apt update && sudo apt install usbguard -y
```

**2.** We verify the version of the installed utility and inspect package details:
```bash
apt policy usbguard
```

> [!WARNING]
> Upon starting USBGuard, any newly connected USB devices lacking an explicit `allow` rule will be instantly blocked. Before starting the service, ensure the pre-configured YubiKey remains connected (unless a hardware Kill Switch is deployed). After starting, verify policy functionality using a secondary flash drive or another non-critical device.

**3.** We enable USBGuard at boot and immediately audit the daemon status:
```bash
sudo systemctl enable --now usbguard && systemctl status usbguard --no-pager
```

**4.** We open the USBGuard configuration, which dictates how the daemon handles both connected and newly inserted USB devices:
```bash
sudo nano /etc/usbguard/usbguard-daemon.conf
```

**5.** Clear the contents of the file using **«Ctrl + K»** and populate it with the following directive suite:
```ini
RuleFile=/etc/usbguard/rules.conf
RuleFolder=/etc/usbguard/rules.d/
ImplicitPolicyTarget=block
PresentDevicePolicy=apply-policy
PresentControllerPolicy=keep
InsertedDevicePolicy=apply-policy
AuthorizedDefault=none
RestoreControllerDeviceState=false
DeviceManagerBackend=uevent
IPCAllowedUsers=root
IPCAllowedGroups=root
IPCAccessControlFiles=/etc/usbguard/IPCAccessControl.d/
DeviceRulesWithPort=false
AuditBackend=FileAudit
AuditFilePath=/var/log/usbguard/usbguard-audit.log
HidePII=false
```

**6.** To manage policy rules and authorize new hardware, we access the `rules.conf` configuration file:
```bash
sudo nano /etc/usbguard/rules.conf
```

Meticulously audit which hardware devices are authorized under the active policy. If necessary, strip unneeded entries from the whitelist. For example, a laptop's integrated webcam can be blocked simply by removing its corresponding rule entry.

**7.** We verify that unprivileged users cannot interface with the IPC channel:
```bash
usbguard list-devices
```
The terminal must output an access denial error: `ERROR: IPC connect: service=usbguard: Operation not permitted`

Next, we walk through a straightforward workflow for whitelisting a new device while testing USBGuard policy enforcement. Insert an unlisted USB flash drive or secondary YubiKey into an available USB port.

**8.** We open the rules configuration for editing:
```bash
sudo nano /etc/usbguard/rules.conf
```

Locate the new device within the listed directives — which USBGuard blocked due to the absence of a permissive rule — and toggle its status flag from `block` to `allow`.

**9.** We restart the daemon to enforce the revised configuration:
```bash
sudo systemctl restart usbguard
```

Following the service restart, the newly configured device successfully transitions to an authorized state and becomes accessible to the operating system.

<br>

## Installing the KeePassXC Local Password Manager

#### Introduction:

To establish secure, centralized storage for all generated system passwords, cryptographic keys, GRUB bootloader passphrases, and online credentials, we will configure the local offline password manager KeePassXC. The application's core database is an encrypted container file backed by the robust AES-256 cipher standard. Depending on hardware availability and operational security requirements, one of three key protection scenarios can be selected.

#### Vault Protection Scenarios:

* **«Basic» Scenario:** Securing the database exclusively with a master passphrase. The primary operational risk: if an adversary obtains the `.kdbx` file and covertly captures the master password (e.g., via a hidden keylogger), the entire vault becomes fully compromised.
* **«Advanced/Two-Factor» Scenario:** Hardening the master passphrase with a unique keyfile (*Keyfile*). Any existing file (an image, audio file, or document) can serve as a keyfile, or one can be generated randomly directly within the software.

> [!WARNING]
> The optimal strategy is storing the keyfile on a separate external physical medium (such as an encrypted flash drive or SD card) and connecting it to the host strictly when opening the database. Storing the keyfile in the same directory as the `.kdbx` vault file is strictly forbidden! If no external media is available, any third-party, deeply hidden file that is guaranteed never to undergo modification (such as a specific personal photo, PDF manual, or MP3 track) may be used. Modifying even a single byte or metadata attribute within this file permanently locks the encrypted container. When utilizing this method, a secondary backup of the keyfile must be archived to an independent storage location to prevent accidental deletion or corruption.

* **«Ultimate» Scenario:** Hardening the master passphrase with a YubiKey hardware token operating via the low-level Challenge-Response (HMAC-SHA1) algorithm. This specific deployment requires a hardware key from the *YubiKey 5 Series* (or YubiKey 4). The entry-level *Yubico Security Key* series (typically blue hardware units) is completely incompatible, as it lacks the underlying HMAC-SHA1 cryptographic response feature.

#### Installing the Software Suite:

Once network interfaces, encrypted VPN gateways, and local package indexes are fully updated, open the terminal and execute the deployment.

**1.** We add the developers' official PPA repository to pull the latest, most secure build of KeePassXC:
```bash
sudo add-apt-repository ppa:phoerious/keepassxc -y
```

**2.** We download and deploy the password manager, the token console management utility, and the secure clipboard sanitization library in a single command (the package index updates automatically upon adding the PPA):
```bash
sudo apt install keepassxc yubikey-manager xclip -y
```
> *(The `xclip` package is deployed pre-emptively so KeePassXC can forcibly flush the system clipboard via a dynamic timer following password copying, neutralizing memory-scraping clipboard hijackers).*

#### Creating and Hardware-Securing the Database:

**1.** Launch the application through the standard GNOME application menu (or by entering `keepassxc` into the terminal console).

**2.** In the initial graphical splash window, click **Create new database**.

**3.** Enter an arbitrary name for the database file (e.g., `vault`) and click **Continue**.

**4.** Leave the cryptographic parameters at their default values during the encryption setup step. Click **Continue**.

**5.** In the **Master Password** setup window, enter a primary passphrase at least 16–20 characters in length (when using a YubiKey hardware token, the character length requirement can be significantly relaxed), ensuring it is memorized securely.

* If configuring the **«Basic» Scenario:** Ignore additional parameters, leave extra fields unselected, and proceed directly to Step 11.
* If configuring the **«Advanced/Two-Factor» Scenario:** Proceed to Step 6.
* If configuring the **«Ultimate» Scenario:** Proceed to Step 9.

**6.** Enable the **Key file** checkbox, click **Add Key File**, and select **Create** from the dropdown menu to generate a new randomized cryptographic sequence (or select the path to an existing, static disguise file).

**7.** Upon generating a new key, the application will prompt for a save destination. Connect external removable media or an SD card and save the file under a neutral file name.

**8.** Click **Continue** and proceed directly to Step 11.

**9.** Click **Add YubiKey Challenge-Response**.

**10.** Program Slot #2 for offline cryptographic calculations (or audit its status). If the hardware token is brand new, initialize Slot #2 in the terminal via `ykman otp chalresp --generate 2`. If the key is already utilized for authenticating an existing KeePassXC database via Slot #2, **DO NOT RE-GENERATE** the secret, or the existing seed will be permanently overwritten! The application will immediately discover the token attached to the USB port. Click **Continue**.

**11.** The application will prompt to save the resulting database file with the `.kdbx` extension. Select a secure target destination (e.g., the root of the home directory `~/vault.kdbx`).

> [!NOTE]
> Integrating a YubiKey hardware factor (HMAC-SHA1) fundamentally transforms the security baseline. Even if the master passphrase is only 8 characters long, offline brute-force attacks via GPU clusters or ASIC farms become computationally irrelevant. Without physical access to the connected hardware token, adversaries are forced to brute-force a hidden 160-bit cryptographic response payload generated by the chip, which is mathematically impossible within reasonable physical timeframes. The sole remaining attack vector in this scenario is live keylogging on a compromised host — precisely why we build our isolated host architecture.

#### Deep Hardening of Internal Security Settings:

Navigate to **Tools** ➔ **Application Settings** and forcibly enable the following security directives:

* **Security** tab ➔ **Timeouts** sub-section:
* **Clear clipboard after** — set strictly to *5–10 seconds* (this triggers the `xclip` utility).
* **Lock database after inactivity** — enable and set strictly to 600 seconds (10 minutes).
* **General** tab ➔ **Entry Management** sub-section:
* **Hide window when copying to clipboard** — enable to immediately minimize the application to the system tray upon pressing **«Ctrl + C»**.

> [!WARNING]
> Refrain from installing any third-party browser extensions (including the official KeePassXC-Browser) inside your Firefox instance. First, browser extensions run within the shared context of the WebExtensions API, introducing potential attack surface vectors such as Cross-Site Scripting (XSS) and credential theft from an unlocked database. Second, our hardened operational security configuration (`privacy.resistFingerprinting = true`) inside Firefox intentionally restricts local Unix domain socket IPC communication required by extension bridges. The chosen approach for a sovereign host environment relies on native clipboard transfers combined with automated sanitization.

#### Secure Data Entry via Protected Clipboard:

Because the graphical subsystem in Ubuntu 24.04 LTS runs on top of the **Wayland** display server protocol, global keyboard event simulation (Auto-Type) is restricted by kernel-level security architecture (applications are prohibited from injecting keystrokes into external windows). By avoiding vulnerable browser plugins entirely, we utilize the native secure data transfer model via the clipboard protected by `xclip`.

**1.** Configure rapid copying: in the primary application menu, navigate to **Tools** ➔ **Settings** ➔ **General** tab. Under **Entry Management**, activate the **Copy data on double clicking field in entry view** checkbox and click **OK**.

**2.** Transfer credentials: navigate to the target website inside Firefox, switch focus to the KeePassXC application window, and **double-left-click** the desired password entry line.

**3.** The application will instantly copy the secret to the clipboard and automatically minimize to the system tray, returning operational focus to the browser window. Paste the credentials into the target site's input field using **«Ctrl + V»**.

> [!NOTE]
> Thanks to the `xclip` system utility deployed earlier, copied credentials remain cached in system RAM strictly for **5–10 seconds** (governed by the timeout defined in the Security tab), after which host memory space allocated to the clipboard is forcibly purged to absolute zero, eliminating data interception risks from background memory scrapers.

**Chapter Asset:** *_assets\images\12_keepassxc*

<br>

## Installing and Running the Wireshark Network Analyzer

#### Introduction:

Deep auditing, logging, and real-time network packet analysis are conducted using Wireshark. It allows full inspection of network packet payloads across all layers of the communication stack. It is an extremely powerful tool, and providing a detailed overview of its full feature set and analysis methodologies would require an entire textbook. Within the scope of this deployment guide, we focus on inspecting active connections through its accessible graphical interface. Through the GUI, operators can visually audit exactly which IP addresses and ports are utilized to transmit and receive host traffic. Any suspicious, undocumented, or non-recommended IP destinations should be immediately added to firewall blacklists. Advanced instructions and packet dissection examples are available in specialized technical documentation on verified IT resources, such as `varonis.com`, `sans.org`, or the official reference community `ask.wireshark.org`.

#### Installing and Launching Wireshark:

> [!WARNING]
> **Warning!** Before proceeding, verify that you have exited the persistent superuser shell (via the `exit` command) and that the command prompt displays the standard non-privileged `$` symbol. The installation workflow must be executed strictly under an unprivileged user context.

**1.** We launch the network analyzer installation:
```bash
sudo apt install wireshark -y
```

During package deployment, the APT package manager will display an interactive terminal dialog asking a critically important question: *«Should non-superusers be able to capture packets?»*. Use the keyboard arrow keys to strictly select **«Yes»**.

**2.** We append the current user account to the system `wireshark` group:
```bash
sudo usermod -aG wireshark $USER
```

**3.** To apply new group memberships without terminating the active session, we require the `newgrp` utility. On Ubuntu 26.04, it is provided by the `util-linux-extra` package, so we deploy it:
```bash
sudo apt install util-linux-extra
```

To force group membership changes to take effect immediately — without rebooting the system or restarting the entire desktop session — we execute the environment re-initialization command:

**4.** We update access privileges for the active terminal window:
```bash
newgrp wireshark
```

> [!NOTE]
> **Author's Note:** The `newgrp` command updates access privileges exclusively within the active terminal window. Across newly spawned console windows, updated privileges will take effect automatically only after a full system reboot or session restart.

**5.** We launch the analyzer's graphical interface under the unprivileged user account:
```bash
wireshark
```

#### Critical Security Concept: Packet Capture Subsystem Security:

The operational rationale for adding the user account to the system `wireshark` group is to completely eliminate running Wireshark via `sudo`. This analytical suite comprises millions of lines of complex C/C++ code, featuring dissectors for hundreds of network protocols. Historically, critical vulnerabilities — including Remote Code Execution (RCE) — are regularly discovered within these dissectors. If the GUI is launched with root privileges, any maliciously crafted packet arriving at the network interface from an external network could instantly execute arbitrary code with maximum system privileges. Running the application strictly as an unprivileged user via an isolated dedicated group is a fundamental global security standard.

#### Stealth Traffic Capture (Headless Console Mode):

If you need to rapidly capture network activity logs without spawning a heavy graphical user interface (for instance, to avoid de-cloaking monitoring activities to onlookers or to preserve system RAM), we utilize its command-line counterpart:

**1.** We install `tshark`, the console utility for packet capturing and deep network analysis:
```bash
sudo apt install tshark
```

**2.** We initiate covert packet capture on the secure VPN interface, saving the output to a dump file (replace the network interface name if yours differs or if a VPN is not active):
```bash
tshark -i tun0 -w ~/Downloads/dump.pcap
```

This command silently captures all network traffic passing through the protected `tun0` VPN interface into the `dump.pcap` capture file located in the user's Downloads directory. The resulting dump file can subsequently be opened and thoroughly analyzed inside the graphical Wireshark GUI at any convenient time.

#### Practical Wireshark Field Guide:

After installing Wireshark, do not attempt to immediately decipher every single field within each packet. During the initial phase, our goal is simply to grasp the general structure of network exchanges and learn how to locate specific events of interest.

Upon launching the application, select the active network interface carrying host traffic and initiate the capture session. On a physical host, this is typically Ethernet or Wi-Fi, while deploying a VPN will introduce a virtual interface such as `tun0`.

Once the capture starts, a live packet list populates the top pane. Each row corresponds to a single packet, with key columns providing an immediate snapshot of its origin:

* **No.** — Sequential packet number in the active capture session;
* **Time** — Timestamp of packet arrival relative to capture commencement;
* **Source** — Originating host IP address;
* **Destination** — Target host IP address;
* **Protocol** — Top-layer network protocol identified by Wireshark;
* **Length** — Total packet size in bytes;
* **Info** — Concise summary of packet contents or operational flags.

For instance, a captured frame summary line might read: *70   40.244944613   192.168.1.119   104.18.32.47   TCP   54 56042 → 443 [ACK] Seq=19884 Ack=1062 Win=802 Len=0*

Breaking down this structure segment by segment:

* 70 — Sequential packet index within the active capture session.
* 40.244944613 — Arrival timestamp relative to recording initialization.
* 192.168.1.119 — Source IP address (the local host machine).
* 104.18.32.47 — Destination IP address (the remote endpoint engaged in communication).
* TCP — Underlying transport layer protocol.
* 54 — Frame payload size in bytes.
* 56042 → 443 — Source and destination TCP ports. Port 56042 represents an ephemeral port allocated on the local host, while port 443 denotes standard HTTPS traffic.
* [ACK] — TCP Acknowledgement frame. No user-level application payload is transmitted here; this packet strictly acknowledges a previously received segment.
* Seq=19884 — TCP sequence number tracking this payload stream segment.
* Ack=1062 — Next expected sequence byte number from the remote endpoint.
* Win=802 — Currently advertised TCP receive window size.
* Len=0 — Payload length within this specific TCP segment is zero. This represents operational transport control overhead rather than website content payload.

**Dissecting Individual Packets:**

Selecting any individual packet expands its internal encapsulation hierarchy within the lower inspection pane. Wireshark structures packet metadata into stacked operational layers.

A standard TCP packet typically comprises the following layer stack:

* Frame
* Ethernet II
* Internet Protocol Version 4
* Transmission Control Protocol
* Application Protocol

Each layer encapsulates specific network communication data:

* **Frame** contains capture-level metadata: frame index, precise timestamp, total length, and capture parameters.
* **Ethernet II** exposes Data Link layer metadata, detailing source and destination hardware MAC addresses.
* **Internet Protocol Version 4 (IPv4)** exposes Network layer attributes: sender and recipient IP addresses, Time-to-Live (TTL) values, and routing parameters.
* **Transmission Control Protocol (TCP)** details Transport layer attributes: source/destination ports, sequence/acknowledgement numbers, and control flags.

When inspecting UDP traffic streams, the Transport layer section reflects **User Datagram Protocol** attributes instead of TCP parameters.

**Understanding Core TCP Flags**

During TCP stream analysis, tracking essential operational flags is critical:

* **SYN** — Initiates TCP connection establishment;
* **SYN, ACK** — Response acknowledging connection establishment requests;
* **ACK** — Confirms receipt of transmitted data segments;
* **FIN** — Signals graceful connection termination;
* **RST** — Abruptly resets or aborts an active connection;
* **PSH** — Instructs the receiving stack to push buffered data directly to the application layer.

Note that occasional `RST` flags or retransmitted segments should not automatically be flagged as an active attack. Operating system network stacks routinely encounter packet drops, connection timeouts, and standard session terminations.

**Auditing IP Addresses and Port Mappings**

When auditing active connections, inspect both IP addresses and associated transport ports: *192.168.1.15:41832 → 9.9.9.9:53* indicates that a local application bound outgoing ephemeral port `41832` to communicate with remote port `53` (standard DNS resolution). Similarly, *192.168.1.15:52314 → 142.250.x.x:443* reflects an outbound session routed to a remote host over TCP port `443` (standard HTTPS).

Port designations alone do not definitively guarantee the underlying application protocol; they represent standardized networking conventions between communicating endpoints.

**Auditing DNS Traffic**

Filtering for DNS traffic offers an effective starting point for baseline auditing. Enter **dns** into the display filter bar. Wireshark will isolate packets recognized as domain resolution queries. You will observe request pairs such as *Standard query A example.com* alongside responses such as *Standard query response A 93.184.216.34*. This audit reveals domain resolution targets generated by the system. To isolate queries for a specific domain, apply the filter: **dns.qry.name == "example.com"**. This proves invaluable when auditing newly deployed software: launch the application, inspect generated DNS queries, and cross-reference them against expected network endpoints.

**Filtering Traffic Streams**

Wireshark allows rapid dataset narrowing using display filters: *ip.addr == 9.9.9.9* isolates packets associated with the specified IP address. *ip.src == 192.168.1.15* isolates traffic originating strictly from that host address. *tcp.port == 443* isolates TCP traffic linked to port `443`. *udp.port == 53* filters for UDP traffic utilizing port `53`. Logical operators allow combining criteria for targeted isolation: **ip.addr == 192.168.1.15 && tcp.port == 443**. These targeted filters allow operators to narrow broad packet captures down to specific session streams.

> [!TIP]
> Do not attempt to memorize complex display filter syntax initially. Mastering a few core directives is sufficient for basic operational audits: `ip.addr`, `ip.src`, `ip.dst`, `tcp.port`, `udp.port`, and `dns.qry.name`.

**Inspecting Encrypted HTTPS Streams**

When navigating to a website over HTTPS, Wireshark captures connection establishment, remote server IP addresses, target ports, and TLS handshake negotiations, while the underlying HTTP application payload remains fully encrypted.

Captured sessions will display sequences such as: *TCP*, *TLS Client Hello*, *TLS Server Hello*, and *TLS Application Data*.

The presence of *TLS Application Data* packets does not imply Wireshark can read the underlying payload. Without master decryption keys and specialized configurations, TLS payload data remains cryptographically secure. Keep this fundamental rule in mind during packet audits: **Wireshark exposes network communication flows, but cannot decrypt protected payload contents without proper key material.**

**Practical Verification Workflow**

To gain practical familiarity with packet analysis mechanics, execute this basic operational experiment:

**1.** Initiate packet capture on the active network interface.  
**2.** Launch the web browser.  
**3.** Navigate to a known website.  
**4.** Allow traffic to flow for a few seconds, then stop the capture.  
**5.** Apply the display filter: **dns**  
**6.** Audit which domain names were resolved during the session.  
**7.** Clear the display filter bar and enter: **tcp.port == 443**  
**8.** Inspect the HTTPS connection streams initiated following site navigation.  

Select any captured frame and expand its protocol stack layers. This practical exercise demonstrates how a single user action translates across multiple layers of the operational network stack.

> [!IMPORTANT]
> Wireshark does not automatically determine whether an observed network connection is benign or malicious. It captures raw network telemetry and provides tools for inspection. Classifying a connection as legitimate, unintended, or suspicious requires human analytical context and knowledge of expected software behavior.

Mastering this functional baseline is sufficient for our guide: operators gain the technical capability to independently observe active connections, identify endpoints, verify protocol ports, analyze frame structures, and leverage these insights to audit their hardened host environment.

**Chapter Asset:** *_assets\images\13_wireshark*

<br>

## Installing and Managing the AppArmor Security System

#### Introduction:

Mandatory Access Control (MAC) over the filesystem is implemented via the integrated AppArmor subsystem. It controls hardware resource access and network ports for specific applications. Operating as a low-level Linux kernel enhancement, it strictly confines executed binaries within defined security profiles.

Consider a practical deployment scenario: a PDF viewer application can be completely blocked from accessing external network interfaces while simultaneously denying access to personal user directories.

Under this threat model, the host perimeter remains fortified. Even if a malicious document exploiting a 0-day vulnerability is opened, the exploit code physically cannot read sensitive user directories nor covertly exfiltrate stolen data to a remote command-and-control server.

#### A New Security Paradigm: Kernel Automation:

In Ubuntu 24.04 and 26.04, the AppArmor subsystem transitioned to a deeply automated architecture. In legacy distributions, system administrators were required to manually deploy profile databases and enforce strict containment on critical binaries using commands like `aa-enforce`.

In modern environments, Canonical developers completely removed legacy text profile templates (such as `usr.sbin.resolved`, `usr.sbin.NetworkManager`, or `usr.bin.dumpcap`) from the base installation. Host security has been shifted to deeper low-level kernel mechanisms:

* 1. **System Daemons (`NetworkManager`, `resolved`):** The Linux kernel isolates them out of the box using native `systemd` sandboxing directives and independent Linux namespaces.
* 2. **Network Utilities (`dumpcap`/Wireshark):** During Wireshark deployment, we deliberately selected **`<Yes>`** in the interactive configuration prompt. At that exact moment, the Linux kernel assigned granular system capabilities — specifically **`CAP_NET_RAW`** and **`CAP_NET_ADMIN`** — directly to the `/usr/bin/dumpcap` binary via Linux Capabilities.

> [!NOTE]
> **Author's Security Analysis:** The Linux Capabilities framework allows the packet capture binary `dumpcap` to legitimately intercept traffic from system network interfaces while keeping the process fully unprivileged under standard user permissions. The utility no longer requires dangerous `root` superuser privileges, meaning a potential exploit payload within a captured packet physically cannot compromise the underlying operating system. Attempting to manually enforce a profile on `dumpcap` via `aa-enforce` will return a `Profile not found` error.

Our next strategic task is to isolate heavy user-space applications (browsers, media players, document readers) where external file execution vectors are highest. We will fortify this perimeter in the dedicated sandboxing chapter.

#### Practical Hardening of the AppArmor Subsystem:

To perform deep configuration of audit utilities, open the terminal and execute the following commands:

**1.** We install the official database of extended security profiles:
```bash
sudo apt install apparmor-utils apparmor-profiles -y
```

**2.** Audit active loaded profiles and confined process states:
```bash
sudo aa-status
```

**3.** Force-enable automatic security service initialization during early kernel boot:
```bash
sudo systemctl enable apparmor
```

**4.** Launch the host log parsing and profile analysis utility:
```bash
sudo aa-logprof
```

> [!IMPORTANT]
> On Ubuntu 24.04 distributions, running `aa-logprof` may encounter a fatal parsing error caused by duplicate profile definitions:
> `ERROR: Conflicting profiles for firefox defined in two files...`
> 
> This stems from a conflict between legacy Canonical text profiles and newer kernel policies. To restore the audit tool functionality, isolate the conflicting duplicate profile to a backup directory with a single command:
> ```bash
> sudo mkdir -p /etc/apparmor.d/backup_conflict/ && sudo mv /etc/apparmor.d/firefox /etc/apparmor.d/backup_conflict/ 2>/dev/null || true
> ```
> 
> After isolating the duplicate, re-run `sudo aa-logprof`. The parser will successfully read host logs:
> `Profile: ubuntu_pro_esm_cache_systemd_detect_virt`
> `Capability: perfmon`
> 
> The utility will visually list blocked calls, allowing one-click decisions to allow legitimate calls or keep denials active. Full policy tuning and conflict-free execution of the Firefox browser will be completed in the upcoming Firejail chapter.

<br>

## Installing and Configuring the Firejail Isolated Sandbox

#### Introduction:

To safely execute downloaded files and untrusted assets, we will deploy the Firejail sandboxing framework. It allows operators to isolate web browsers and desktop applications by restricting their access to the filesystem, system hardware resources, network capabilities, and kernel system calls based on defined security profiles.

Firejail is a lightweight SUID sandboxing tool for Linux designed to restrict the runtime execution environment of unprivileged applications.

In this chapter, we will install Firejail, execute previously deployed applications inside the sandbox (Firefox, KeePassXC, Document Viewer, Image Viewer), and install and launch LibreOffice, GIMP, VS Codium, LM Studio, Telegram, Psi+, and Thunderbird. Furthermore, Psi+ and Thunderbird will be configured to interface with OpenPGP (GnuPG). Finally, we will generate convenient desktop launchers for each sandboxed application.

#### Installing Firejail and Preparing the Sandbox:

**1.** We retrieve the current stable build of Firejail from the project's official repository. First, we install the requisite tools, then automatically locate the latest available `.deb` asset and deploy it:
```bash
sudo apt update && sudo apt install -y curl jq ca-certificates

url="$(
    curl -fsSL https://api.github.com/repos/netblue30/firejail/releases/latest |
    jq -r '.assets[] | select(.name | endswith("_amd64.deb")) | .browser_download_url' |
    head -n1
)"

curl -fL "$url" -o /tmp/firejail.deb
sudo apt install -y /tmp/firejail.deb
rm -f /tmp/firejail.deb
```

**2.** We verify the installed Firejail version. Inspect the output specifically for the presence of the `AppArmor support is enabled` flag, as modern Ubuntu installations utilize AppArmor integration to enhance confinement:
```bash
/usr/bin/firejail --version
```

> [!IMPORTANT]
> Starting with Ubuntu 24.04 LTS, AppArmor optionally restricts unprivileged user namespace creation. This is neither an error nor a bug, but an additional kernel-level hardening feature designed to minimize kernel attack surface.
> 
> Under our deployment model, we do not disable global system protections nor rewrite base system profiles manually. First, we verify current kernel state, then leverage native Firejail and AppArmor integration mechanisms.
> 
> Crucial principle: sandboxing framework controls must fortify system security rather than degenerate into an endless chain of manual exceptions that introduce security risks themselves.

**3.** We audit the active restriction status of unprivileged user namespaces:
```bash
sysctl kernel.apparmor_restrict_unprivileged_userns
```
If the kernel outputs:
```bash
kernel.apparmor_restrict_unprivileged_userns = 1
```

This confirms that enhanced AppArmor namespace restriction is active. We leave this protection enabled.

#### CCore Firejail Filtering Options (Reference):

* **`--apparmor`** — Enforces an AppArmor profile to restrict application actions at the Linux kernel level. Firejail initializes namespaces while AppArmor applies mandatory access controls.
* **`--blacklist`** — Forcibly hides specified files or directories from the application environment.
* **`--caps.drop all`** — Drops all Linux capabilities, restricting access to privileged kernel operations.
* **`--deterministic-shutdown`** — Ensures clean sandbox termination alongside child processes once the main application process exits.
* **`--dbus-user=none`** — Disables application access to the user session D-Bus. Applied for strict isolation of software that does not require desktop environment inter-process communication.
* **`--dbus-system=none`** — Disables application access to the system D-Bus bus.
* **`--net=none`** — Completely disables the kernel network stack inside the container, retaining only loopback access (`127.0.0.1`).
* **`--nonewprivs`** — Disallows processes from acquiring new privileges inside the container via `NO_NEW_PRIVS`. Prevents privilege escalation to root.
* **`--no-sandbox`** — Disables an application's internal Chromium/Electron sandbox when wrapped in an external sandbox (such as Firejail) to prevent isolation mechanism collisions.
* **`--private`** — Replaces real user home directories with clean temporary mountpoints in RAM (`tmpfs`).
* **`--private-dev`** — Spawns an isolated, virtualized `/dev` device directory.
* **`--private-etc`** — Generates an isolated `/etc` view containing strictly essential system files and configurations.
* **`--private-tmp`** — Completely isolates the temporary system directory `/tmp` from the host OS.
* **`--protocol`** — Restricts application socket creation to specific Unix socket types and network protocols within the sandbox.
* **`--seccomp`** — Enables Linux kernel Secure Computing Mode, blocking dangerous or non-standard system calls. If a rule violation occurs, the kernel immediately kills the process.
* **`--whitelist`** — Grants explicit read-write access exclusively to the specified file or directory path.

#### Creating a Dedicated Hardened Firefox Profile:

Following Firejail deployment, we proceed with preparing our dedicated, isolated Firefox profile.

By default, Firejail includes a pre-configured profile for Firefox. Instead of editing the system file at `/etc/firejail/firefox.profile`, we generate our own custom user-level override file. This approach allows us to retain Firejail's baseline security directives while enabling our custom modifications without risk of being overwritten during system package updates.

**1.** We create the user Firejail profile directory and copy the default Firefox profile into it:
```bash
mkdir -p ~/.config/firejail && cp /etc/firejail/firefox.profile ~/.config/firejail/firefox-hardened.profile
```

**2.** We open our profile file for inspection and custom fine-tuning:
```bash
nano ~/.config/firejail/firefox-hardened.profile
```

**3.** We replace the line `include firefox.local` with our custom local configuration file `firefox-hardened.local`:
```ini
include firefox-hardened.local
```

Inside, we fully preserve Firejail's default profile architecture. Redesigning it from scratch is unnecessary, as maintainers have already baked in essential constraints:

* seccomp system call filtering;
* capability dropping (`caps.drop all`);
* strict filesystem access restrictions;
* D-Bus filtering;
* baseline hardening inclusion templates.

We will store all our supplemental security directives separately within a dedicated local file.

**4.** We create the local rules file for our hardened Firefox setup:
```bash
nano ~/.config/firejail/firefox-hardened.local
```

**5.** We define strictly necessary permissions for our Firefox profile:
```ini
# Supplemental hardened Firefox directives

# Permit FIDO2/U2F hardware security keys (YubiKey and equivalents)
ignore nou2f

# Grant explicit access to the isolated Firefox profile directory
noblacklist ${HOME}/.mozilla-hardened
whitelist ${HOME}/.mozilla-hardened

# Grant write access for file downloads
whitelist ${HOME}/Downloads

# Force immediate sandbox teardown upon primary process exit
deterministic-shutdown
```
To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

Now we have a custom user Firejail profile for Firefox that operates completely independent of system defaults and remains immune to package updates.

We will avoid using the standard browser profile path directly. Instead, we generate a dedicated directory at `~/.mozilla-hardened` reserved exclusively for our active Firefox profile. This completely isolates the browser configuration from the rest of the user home directory, establishing a transparent structure that is easy to audit inside the sandbox.

**6.** We create the dedicated directory and copy our current Firefox profile into it:
```bash
mkdir -p ~/.mozilla-hardened && cp -r ~/.config/mozilla/firefox ~/.mozilla-hardened/ 2>/dev/null || true
```

**7.** We audit the contents of the new directory:
```bash
ls -la ~/.mozilla-hardened/firefox/
```
Inside, we verify the presence of our Firefox profile directory formatted as `PROFILE_NAME.default-release`.

**8.** We create a persistent `current` symlink targeting our profile directory:
```bash
cd ~/.mozilla-hardened/firefox/ && rm -f current && ln -s PROFILE_NAME.default-release current && cd ~
```

**9.** We verify that the symbolic link points accurately to our target profile:
```bash
readlink -f ~/.mozilla-hardened/firefox/current
```

If the command returns the full absolute path to the profile directory, we have linked everything correctly.

**10.** We set proper user ownership across the copied profile hierarchy:
```bash
chown -R $USER:$USER "$HOME/.mozilla-hardened"
```

Our Firefox environment is now fully prepared for execution within our hardened Firejail perimeter. At this stage, we avoid adding overly complex manual rules or breaking native security primitives. Testing various launch parameters confirms that previous sandbox issues stemmed not from Firejail or AppArmor errors, but from the process execution wrapper.

In the end, our working architecture consists of:

* baseline Firejail profile defaults with all default restrictions;
* isolated Firefox profile data;
* a secured `~/.mozilla-hardened` filesystem path;
* guaranteed container cleanup via `--deterministic-shutdown`.

**11.** We launch Firefox using our hardened Firejail profile:
```bash
firejail --profile=firefox-hardened /usr/bin/firefox --no-remote --profile "$HOME/.mozilla-hardened/firefox/current"
```

**12.** Once launched, we open a adjacent terminal window and audit active sandboxes:
```bash
firejail --list
```

The output must clearly display our active Firefox session: `PID:user::firejail --deterministic-shutdown --profile=firefox-hardened /usr/...`.

Now, we perform the most critical check: we close the Firefox window normally and wait a few seconds.

**13.** We inspect the active sandbox list once again:
```bash
firejail --list
```

If configured properly, the active sandbox list will return an empty output. This confirms Firejail correctly intercepted the termination signal from Firefox, gracefully killed child processes, and completely destroyed the temporary container namespace.

As a result, Firefox launches with all our custom settings, extensions, and `user.js` preferences intact while benefiting from an additional containment layer. Upon exiting the browser, the sandbox is entirely torn down, returning the host system to its baseline sterile state.

> [!NOTE]
> Previously, under certain Firefox execution patterns, the sandbox process could remain orphaned in memory after closing the browser window. The root cause was not profile corruption or AppArmor misconfiguration, but process-tree termination mechanics inside user namespaces.
> 
> Utilizing `deterministic-shutdown` completely resolves this behavior: Firejail actively tracks child processes and guarantees no lingering sandbox sessions remain after closing the graphical application GUI.

* Toward the end of this chapter, we will establish persistent desktop integration by embedding sandboxing parameters directly into custom `.desktop` application launchers.

#### Airtight PDF Vault: Safely Opening Files in an Isolated Offline Mode:

Because document viewers (PDF and DjVu parsers) are routinely targeted via zero-day exploit payloads, isolating them completely from the host operating system and network stack is a critical task. We will build a true "air-gapped vault" for Evince/Papers — a sterile environment with network access severed completely.

Before executing the launch command, we create or locate a dummy PDF document. Let's assume it resides inside our Downloads directory under the name `unsafe.pdf`.

**1.** If no PDF file is readily available, we generate a dummy file to verify sandbox operations:
```bash
touch ~/Downloads/unsafe.pdf
```

* **Guide for Ubuntu 24.04 LTS Noble Numbat Users (Evince):**

**2a.** On Ubuntu 24.04, we launch the application using the following command:
```bash
firejail evince ~/Downloads/unsafe.pdf
```

**3a.** Without closing the active document window, we open a secondary terminal tab and inspect all running isolated environments:
```bash
firejail --list
```

**4a.** On Ubuntu 24.04, we harden the security rules for Evince by appending directives to `evince.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/evince.local
```

**5a.** We insert the following lines into the Evince local configuration:
```ini
# Complete network ban
net none
protocol unix

# Drop capabilities and disallow privilege escalation
caps.drop all
nonewprivs

# Isolate temporary and cache directories
private-cache
private-tmp

# Retain strictly required directories inside private HOME
private-home Downloads,Documents
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to return to the console prompt.

**6a.** On Ubuntu 24.04, we execute a verification launch of the application:
```bash
firejail evince ~/Downloads/unsafe.pdf
```

* **Guide for Ubuntu 26.04 LTS Resolute Raccoon Users (Papers):**

**2b.** On Ubuntu 26.04, we launch the application using the following command:
```bash
firejail papers ~/Downloads/unsafe.pdf
```

**3b.** Without closing the active document window, we open a secondary terminal tab and inspect all running isolated environments:
```bash
firejail --list
```

**4b.** On Ubuntu 26.04, we harden the security rules for Papers by appending directives to `papers.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/papers.local
```

**5b.** We insert the following lines into the Papers local configuration:
```ini
# Complete network ban
net none
protocol unix

# Drop capabilities and disallow privilege escalation
caps.drop all
nonewprivs

# Isolate temporary and cache directories
private-cache
private-tmp

# Retain strictly required directories inside private HOME
private-home Downloads,Documents
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to return to the console prompt.

**6b.** On Ubuntu 26.04, we execute a verification launch of the application:
```bash
firejail papers ~/Downloads/unsafe.pdf
```

* Toward the end of this chapter, we will establish persistent sandboxed desktop execution by integrating sandbox flags directly into system root launchers.

#### Sandboxing Image Viewer for Secure Media Inspection:

**1.** If no PNG file is readily available, we generate a dummy image asset for operational testing:
```bash
touch ~/Pictures/unsafe.png
```

* **Guide for Ubuntu 24.04 LTS Noble Numbat Users:**

**2a.** We execute the initial launch command:
```bash
firejail eog ~/Pictures/unsafe.png
```

**3a.** Without closing the open image viewer window, we open a secondary terminal tab and inspect active container environments:
```bash
firejail --list
```

**4a.** We harden security directives for Image Viewer by appending local rules to `eog.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/eog.local
```

**5a.** We insert the following lines into the Eog configuration file:
```ini
# Complete network and command shell ban
net none
protocol unix
caps.drop all
nonewprivs
private-cache
private-tmp
```

**6a.** We execute a verification launch of the application:
```bash
firejail eog ~/Pictures/unsafe.png
```

* **Guide for Ubuntu 26.04 LTS Resolute Raccoon Users:**

**2b.** We execute the initial launch command:
```bash
firejail loupe ~/Pictures/unsafe.png
```

**3b.** Without closing the open image viewer window, we open a secondary terminal tab and inspect active container environments:
```bash
firejail --list
```

**4b.** We harden security directives for Image Viewer by appending local rules to `loupe.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/loupe.local
```

**5b.** We insert the following lines into the Loupe configuration file:
```ini
# Complete network and command shell ban
net none
protocol unix
caps.drop all
nonewprivs
private-cache
private-tmp
```

**6b.** We execute a verification launch of the application:
```bash
firejail loupe ~/Pictures/unsafe.png
```

* Toward the end of this chapter, we will establish persistent desktop integration by embedding sandboxing parameters directly into custom `.desktop` application launchers.

#### KeePassXC Sandboxing Scenario:

By isolating KeePassXC inside Firejail, we transform a program running in shared user space into an autonomous offline vault. It interfaces with the outside environment exclusively via Unix domain sockets (to detect our YubiKey hardware token) while exposing only one specific target asset — our password database. The rest of the host filesystem remains invisible to the process.

Kernel-level seccomp filters, capability dropping (`caps.drop all`), and `ptrace` memory inspection prohibitions native to Firejail profiles completely prevent third-party processes from inspecting KeePassXC memory space or reading its allocated address space.

**1.** We create a clean configuration directory (if not already present) and open the local override file for the password manager profile:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/keepassxc.local
```

**2.** We insert the non-conflicting monolithic configuration block. It overrides hidden kernel device blacklists, restores access permissions for USB hardware tokens, enables netlink socket communication for YubiKey Challenge-Response verification, and isolates the main home directory while whitelisting strictly required settings and database files:
```ini
# Permit FIDO2/U2F hardware security keys (YubiKey and equivalents)
ignore private-dev
ignore protocol unix
ignore nou2f

# Permit standard user access groups
ignore groups
ignore nogroups

# Restore access to GTK glycin loader binaries
noblacklist /usr/libexec
whitelist /usr/libexec/glycin-loaders

# Grant explicit access to KeePassXC configuration paths
noblacklist ${HOME}/.config/keepassxc
nowhitelist ${HOME}/.config/keepassxc
whitelist ${HOME}/.config/keepassxc

# IMPORTANT: Grant access to password databases and optional keyfiles.
# Replace placeholder paths with your actual filesystem locations.
# KeePassXC Database path:
# noblacklist ${HOME}/Documents/passwords.kdbx
# whitelist ${HOME}/Documents/passwords.kdbx

# Key-file path (e.g., located on external media):
# noblacklist /media/$USER/DRIVE_NAME/passwords.key
# whitelist /media/$USER/DRIVE_NAME/passwords.key
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to return to the console prompt.

**3.** We launch KeePassXC inside our Firejail sandbox:
```bash
firejail keepassxc
```

> [!IMPORTANT]
> Disabling D-Bus entirely may increase isolation depth, but on modern Linux systems running Wayland display servers, it frequently introduces incompatibilities with GUI applications. Many programs rely on user session D-Bus interfaces and XDG Desktop Portals for secure desktop integration.
>
> If an application fails to launch after completely disabling D-Bus, applying a granular filtering mode is recommended:
>
> ```bash
> --dbus-user=filter
> ```
>
> This mode maintains strict inter-process communication controls: it blocks unauthorized bus calls while preserving core system interfaces necessary for modern graphical application stability.

> [!NOTE]
> The `firecfg` utility generates binary symlinks exclusively for standard software installed via system `.deb` packages or compiled from source. As established in the opening chapters of our guide, Canonical's telemetry-heavy Snap engine was completely removed from the operating system. Firejail achieves its maximum mandatory security potential precisely within our clean baseline setup: classical binary executables deployed via system `apt` alongside standalone, self-contained AppImage containers.

* Toward the end of this chapter, we will establish persistent desktop integration by embedding sandboxing parameters directly into custom `.desktop` application launchers.

#### Installing and Sandboxing the LibreOffice Suite:

Office documents serve as one of the most common vectors for information exchange across organizations. However, the sheer complexity of modern document formats (DOCX, XLSX, ODT) turns office suites into complex parsers of untrusted external data. Therefore, executing LibreOffice within our isolated Firejail environment is strongly recommended, particularly when interacting with files received from untrusted sources.

**1.** We deploy LibreOffice via the system package manager:
```bash
sudo apt install libreoffice -y
```

**2.** We open our custom Firejail profile override using the `nano` editor:
```bash
nano ~/.config/firejail/libreoffice.profile
```

**3.** We insert our hardened runtime security profile:
```ini
# Enforce native GTK3 UI rendering
env SAL_USE_VCLPLUGIN=gtk3

# Filesystem isolation parameters
private-tmp
private-dev

# Whitelist strictly essential workspace paths
whitelist ${HOME}/Documents
whitelist ${HOME}/Downloads
whitelist ${HOME}/.config/libreoffice

# Completely disable networking sockets
protocol unix
ignore protocol inet
ignore protocol inet6

blacklist /tmp/.X11-unix
blacklist ${HOME}/.Xauthority

# Disable D-Bus and unneeded hardware services
nosound

# Kernel security hardening
caps.drop all
nonewprivs
noroot
seccomp

blacklist ${HOME}/.ssh
blacklist ${HOME}/.gnupg
blacklist ${HOME}/.mozilla

# Deny access to external storage media
blacklist /media
blacklist /mnt
blacklist /run/media
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

**4.** We launch the main LibreOffice hub within our sandbox:
```bash
firejail libreoffice
```

**5.** To launch individual components (Writer, Calc, Impress, Draw, Math, Base), we execute:
```bash
firejail libreoffice --writer
firejail libreoffice --calc
firejail libreoffice --impress
firejail libreoffice --draw
firejail libreoffice --math
firejail libreoffice --base
```

* Toward the end of this chapter, we will establish persistent sandboxed execution by embedding these directives directly into custom user `.desktop` application launchers.

#### Installing and Sandboxing GNU Image Manipulation Program (GIMP):

Graphical image editors rank among the most complex user-space applications. GIMP parses a vast array of file formats (PSD, TIFF, PNG, JPEG, SVG, among others) and supports external third-party plugins. Consequently, memory corruption vulnerabilities in image parsers or plugin extensions could potentially lead to arbitrary code execution.

To mitigate exploit risks when opening untrusted graphics assets, we construct a confined runtime sandbox for GIMP. The application operates without network access, stripped of Linux capabilities, and restricted strictly to specified directories.

**1.** We deploy GIMP:
```bash
sudo apt install gimp -y
```

Assume an untrusted graphic asset was downloaded for inspection to `~/Downloads/unsafe.png`.

**2.** We execute the target file within our sandbox environment:
```bash
firejail gimp ~/Downloads/unsafe.png
```

On Ubuntu 26.04, prior to applying a custom local profile, automatic process termination for GIMP 3.x may fail to trigger cleanly. We explicitly enforce `deterministic-shutdown` within our local overrides.

**3.** We harden security controls for GIMP by creating a local profile override:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/gimp.local
```

**4.** We append the following rules to the configuration:
```ini
# Complete network access ban
net none

# Drop all Linux capabilities
caps.drop all

# Preserve dconf and portal interfaces for native file chooser functionality
ignore nodbus
ignore dbus-user none
ignore dbus-system none

# Mute audio subsystem bindings to eliminate PulseAudio terminal warnings
env PULSE_SERVER=disabled

# Override global blacklists for GIMP settings directory
noblacklist ${HOME}/.config/GIMP
whitelist ${HOME}/.config/GIMP

# Restrict filesystem visibility strictly to active workspace paths
whitelist ${HOME}/Documents
whitelist ${HOME}/Downloads
whitelist ${HOME}/Pictures

# Terminate sandbox immediately upon closing the main GIMP UI window
deterministic-shutdown
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

**5.** We perform a verification launch of the application:
```bash
firejail gimp ~/Downloads/unsafe.psd
```

Unlike lightweight document viewers, GIMP does not employ full home directory virtualization (`private`), as it continuously reads user-defined configurations, brushes, plugins, custom fonts, and color profiles.

* Toward the end of this chapter, we will establish persistent desktop launcher integration by embedding sandboxing parameters into `.desktop` files.

#### Installing and Sandboxing VS Codium (Development IDE):

VS Codium is a telemetry-free binary distribution of Microsoft's Visual Studio Code (VS Code) with proprietary tracking components and telemetry removed. It provides an open-source development environment built for privacy. However, like any feature-rich IDE, it maintains extensive filesystem permissions and spawns numerous sub-processes, making strict isolation essential.

**1.** We deploy requisite utilities, navigate to our downloads folder, and retrieve the latest stable VS Codium AppImage build directly from the official GitHub repository:
```bash
sudo apt install curl jq -y && cd ~/Downloads && API_HOST="api.github.com" && LATEST_URL=$(curl -s "https://${API_HOST}/repos/VSCodium/vscodium/releases/latest" | jq -r '.assets[].browser_download_url' | grep -E 'x86_64.*\.AppImage$' | head -n 1) && curl -L -o VSCodium.AppImage "$LATEST_URL"
```

**2.** We grant executable permissions, extract the AppImage archive, relocate binaries to `/opt/`, and initialize configuration paths in our user home directory:
```bash
chmod +x VSCodium.AppImage && ./VSCodium.AppImage --appimage-extract && sudo mv squashfs-root /opt/vscodium && rm VSCodium.AppImage && mkdir -p ~/.config/VSCodium ~/.vscode-oss/extensions && mkdir -p ~/.vscode-oss-shared
```

**3.** We set standard SUID permissions on the embedded Chromium sandbox binary, then recursively assign ownership over configuration directories to our current user via `$USER` (preventing `EACCES: permission denied` errors during extension execution):
```bash
sudo chown root:root /opt/vscodium/usr/share/codium/chrome-sandbox && sudo chmod u+s /opt/vscodium/usr/share/codium/chrome-sandbox && sudo chown -R $USER:$USER ~/.config/VSCodium ~/.vscode-oss ~/.vscode-oss-shared
```

**4.** We ensure our Firejail configuration path exists and open our custom profile:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/vscodium.profile
```

**5.** We add baseline security containment rules. We explicitly whitelist our `extensions` path (preventing extension marketplaces from mounting in Read-Only mode) and include `runuser` and `var` profile templates to prevent embedded Node.js language servers from crashing on startup:
```ini
# Baseline security controls
caps.drop all
netfilter
private-cache
private-dev
private-tmp
disable-mnt

dbus-system none

include disable-common.inc
include disable-devel.inc
include disable-exec.inc
include disable-interpreters.inc

# Whitelist settings, extension stores, and shared memory IPC paths
whitelist ~/.config/VSCodium
whitelist ~/.vscode-oss
whitelist ~/.vscode-oss/extensions
whitelist ~/.vscode-oss-shared

# Permit execution of internal Node.js language servers required by extensions
include whitelist-runuser-common.inc
include whitelist-var-common.inc
include whitelist-common.inc

# Optional rapid teardown flag (retained for asynchronous Electron process management)
#deterministic-shutdown
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

**6.** We create a dedicated directory for our project workspaces:
```bash
mkdir -p ~/Documents/VSCodium_Projects
```

**7.** We correct directory permissions on our primary `Documents` path:
```bash
sudo chown $USER:$USER "$HOME/Documents" && chmod 700 "$HOME/Documents"
```

**8.** We launch the IDE directly inside our terminal session. For complex Electron-based development tools, this launch structure represents our operational standard:
```bash
firejail --profile=~/.config/firejail/vscodium.profile /opt/vscodium/AppRun --no-sandbox
```

> [!NOTE]
> Upon exiting the graphical interface, background Electron services (such as `fileWatcher`) may occasionally keep the container namespace active, preventing our host terminal prompt from returning immediately. Under standard desktop operations, this behavior is resolved by invoking launch routines asynchronously via `.desktop` menu shortcuts.

* Toward the end of this chapter, we will establish persistent sandboxed execution by generating custom `.desktop` launchers.

#### Installing and Sandboxing LM Studio Bionic Local AI:

Cybersecurity professionals should refrain from submitting proprietary source code, system configuration files, or internal log outputs to public cloud-based AI services due to data leakage risks.

Furthermore, vulnerability research demonstrates that malicious payloads can be embedded directly within chat templates inside GGUF format model files.

To neutralize these threat vectors, we contain our local AI workflow inside an air-gapped host perimeter.

Because recent releases of LM Studio are packaged as monolithic AppImage binaries (~1 GB) and native Firejail mounting mechanisms on Ubuntu 24.04/26.04 can produce filesystem mount conflicts (`Invalid argument`), we deploy via pre-extraction.

**1.** We navigate to the Downloads directory and pull the latest stable Linux AppImage build directly from the vendor's distribution endpoint using `curl`:
```bash
sudo apt install curl -y && cd ~/Downloads && curl -L -o LM-Studio.AppImage "https://lmstudio.ai/download/latest/linux/x64?format=AppImage"
```

> [!TIP]
> **Author's Operational Note:** The asset size is ~1 GB; ensure the download transfers completely before we proceed. By targeting the static endpoint URL, this command consistently retrieves the current build of the software.

**2.** We grant executable permissions to the binary asset and extract its filesystem payload:
```bash
chmod +x LM-Studio.AppImage && ./LM-Studio.AppImage --appimage-extract
```

**3.** We move the extracted GUI runtime files into an isolated directory structure under our user profile:
```bash
mv squashfs-root ~/.lmstudio_gui
```

**4.** We ensure our Firejail configuration path exists and open our custom profile:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/lmstudio.profile
```

**5.** We write base containment directives to the profile file:
```ini
# Do not isolate /dev — GPU acceleration and graphic display drivers require hardware device node access
ignore private-dev

# Grant read/write access to model weights and local LM Studio configuration data
noblacklist ${HOME}/.lmstudio

# Force container teardown immediately upon main interface closure
deterministic-shutdown
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

**6.** At this stage, network access is temporarily retained so we can download initial model weights via Hugging Face. To preserve GPU acceleration performance across vendors, we launch the application via a dynamic wrapper. The execution string detects active graphics hardware: if NVIDIA drivers are active, device nodes (`/dev/nvidia*`) remain exposed; otherwise, standard Intel/AMD Mesa graphics stacks are targeted natively:
```bash
firejail --profile=lmstudio ~/.lmstudio_gui/lm-studio --no-sandbox
```

> [!NOTE]
> Once we have completely downloaded the required LLM model files via the embedded search interface, we close the application. Online network access will no longer be required during our routine offline operations. Downloaded model weights are stored persistently within our user home directory under `~/.lmstudio/`. We now proceed to complete our air-gap lockdown.

Detailed setup routines for establishing dual launch modes (*Secure Sandbox* without networking vs. *Online Downloader* with networking) featuring high-resolution 512px and 256px application icons are covered **further in the text under the `firecfg` section**. The automated script provided there generates menu entries within the GNOME desktop interface.

**7.** To execute the graphical interface of LM Studio inside a fully air-gapped kernel namespace (bypassing the application menu), we run the following command with the network stack explicitly disabled (`--net=none`):
```bash
firejail --net=none --profile=lmstudio ~/.lmstudio_gui/lm-studio --no-sandbox
```

**8.** If the GUI interface is not required and we prefer executing only the lightweight local inference engine as a background service (Daemon) for API integration while strictly air-gapped, we run:
```bash
firejail --net=none --profile=lmstudio $HOME/.lmstudio/bin/lms daemon up
```

**9.** We remove the leftover installation AppImage binary from our Downloads directory:
```bash
rm ~/Downloads/LM-Studio.AppImage
```

> [!NOTE]
> **Security Analysis:** Our local LLM platform is fully prepared for operation within an air-gapped sandbox in both graphical (GUI) and server (CLI/Daemon) execution modes. The `--net=none` flag completely unbinds network namespaces within the Linux kernel for our target process. GPU acceleration handles matrix computations locally without exposing host filesystem access. Prompts, system logs, and security code snippets remain confined entirely to local GPU VRAM and host RAM, physically severed from network interfaces.

* Toward the end of this chapter, we will establish persistent sandboxed execution by generating custom `.desktop` application launchers.

#### Securing Communications: Mandatory Isolation of Messengers and Crypto Infrastructure (Author's OPSEC Setup):

For everyday work tasks, regular users choose **Telegram**. However, in the professional information security environment, the standards for privacy, decentralization, and absolute digital sovereignty remain the **XMPP (Jabber)** protocol and encrypted email paired with end-to-end **OpenPGP (GnuPG)** encryption.

> [!NOTE]
> When using ProtonMail secure email, keep in mind that within the "Proton-to-Proton" ecosystem, end-to-end OpenPGP encryption is already built into the web interface by default. However, to achieve full sovereignty (a defense model against the compromise of the email provider itself), we can use a **cascading encryption** tactic: encrypt the message text with our local offline Curve 25519 key directly on the host, and then send the resulting ciphertext via Proton. In this scenario, intercepting correspondence is mathematically impossible, even if a third party gains access to the servers in Switzerland.

Any communication client continuously processes vast amounts of complex external data: HTML code in emails, XML streams in chats, asynchronous links, avatars, and media files from untrusted sources. This opens up a critical attack surface for exploitation of parsing vulnerabilities (including buffer overflow errors in the application core). We completely eliminate the risk of 0-day exploit execution and theft of host personal data by isolating each communication tool at the Linux kernel level using the Firejail sandbox.

#### Installing and Sandboxing Telegram Desktop:

The main issue with the default Telegram client in Linux is that it has full access to our home directory and stores all cached files, media, and session keys in plaintext. If a malicious stealer script executes inside the system, it can easily hijack active messenger sessions.

Let's strictly restrict Telegram: we deny it access to any files in the system except for its own configuration directory and one specific folder for downloads. At the same time, the messenger must maintain full traffic visibility for Portmaster firewall eBPF lenses.

> [!IMPORTANT]
> Since the Snap package base is completely purged in our paranoid OPSEC perimeter, and Flatpak versions have hidden issues with D-Bus passthrough, we will strictly use the official, clean static binary of the messenger. This allows our Firejail sandbox to achieve the highest level of mandatory process control.

**1.** We navigate to our downloads directory, download the official stable messenger archive in a single command directly via the official `telegram.org` gateway, unpack its structure, move the clean executable to the canonical system path directory `/usr/bin/`, and automatically purge all temporary junk behind us:
```bash
sudo apt install curl -y && cd ~/Downloads && curl -L -o telegram.tar.xz "https://telegram.org/dl/desktop/linux" && tar -xvf telegram.tar.xz && sudo mv Telegram/Telegram /usr/bin/telegram-desktop && rm -rf Telegram/ telegram.tar.xz
```

The command executed via our `curl -L` utility will faithfully follow the HTTP redirect of the official download gateway, pull the heavy original tarball of the latest version, extract it, and move the clean static binary to the `/usr/bin/` directory named `telegram-desktop`. This is a legitimate execution path in the Linux kernel, ensuring a conflict-free launch of the executable by our graphical shell.

**2.** To keep files downloaded from chats from scattering across the entire disk, we create a dedicated secure gateway folder in our user directory:
```bash
mkdir -p ~/Downloads/Telegram_Downloads
```

**3.** We ensure executable file integrity (POSIX protection):
```bash
sudo chown root:root /usr/bin/telegram-desktop
```

**4.** We set execution permissions (Principle of Least Privilege):
```bash
sudo chmod 755 /usr/bin/telegram-desktop
```

**5.** We create the directory if it is missing, and open our custom configuration file in the `nano` editor:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/telegram.profile
```

**6.** We write baseline isolation rules into the opened file:
```ini
# Telegram Desktop
seccomp

# Allow only necessary directories
whitelist ${HOME}/.local/share/TelegramDesktop
whitelist ${HOME}/Downloads/Telegram_Downloads
```
To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

**7.** On Ubuntu 24.04/26.04 distributions, default system messenger profiles are bloated with redundant AppArmor filters, causing Qt applications to drop network sockets and go blind before the Portmaster eBPF driver. To completely bypass this bottleneck, we launch Telegram using our ultimate direct command: the `--profile=telegram` parameter completely seals the filesystem perimeter according to our rules. The `--seccomp` mechanism activates system call filtering at the host kernel level, thwarting attempts to exploit local privilege escalation (LPE) vulnerabilities:
```bash
firejail --profile=telegram /usr/bin/telegram-desktop
```

The messenger will instantly gain access to the host's internet network, and Portmaster eBPF lenses will immediately capture and display the `telegram-desktop` process in our network monitor window. At the same time, the built-in messenger file explorer will physically see nothing in our home directory besides our active chats and the isolated `Telegram_Downloads` directory. Even if an attacker sends us a malicious file and we accidentally execute it inside the messenger, the exploit will remain trapped in a virtual memory vacuum, unable to reach our SSH keys, crypto wallets, or hidden host machine system configs!

* Toward the end of this chapter, we will establish persistent sandboxed execution via a desktop shortcut by embedding rules directly into a user `.desktop` file.

#### Host Cryptographic Foundation: Generating and OPSEC-Protecting GnuPG Keys:

Before passing the cryptographic core into isolated sandboxes for messengers and email clients, we must deploy a flawless, mathematically indestructible **OpenPGP (GnuPG)** asymmetric encryption base on the host. Errors during generation or negligence in key file permissions completely invalidate protection, allowing local malware to hijack your digital identity.

> [!NOTE]
> GnuPG tooling is a pre-installed baseline component in our Ubuntu Desktop out of the box. The `apt` package manager continuously uses GPG cryptographic algorithms at a deep system level to verify Canonical repository digital signatures during every system update, so the utility is fully ready to work out of the box.

**1.** We abandon legacy and heavyweight RSA algorithms in favor of modern, lightning-fast, and robust **Elliptic Curve Cryptography (ECC)**. Launch the interactive GnuPG core generator:
```bash
gpg --full-generate-key
```
**Select strictly the following security parameters in the dialog window:**
> 1. **Key type:** Choose option `(9) ECC and ECC (Sign and Encrypt)` — this provides separate elliptic curve keys for signing and encryption.
> 2. **Elliptic curve type:** Select `(1) Curve 25519` (the famous Edwards curve `Ed25519`/`Cv25519`) — the recognized global EdDSA standard, protected against hidden intelligence agency backdoors.
> 3. **Expiration date:** Choose `0` (key does not expire) OR set a strict rotation schedule (e.g., `1y` — one year).
> 4. **User ID:** Enter your name/nickname and email.
> 5. **Passphrase:** The system will prompt for a password to protect the secret key in RAM. Use a generated passphrase **at least 20–24 characters long** (a random set of mixed-case letters, numbers, and special characters).

> [!IMPORTANT]
> If we are creating a completely anonymous communication perimeter, strictly use a fictitious pseudonym and a non-existent email account in a trusted jurisdiction (e.g., `dark_agent@proton.me`).

**2.** By default, the `~/.gnupg` directory is created with permissions that are too soft. If an unprivileged spy script gets into the system, it can read your key metadata. We block this vector by enforcing strict Linux kernel-level POSIX permission masks on the hidden directory and files:
```bash
chmod 700 ~/.gnupg && find ~/.gnupg -type f -exec chmod 600 {} + && find ~/.gnupg -type d -exec chmod 700 {} +
```

> **Defense Physics:** Now the permissions mask looks like an ideal Infosec monolith `drwx------`. Any process launched outside our current user account will receive a hard OS kernel hardware rejection when attempting to look into the key folder: `Permission denied`.

> **(OPSEC Recommendations for Storing Public and Private Pairs):** Asymmetric cryptography separates data into two entities, and the rules for storing them are fundamentally different:

> [!IMPORTANT]
> When executing export commands, replace the demonstration email address `YOUR-EMAIL@DOMAIN.COM` strictly with the actual email personally entered in Step 1 during key generation. Otherwise, the GnuPG core will throw a `WARNING: nothing exported` error.

**3.** Public Key: Our digital business card. Correspondents use it to encrypt messages sent to us and to verify our digital signature. Its security is not secret. We can post it on GitHub, send it as a file in an open chat, or pin it in an XMPP profile description. Exporting the public card to a text file:
```bash
gpg --armor --export YOUR-EMAIL@DOMAIN.COM > ~/Downloads/my_public_key.asc
```

**4.** Export the private key to the Downloads folder:
```bash
gpg --armor --export-secret-keys YOUR-EMAIL@DOMAIN.COM > ~/Downloads/my_PRIVATE_key.asc
```

**MANUAL ACTION:** Copy the `my_PRIVATE_key.asc` file to an external encrypted drive!

**5.** Destroy the temporary key in Downloads using the `shred` secure deletion utility:
```bash
shred -u -v -n 3 ~/Downloads/my_PRIVATE_key.asc
```

> [!WARNING]
> **Private Key:** Our digital life, the DNA of our sovereignty. We use it to decrypt incoming messages and sign our files. It **MUST NEVER** be stored in cloud services, email, or network drives. The original master private key must reside exclusively in Cold Storage — on an encrypted external drive (or inside its crypto-container). Only easily replaceable operational secret subkeys for daily email encryption should be imported onto the LUKS host itself into the hidden `~/.gnupg` directory, eliminating the compromise of your entire digital identity in the event of physical loss or system breach.

> [!NOTE]
> The physics of residual data securely wiped with `shred`/`wipe` utilities, metadata handling in `mat2`, and deployment of **VeraCrypt** crypto-containers were covered in detail in previous chapters. At this stage, we should already have an encrypted offline drive ready, where we copy the private key before physically wiping its original from the downloads folder.

#### Installing and Sandboxing the Psi+ Jabber Client:

For everyday routine tasks, standard users typically choose Telegram. However, in the professional cybersecurity community, the **XMPP (Jabber)** stack coupled with end-to-end encryption remains the benchmark for privacy, decentralization, and absolute digital sovereignty.

As our reference client, we will use **Psi+**. Unlike the heavy Gajim (written in Python with an extensive cascade of third-party dependencies), Psi+ is a native Qt/C++ client featuring a lightweight architecture and built-in XMPP diagnostic tools, including an XML console.

However, any XMPP client continuously processes massive volumes of external XML data, asynchronous links, avatars, and media files from untrusted contacts. Theoretically, this opens a dangerous attack vector for exploiting parsing vulnerabilities (including critical buffer overflow flaws inside the core application binary). We significantly restrict the impact of potential exploit attempts against Psi+ by isolating the client using Firejail.

We outline three legitimate encryption vectors for chat communications depending on our threat model:

* **OMEMO (Modern Standard):** Powered by the Double Ratchet cryptographic protocol (similar to Signal), featuring Forward Secrecy and file transfer encryption. Ideal for daily cybersecurity operations.
* **OpenPGP/GnuPG (Old-School Benchmark):** Asymmetric encryption using robust key pairs. The Psi+ OpenPGP plugin leverages host GnuPG infrastructure to manage OpenPGP keys.
* **OTR/Off-the-Record Messaging:** Absolute symmetric mathematical resistance impervious to quantum cryptanalysis (each key is generated manually and used strictly once per message).

Our objective is to build a universal, resilient sandbox profile that isolates the host filesystem while seamlessly passing through any chosen cryptographic pipeline.

Since we have strict rules enforced in UFW, we will need to add firewall exceptions:

**1.** We open standard XMPP outbound port 5222 to all servers for baseline Psi+ connectivity:
```bash
sudo ufw allow out to any port 5222 proto tcp
```

**2.** Optionally, for servers configured with direct TLS, we open outbound XMPP TLS port 5223 to all destinations to ensure secure transport encryption:
```bash
sudo ufw allow out to any port 5223 proto tcp
```

* **Guide for Ubuntu 24.04 LTS Noble Numbat Users:**

**3a.** The default native package in Ubuntu 24.04 repositories suffers from critical Qt library link errors when interacting with the Wayland display server (resulting in application *Segmentation fault* crashes). To bypass this system bug, we forcibly attach the official PPA repository from Psi+ developers, retrieving a targeted stable build of the messenger (Psi+ v1.5.2068), its plugin bundle (including OMEMO), and the base GnuPG subsystem in a single command:
```bash
sudo add-apt-repository ppa:psi-plus/ppa -y && sudo apt update && sudo apt install psi-plus psi-plus-plugins gnupg -y
```

* **Guide for Ubuntu 26.04 LTS Resolute Raccoon Users:**

In Ubuntu 26.04, the standard repository offers Psi+ version 1.4.1456. The required 1.5.2068 build could not simply be copied from Noble because existing Noble plugins were compiled against outdated ABIs. Therefore, Psi+ 1.5.2068 was recompiled directly on Ubuntu 26.04 Resolute from the source 1.5.2068 release archive. The client and its plugins were then consolidated into a single unified package: `psi-plus-resolute-client-and-plugins_1.5.2068-1~resolute1_amd64.deb`. Consequently, OMEMO, OTR, and OpenPGP utilize native libraries available directly within Resolute without bringing over legacy Noble dependencies.

We have two installation paths available. Option one installs the older yet functional Psi+ v1.4.1456 client directly from the main repository. Option two deploys the updated version compiled specifically for our setup, pulled from the book's author repository on GitHub based on the `noble` release source.

**Option 1:**

**3b1.** We install Psi+ version 1.4.1456 directly from the standard repository in a single command:
```bash
sudo apt update && sudo apt install psi-plus psi-plus-plugins -y
```

**Option 2:**

**3b2-1.** We download the `.deb` package directly from the author repository at `github.com/eugexo`:
```bash
wget https://raw.githubusercontent.com/EugeXo/security-baseline-ubuntu/main/_assets/psi-plus/psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
```

> [!IMPORTANT]
> Before installing the fetched `.deb` package, we will not blindly trust the downloaded archive. We first verify its cryptographic checksum and inspect its contents. While this does not inherently prove the absence of malicious code, it ensures file integrity and gives us full visibility into what we are deploying. **We should apply this verification routine to all untrusted or unofficial sources.**
> 
> We verify the SHA-256 checksum of the package:
> ```bash
> sha256sum psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
> ```
> 
> We inspect `.deb` package metadata prior to installation:
> ```bash
> dpkg-deb -I psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
> ```
> 
> We audit the internal payload structure of the package:
> ```bash
> dpkg-deb -c psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
> ```
> A matching SHA-256 hash confirms the integrity of our downloaded asset against a known reference baseline, though hash verification alone does not serve as absolute proof of software safety. Thus, checksum verification remains one layer of our defense-in-depth inspection, not an exclusive guarantee of trust.

**3b2-2.** After verifying the checksum, we initiate the installation of Psi+. Ubuntu will automatically resolve and pull missing system dependencies required for proper runtime operation:
```bash
sudo apt install ./psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb -y
```

**4.** We launch Psi+ using its canonical system binary execution call. The Firejail sandbox environment will automatically read system default security profiles, apply mandatory security masks, and instantiate the GUI layout:
```bash
firejail psi-plus
```

The Psi+ client allows us to leverage OMEMO, OTR, or OpenPGP to secure our communications. Simultaneously, Firejail mandatory sandbox boundaries restrict application access to our host filesystem, drastically mitigating potential exploit impact should vulnerabilities be targeted within the messenger core.

We deliberately excluded WebKit/WebEngine and other non-essential modules from the custom build process. This yields a streamlined, hardened deployment of Psi+ 1.5.2068 containing the complete suite of default plugins—including OMEMO, OTR, and OpenPGP—without extraneous browser rendering engines or unnecessary attack surface area.

> [!IMPORTANT]
> For out-of-band file transfers, additional outbound network permissions depend on your specific XMPP server deployment and its associated HTTP Upload/proxy services.

* Toward the end of this chapter, we will establish persistent sandboxed execution via a desktop shortcut by embedding rules directly into a user `.desktop` file.

#### Installing and Sandboxing Thunderbird (Encrypted Email Workflow):

Email represents a highly sensitive exposure vector on the host. Modern phishing campaigns and targeted attacks routinely package malicious payloads and hidden scripts inside incoming messages. Running an uncontained email client poses a direct threat of system compromise. We will deploy **Thunderbird** as our reference client, seal its profile storage within an isolated perimeter, and link it cleanly to our OpenPGP cryptographic core.

**1.** The default `thunderbird` package in Ubuntu repositories is a transitional dummy package that forcefully requires the `snapd` subsystem we previously purged. To bypass this system deadlock and instruct our package manager to pull the clean binary directly from the official Mozilla Team PPA, we establish a strict APT priority configuration file:
```bash
sudo tee /etc/apt/preferences.d/mozilla-thunderbird <<EOF
Package: thunderbird*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
Package: thunderbird*
Pin: release o=Ubuntu
Pin-Priority: -10
EOF
```

* **For Ubuntu 24.04 LTS Noble Numbat Users:**
**2a.** We protect our upcoming native package from accidental deletion, rollback, or forced replacement by a Snap dummy package during background system updates:
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:noble";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-mozilla
```

* **For Ubuntu 26.04 LTS Resolute Raccoon Users:**
**2b.** Activate an equivalent system rule for the package base of the 26.04 distribution:
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:resolute";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-mozilla
```

**3.** We update our package repositories and install the native Thunderbird build:
```bash
sudo apt update && sudo apt install thunderbird -y
```

**4.** We create a custom Firejail profile for Thunderbird:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/thunderbird.profile
```

**5.** We write our baseline isolation rules into the opened profile file:
```ini
caps.drop all
nonewprivs

whitelist ~/.thunderbird
whitelist ~/Downloads/Mail_Attachments

# Force container teardown immediately upon application exit
deterministic-shutdown
```

To save changes in `nano`, we press **«Ctrl + O»** → **«Enter»**, then **«Ctrl + X»** to exit.

> [!WARNING]
> **We must not click** the Thunderbird icon while the system is connected to the network. Upon its initial start, the client will immediately transmit baseline telemetry packets across the wire.

**6.** We completely disconnect networking so the email client cannot call home during initialization, then launch Thunderbird to generate its baseline internal profile structure:
```bash
nmcli networking off
```
**After executing the command, we launch Thunderbird manually from our applications menu.** We wait 2–3 seconds while it creates its default directory structure, then close the application completely.

**7.** We navigate into the generated UUID profile directory and instantiate a clean configuration file:
```bash
cd ~/.thunderbird/*default-release && touch user.js
```

**8.** We open our newly created `user.js` in the `nano` terminal editor:
```bash
nano user.js
```

**9.** We copy our ultimate OPSEC array of security settings, completely blinding the Gecko engine's surveillance modules, and paste it entirely into the editor window:
```javascript
// ============================================================================
// HARDENING CONFIG FOR MOZILLA THUNDERBIRD (USER.JS)
// OPTIMIZED OPSEC PROFILE & EMAIL PRIVACY MATRIX
// ============================================================================

// 1. COMPLETE PURGING OF SYSTEM TELEMETRY AND CRASH REPORTING (BREAKPAD)
user_pref("toolkit.telemetry.unified", false);
user_pref("toolkit.telemetry.enabled", false);
user_pref("toolkit.telemetry.archive.enabled", false);
user_pref("toolkit.telemetry.rejected", true);
user_pref("toolkit.telemetry.server", "data:text/plain,");
user_pref("datareporting.healthreport.uploadEnabled", false);
user_pref("datareporting.policy.dataSubmissionEnabled", false);
user_pref("datareporting.healthreport.service.enabled", false);
user_pref("browser.tabs.crashReporting.sendReport", false);
user_pref("toolkit.crashreporter.enabled", false);
user_pref("breakpad.reportURL", "data:text/plain,");
user_pref("security.ssl.errorReporting.automatic", false);
user_pref("network.allow-experiments", false);
// Purge build history and unique profile UUID identifiers (DAU)
user_pref("toolkit.telemetry.cachedClientID", "");
user_pref("toolkit.telemetry.cachedProfileGroupID", "");
user_pref("toolkit.telemetry.previousBuildID", "");
user_pref("datareporting.dau.cachedUsageProfileGroupID", "");
user_pref("datareporting.dau.cachedUsageProfileID", "");

// 2. DISABLE HIDDEN MOZILLA EXPERIMENTS AND NIMBUS STUDIES
user_pref("app.shield.optoutstudies.enabled", false);
user_pref("app.normandy.enabled", false);
user_pref("app.normandy.api_url", "");
user_pref("nimbus.telemetry.targetingContextEnabled", false);

// 3. BASE PRIVACY PROTECTION AND IN-MAIL TRACKER BLOCKING
user_pref("privacy.trackingprotection.enabled", true);
user_pref("privacy.trackingprotection.socialtracking.enabled", true);
user_pref("privacy.trackingprotection.fingerprinting.enabled", true);
user_pref("dom.private-attribution.submission.enabled", false);
user_pref("dom.netinfo.enabled", false);
user_pref("beacon.enabled", false);

// 4. PREVENT BACKGROUND NETWORK PREFETCHING AND DNS PREDICTION
user_pref("network.predictor.enabled", false);
user_pref("network.predictor.enable-hover", false);
user_pref("network.prefetch-next", false);
user_pref("network.dns.disablePrefetch", true);
user_pref("network.dns.disablePrefetchFromHTTPS", true);
user_pref("network.http.speculative-parallel-limit", 0);

// 5. PURGE ADD-ON RECOMMENDATIONS AND MARKETPLACE CACHING
user_pref("extensions.getAddons.cache.enabled", false);
user_pref("extensions.htmlaboutaddons.recommendations.enabled", false);
user_pref("browser.discovery.enabled", false);

// 6. RELOCATE DISK CACHE ENTIRELY TO SYSTEM RAM (SSD WEAR PROTECTION)
user_pref("browser.cache.disk.enabled", false);
user_pref("browser.cache.memory.enabled", true);
user_pref("browser.cache.memory.capacity", 262144);

// 7. ISOLATE PERIPHERALS, START PAGES, AND HOME CALLS
user_pref("mailnews.start_page.enabled", false);
user_pref("mailnews.start_page.url", "about:blank");
user_pref("mail.shell.checkDefaultClient", false);
user_pref("media.peerconnection.enabled", false);
user_pref("media.peerconnection.use_document_iceservers", false);
user_pref("dom.gamepad.enabled", false);
user_pref("device.sensors.enabled", false);

// 8. BLOCK DATA LEAKAGE VECTORS & ENFORCE URL QUERY STRIPPING
user_pref("privacy.query_stripping.enabled", true);
user_pref("privacy.query_stripping.enabled.pbmode", true);
user_pref("layout.css.font-visibility", 1);
user_pref("network.http.referer.XOriginPolicy", 2);

// 9. UI OPTIMIZATION AND WEBRENDER HARDWARE ACCELERATION (GPU LOAD)
user_pref("general.smoothScroll", true);
user_pref("mousewheel.min_line_scroll_amount", 20);
user_pref("gfx.webrender.all", true);
user_pref("dom.ipc.processCount", 8);

// 10. MASK NETWORK FINGERPRINTS & ISOLATE INFRASTRUCTURE CHECKS
// Rebind Gecko's internal connectivity check mechanisms from commercial Cloudflare servers to privacy-focused Quad9 infrastructure. Additionally strip regional telemetry, forcing system locale masking to neutral US baseline.
user_pref("browser.search.region", "US");
user_pref("geo.enabled", false);
user_pref("webgl.disabled", true);
```

To save the configuration in the `nano` editor, we press **«Ctrl + O»** → **«Enter»**, and then **«Ctrl + X»** to exit back to the console.

**10.** We lock down file permissions by applying a strict read-only POSIX mask (`0400`), ensuring no background host process can silently modify our security matrix:
```bash
chmod 0400 user.js
```

**11.** To prevent files downloaded from incoming emails from scattering across the system and silently modifying host files, we initialize a strictly dedicated exchange gateway:
```bash
mkdir -p ~/Downloads/Mail_Attachments
```
**12.** We restore our internet connection (replacing `enp0s1` with your specific interface name):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

**13.** We launch an isolated instance of Thunderbird without using buggy default profiles (the `--noprofile` flag). To prevent heavy email rendering on NVIDIA GPUs from causing interface crashes under Wayland, we wrap the launch in a universal wrapper: the script checks for proprietary drivers in the system and whitelists paths on the fly, while maintaining the default paranoid file perimeter whitelist for Intel/AMD integrated graphics users:

```bash
firejail --profile=thunderbird /usr/bin/thunderbird
```

> [!IMPORTANT]
> *Secure Encrypted Mail Workflow* **(Air-Gapped Setup)**: Since permanently storing a private key on the host or inside the sandbox constitutes a critical security vulnerability, we employ a temporary isolated import tactic in full offline mode:
> 
> **1.** We launch Thunderbird inside the Firejail sandbox to perform an initial fetch and download of encrypted incoming mail from remote servers.
> **2.** We completely disable the host's network interface, bringing the entire system and Thunderbird into an isolated offline state:
> ```bash
> nmcli networking off
> ```
> **3.** We connect our secure external USB drive and copy the key files exclusively into our single open exchange gateway: `~/Downloads/Mail_Attachments`.
> **4.** In the top-right corner of Thunderbird, we click the **hamburger menu**, navigate to **Tools** → **OpenPGP Key Manager** → **File**, and sequentially select **Import Public Key(s) From File** and **Import Secret Key(s) From File**.
> **5.** We import the keys from the gateway, decrypt, and inspect the required confidential emails.
> **6.** After reading, we completely delete the private key from the Thunderbird interface itself.
> **7.** We completely destroy the key files in the exchange directory by executing a 3-pass kernel-level secure wipe tool in the host terminal (for full protection against residual data recovery):
> ```bash
> shred -u -n 3 ~/Downloads/Mail_Attachments/PRIVATE_key.asc
> ```
> **8.** Only after confirming the shredding of cryptographic traces do we restore the host's network connection. In Ubuntu 24.04/26.04 distributions, automatic link re-establishment after severing the network stack often breaks. To restore internet connectivity, we use an explicit command (replacing `netplan-enp0s1` with the name of your physical interface):
> ```bash
> nmcli networking on && nmcli connection up netplan-enp0s1
> ```
> 
> Email traffic remains completely transparent to Portmaster eBPF lenses, but the host filesystem operates under near-complete protection: even if an incoming encrypted message contained a zero-day exploit payload, the attack would completely stall inside the isolated container, lacking any network egress channel for data exfiltration and unable to break through the kernel's Strict Read-Only perimeter!

* Towards the end of this chapter, we will establish persistent sandboxed execution for the application via a desktop shortcut, embedding the execution rules directly into a user `.desktop` file.

#### Automating the Defensive Perimeter (Firecfg Utility) and Customizing System Icons:

Constantly typing long commands manually in the terminal quickly becomes exhausting. To automate this process, we use the built-in `firecfg` tool. It scans the system and automatically wraps the execution of standard applications (browsers, torrent clients, mail agents) inside isolated sandbox containers.

> [!IMPORTANT]
> In modern Firejail releases, local passwordless automation mode has been removed. Running `firecfg` requires superuser privileges because the utility generates global symlinks inside the system directory `/usr/local/bin`.
>
> While `sudo firecfg` is convenient for bulk-enabling Firejail, we do not recommend applying it blindly without reviewing which applications will run inside the sandbox. We favor targeted and controlled isolation—setting up individual profiles and user `.desktop` files strictly for software that actually requires containment.

**1.** We activate the global protective desktop entry perimeter across the system:
```bash
sudo firecfg
```

**2.** To completely eliminate hidden path conflicts, legacy symlink layering, and cascading failures when coexisting with AppArmor, we execute a dual-command pipeline via the `&&` operator. This cleanly purges stale system symlink caches and deploys updated sandbox protection from scratch:
```bash
sudo firecfg --clean && sudo firecfg
```

This command first resets and purges older, potentially conflicting symlinks, then deploys a clean, conflict-free sandbox layout in a single pass. Now, launching Firefox or Evince directly from the GNOME application launcher will automatically route execution through an isolated container.

To eliminate human error, visually differentiate sandboxed applications from the uncontained host, and replace default GNOME icons, we deploy independent local desktop entries paired with custom icon sets for our browser and local AI environment.

**3.** We create our local hidden icon structure and populate it with our downloaded 256px (256x256) and 512px (512x512) PNG assets:
```bash
mkdir -p ~/.local/share/icons/{256x256,256x256@2x} && cp "$HOME/PATH-TO-FILES/icons/256x256/"*.png ~/.local/share/icons/256x256/ && cp "$HOME/PATH-TO-FILES/icons/256x256@2x/"*.png ~/.local/share/icons/256x256@2x/
```

> [!WARNING]
> After modifying `Exec=` lines for applications such as LibreOffice, Image Viewer, Document Viewer, and others to integrate Firejail, we must end the active user session (Log Out...). Alternatively, rebooting the system ensures modified `Exec=` targets take effect across all desktop environments.

* We generate our primary isolated **Mozilla Firefox (Firejail Sandbox)** launcher, binding it directly to our local security profile and custom icon path:
```bash
cat <<EOF> ~/.local/share/applications/firefox-secure.desktop
[Desktop Entry]
Name=Firefox (Secure Sandbox)
Comment=Browse the World Wide Web in Firejail Sandbox
Exec=firejail --profile=firefox-hardened /usr/bin/firefox --no-remote --profile $HOME/.mozilla-hardened/firefox/current --name firefox-secure %u
StartupNotify=true
Terminal=false
Type=Application
Icon=/home/$USER/.local/share/icons/256x256@2x/firefox-secure.png
Categories=Network;WebBrowser;
MimeType=text/html;text/xml;application/xhtml+xml;
EOF
```

* We update our host administrative **Mozilla Firefox (Unsecured Host)** launcher (used for downloading heavy files), assigning it our custom bronze fox icon:

```bash
sudo sed -i -e 's/^Name=.*/Name=Firefox (Unsecured Host)/' -e "s|^Icon=.*|Icon=/home/$USER/.local/share/icons/256x256@2x/firefox-unsecure.png|" /usr/share/applications/firefox.desktop
```

* **For Ubuntu 24.04 LTS Noble Numbat Users (Documents and Images):**

We configure Firejail sandbox wrapping in the **Evince Document Viewer** launcher:
```bash
sudo sed -i 's|^Exec=evince.*$|Exec=firejail evince|' /usr/share/applications/org.gnome.Evince.desktop
```

We verify our modifications:
```bash
grep 'Exec=' /usr/share/applications/org.gnome.Evince.desktop
```

We configure Firejail sandbox wrapping in the **Eog Image Viewer** launcher:
```bash
sudo sed -i 's|^Exec=eog.*$|Exec=firejail eog|' /usr/share/applications/org.gnome.eog.desktop
```

We verify our modifications:
```bash
grep 'Exec=' /usr/share/applications/org.gnome.eog.desktop
```

* **For Ubuntu 26.04 LTS Resolute Raccoon Users (Documents and Images):**

We configure Firejail sandbox wrapping in the **Papers Document Viewer** launcher:
```bash
sudo sed -i 's|^Exec=papers.*$|Exec=firejail papers|' /usr/share/applications/org.gnome.Papers.desktop
```

We verify our modifications:
```bash
grep 'Exec=' /usr/share/applications/org.gnome.Papers.desktop
```

We configure Firejail sandbox wrapping in the **Loupe Image Viewer** launcher:
```bash
sudo sed -i 's|^Exec=loupe.*$|Exec=firejail loupe %U|; s|^DBusActivatable=true$|DBusActivatable=false|' /usr/share/applications/org.gnome.Loupe.desktop
```

We verify our modifications:
```bash
grep -E '^(Exec|DBusActivatable)=' /usr/share/applications/org.gnome.Loupe.desktop
```

* We update our security launcher for **KeePassXC**, linking it to our database and blocking external network egress (optionally backing up the standard entry):
```bash
sudo cp /usr/share/applications/org.keepassxc.KeePassXC.desktop /usr/share/applications/org.keepassxc.KeePassXC.desktop.bak
```

```bash
sudo sed -i -e 's/^Name=.*/Name=KeePassXC (Secure Sandbox)/' -e 's|^Exec=.*|Exec=firejail --net=none keepassxc %f|' -e "s|^Icon=.*|Icon=$HOME/.local/share/icons/256x256@2x/keepassxc-secure.png|" /usr/share/applications/org.keepassxc.KeePassXC.desktop
```

* We generate default **LibreOffice** hardened desktop launchers:

We update default execution paths to launch seamlessly under Firejail control by adjusting the primary and secondary `Exec` parameters in each launcher file.

```bash
sudo sed -i 's|^Exec=libreoffice|Exec=firejail libreoffice|' /usr/share/applications/libreoffice-startcenter.desktop
sudo sed -i 's|^Exec=libreoffice --writer|Exec=firejail libreoffice --writer|' /usr/share/applications/libreoffice-writer.desktop
sudo sed -i 's|^Exec=libreoffice --calc|Exec=firejail libreoffice --calc|' /usr/share/applications/libreoffice-calc.desktop
sudo sed -i 's|^Exec=libreoffice --impress|Exec=firejail libreoffice --impress|' /usr/share/applications/libreoffice-impress.desktop
sudo sed -i 's|^Exec=libreoffice --draw|Exec=firejail libreoffice --draw|' /usr/share/applications/libreoffice-draw.desktop
sudo sed -i 's|^Exec=libreoffice --math|Exec=firejail libreoffice --math|' /usr/share/applications/libreoffice-math.desktop
sudo sed -i 's|^Exec=libreoffice --base|Exec=firejail libreoffice --base|' /usr/share/applications/libreoffice-base.desktop
```
Following this modification, all office suite tools will launch restricted by our custom `libreoffice.profile`.

We verify each desktop launcher file:
```bash
grep 'Exec=' /usr/share/applications/libreoffice-writer.desktop
grep 'Exec=' /usr/share/applications/libreoffice-calc.desktop
grep 'Exec=' /usr/share/applications/libreoffice-impress.desktop
grep 'Exec=' /usr/share/applications/libreoffice-draw.desktop
grep 'Exec=' /usr/share/applications/libreoffice-math.desktop
grep 'Exec=' /usr/share/applications/libreoffice-base.desktop
```

* We generate a default hardened desktop launcher for **GIMP**:
We locate the target `gimp.desktop` file:
```bash
find /usr/share/applications -iname '*gimp*'
```

We prepend our Firejail execution string (if system package updates alter the target file name from `gimp.desktop`, update the command target accordingly):
```bash
sudo sed -i 's|^Exec=|Exec=firejail |' /usr/share/applications/gimp.desktop
```

We verify our modifications:
```bash
grep 'Exec=' /usr/share/applications/gimp.desktop
```

* We generate a hardened launcher for **VS Codium without network access (Air-Gapped Mode)**:
```bash
cat <<EOF> ~/.local/share/applications/vscodium-offline.desktop
[Desktop Entry]
Name=VS Codium (Offline IDE)
Comment=Code Editing without Network Access
Exec=firejail --net=none --profile=${HOME}/.config/firejail/vscodium.profile --whitelist=${HOME}/Documents /opt/vscodium/AppRun --no-sandbox
Icon=/home/$USER/.local/share/icons/256x256@2x/vscodium-offline.png
Terminal=false
Type=Application
Categories=Development;TextEditor;IDE;
MimeType=text/plain;
EOF
```

* We generate a hardened launcher for **VS Codium with network access (Plugin Installation Mode)**:
```bash
cat <<EOF> ~/.local/share/applications/vscodium-online.desktop
[Desktop Entry]
Name=VS Codium (Online IDE)
Comment=Code Editing with Network Access (Strict Sandbox)
Exec=firejail --profile=${HOME}/.config/firejail/vscodium.profile /opt/vscodium/AppRun --no-sandbox
Icon=/home/$USER/.local/share/icons/256x256@2x/vscodium-online.png
Terminal=false
Type=Application
Categories=Development;TextEditor;IDE;
MimeType=text/plain;
EOF
```

* We generate an administrative launcher for **LM Studio with internet access** (for discovering and fetching large LLM model weights from Hugging Face), configured to dynamically adapt to NVIDIA GPU or CPU inference modes:
```bash
cat <<EOF> ~/.local/share/applications/lm-online.desktop
[Desktop Entry]
Name=LM Studio (Online Downloader)
Comment=Run LM Studio with internet access to download LLM models
Exec=firejail --profile=lmstudio ${HOME}/.lmstudio_gui/lm-studio --no-sandbox
Icon=/home/$USER/.local/share/icons/256x256@2x/lm-unsecure.png
Terminal=false
Type=Application
Categories=Development;Science;
EOF
```

* We update our desktop launcher for our local AI engine **LM Studio for air-gapped offline operation**. The launcher script checks for NVIDIA hardware, exposes CUDA paths, forces network isolation via Linux kernel Kill Switch logic, and attaches our high-resolution icon:
```bash
cat <<EOF> ~/.local/share/applications/lm-offline.desktop
[Desktop Entry]
Name=LM Studio (Offline AI)
Comment=Local LLM Sandbox Agent
Exec=firejail --net=none --profile=lmstudio ${HOME}/.lmstudio_gui/lm-studio --no-sandbox
Icon=/home/$USER/.local/share/icons/256x256@2x/lm-secure.png
Terminal=false
Type=Application
Categories=Development;Science;
EOF
```

> [!WARNING]
> Background processes for LM Studio (`node-Main`) remain active in the system tray after closing the main application window. If not fully terminated from memory, launching an alternate entry will attach to the existing active instance. Completely quit the tray icon before switching between online and offline profiles.

* We generate a hardened desktop launcher for **Telegram**, linking execution to our lightweight sandbox profile paired with kernel-level `seccomp` filtering:
```bash
cat <<EOF> ~/.local/share/applications/telegramdesktop.desktop
[Desktop Entry]
Version=1.0
Name=Telegram Desktop (Secure Sandbox)
Comment=Official desktop version of Telegram inside Firejail Sandbox
Exec=firejail --profile=telegram /usr/bin/telegram-desktop u%
Icon=/home/$USER/.local/share/icons/256x256@2x/telegram-secure.png
Terminal=false
Type=Application
Categories=Network;InstantMessaging;
MimeType=x-scheme-handler/tg;
EOF
```

* We generate a hardened launcher for the **Psi+** XMPP client. This command registers the application within GNOME menus, restricts access across the user home directory (including downloads), while selectively whitelisting paths to preserve OMEMO keys and chat logs while exposing a secure bridge to the host GnuPG engine:
```bash
cat <<EOF> ~/.local/share/applications/psi-plus.desktop
[Desktop Entry]
Version=1.0
Name=Psi+ (Secure Sandbox)
Comment=XMPP client with OMEMO/GPG safely inside Firejail Sandbox
Exec=firejail psi-plus
Icon=/home/$USER/.local/share/icons/256x256@2x/psi-secure.png
Terminal=false
Type=Application
Categories=Network;InstantMessaging;
EOF
```

> [!WARNING]
> Background processes for Psi+ (`psi-plus`) remain active in the system tray after closing the main window. If not fully terminated, launching an alternate entry will attach to the background session. Always quit the application from the system tray before toggling execution contexts.

* We generate a hardened desktop entry for **Thunderbird**, deploying a optimized path whitelist profile with LPE protection that properly exposes NVIDIA graphics libraries when running under discrete GPUs:
```bash
cat <<EOF> ~/.local/share/applications/thunderbird.desktop
[Desktop Entry]
Version=1.0
Name=Thunderbird (Secure Sandbox)
Comment=Send and receive mail safely inside Firejail Sandbox
Exec=firejail --profile=thunderbird /usr/bin/thunderbird
Icon=/home/$USER/.local/share/icons/256x256@2x/thunderbird-secure.png
Terminal=false
Type=Application
Categories=Network;Email;
MimeType=message/rfc822;x-scheme-handler/mailto;
EOF
```

* For **Ubuntu 24.04**, we update the **Terminal** icon path:
```bash
sudo sed -i "s|^Icon=org.gnome.Terminal|Icon=/home/$USER/.local/share/icons/256x256@2x/terminal.png|" /usr/share/applications/org.gnome.Terminal.desktop
```

* For **Ubuntu 26.04**, we update the **Ptyxis** icon path:
```bash
sudo sed -i "s|^Icon=org.gnome.Ptyxis|Icon=/home/$USER/.local/share/icons/256x256@2x/terminal.png|" /usr/share/applications/org.gnome.Ptyxis.desktop
```

* Optionally, we update our **Trash** icons to custom assets (where `PATH-TO-FILES` maps to your local icon assets inside your home directory, e.g., `/.local/share/`):
```bash
for s in 16x16 16x16@2x 24x24 24x24@2x 32x32 32x32@2x 48x48 48x48@2x 256x256 256x256@2x; do sudo cp "$HOME/PATH-TO-FILES/icons/Trash/$s/"user-trash{,-full}.png /usr/share/icons/Yaru/$s/status/; done && for s in 16x16 16x16@2x 24x24 24x24@2x 32x32 32x32@2x 48x48 48x48@2x 256x256 256x256@2x; do sudo cp "$HOME/PATH-TO-FILES/icons/Trash/$s/"user-trash{,-full}.png /usr/share/icons/Yaru/$s/places/; done
```

We restore standard read permissions across updated system icons:
```bash
sudo find /usr/share/icons/Yaru -type f -name 'user-trash*.png' -exec chmod 644 {} \;
```

**4.** We instruct the desktop shell database parser to re-index all updated applications, ensuring our modified launchers take effect across application menus without requiring a system restart:
```bash
update-desktop-database ~/.local/share/applications/
```

**5.** We update the user icon cache:
```bash
gtk-update-icon-cache -f ~/.local/share/icons/
```

>[!NOTE]
> For applications handling multiple file extensions, we recommend verifying supported MIME types directly via `grep` in the terminal. Supported MIME bindings change between software releases. Querying entries directly ensures file associations remain valid without system conflicts.
>
> Example for retrieving active MIME bindings for the GIMP image editor:
> ```bash
> grep '^MimeType=' /usr/share/applications/gimp.desktop
> ```

* Once configuration files and custom launcher icons are applied, we reboot our system:
```bash
sudo reboot
```

>[!IMPORTANT]
> Let's review enforcing application isolation via user-space `.desktop` overrides.
>
> Direct modification of system files within `/usr/share/applications/` can lead to changes being overwritten whenever upstream packages update.
>
> The recommended approach is establishing local user overrides in:
> ```bash
> ~/.local/share/applications/
> ```
>
> Local user paths take priority over system-wide desktop entries defined in:
> ```bash
> /usr/share/applications/
> ```
>
> To locate an application's original `.desktop` entry, we use:
> ```bash
> find /usr/share/applications/ ~/.local/share/applications/ -name "APP_NAME.desktop" 2>/dev/null
> ```
>
> Alternatively, query installed package manifests via `dpkg`:
> ```bash
> dpkg -L APP_NAME | grep "\.desktop$"
> ```
>
> **Example:** Locating the GIMP desktop launcher:
> ```bash
> dpkg -L gimp | grep "\.desktop$"
> ```
>
> We create a local user copy:
> ```bash
> cp /usr/share/applications/gimp.desktop ~/.local/share/applications/gimp.desktop
> ```
>
> We open the local entry file:
> ```bash
> nano ~/.local/share/applications/gimp.desktop
> ```
> 
> We locate `Exec=gimp %U` and update it to `Exec=firejail --quiet gimp %U`.
> 
> Optionally, update the display name: `Name=GIMP (Sandbox)`
> 
> After saving changes, update the local application launcher index:
> ```bash
> update-desktop-database ~/.local/share/applications/
> ```
>
> Executing the application from graphical menus will now automatically launch inside Firejail.
>
> To hide an original system entry from desktop menus entirely, instantiate a local `.desktop` override file:
> ```ini
> cat <<EOF> ~/.local/share/applications/APP_NAME.desktop
> [Desktop Entry]
> Type=Application
> Name=Hidden System Link
> NoDisplay=true
> EOF
> ```
>
> This technique manages application menu visibility and removes duplicate launcher entries.

> [!TIP]
> To hide desktop icons or restore defaults without deleting files, modify GNOME Shell configuration keys directly.
> 
> Desktop Trash icon:
> ```bash
> gsettings set org.gnome.shell.extensions.ding show-trash false  # Hide
> gsettings set org.gnome.shell.extensions.ding show-trash true   # Show
> ```
> 
> Desktop Home directory:
> ```bash
> gsettings set org.gnome.shell.extensions.ding show-home false  # Hide
> gsettings set org.gnome.shell.extensions.ding show-home true   # Show
> ```

> [!IMPORTANT]
> GNOME 46+ running on Wayland maintains aggressive internal application indexing caches. If existing desktop entries share matching filenames while arguments or execution paths are updated, GNOME may silently block execution from menus, flagging entries as invalid. Direct execution tests via `gtk-launch` will run cleanly under terminal debugging.
> 
> The most reliable fix to force GNOME Shell to purge cached metadata is assigning unique application desktop entry IDs distinct from the underlying executable binary.
> 
> If desktop icons fail to launch after updating paths, force a cache purge by renaming desktop entries (demonstrated below using LM Studio):
> 
> * For LM Studio running in Firejail without network access (offline LLM mode):
> ```bash
> mv ~/.local/share/applications/lm-studio.desktop ~/.local/share/applications/lm-offline.desktop 2>/dev/null || true
> ```
> * For LM Studio running in Firejail with network access (online downloader mode):
> ```bash
> mv ~/.local/share/applications/lm-studio-unsecure.desktop ~/.local/share/applications/lm-online.desktop 2>/dev/null || true
> ```
> * Rebuild the application desktop entry index:
> ```bash
> update-desktop-database ~/.local/share/applications/
> ```
> * Refresh local icon caches:
> ```bash
> gtk-update-icon-cache -f ~/.local/share/icons/
> ```
> 
> Opening the GNOME application grid will now register the updated **LM Studio (Offline AI)** and **LM Studio (Online Downloader)** entries, re-validate launcher execution permissions, and restore smooth sandboxed execution on click.

#### Advanced Paranoia Mode: Sandboxing with Session Persistence via Overlay:

Using the `--private` flag is ideal for one-off sessions. But what should we do when we need to inspect the behavior of a suspicious utility in detail, persist its configuration files or plugins, while still strictly guaranteeing that the host operating system is protected from infection?

To achieve this, we deploy Firejail's hidden killer feature—**Overlay Mode**. It creates a temporary virtual "layer" on top of our real file system. The application sees all of our files, but it physically cannot modify a single byte on the actual disk: any write attempts, configuration creation, or stealthy malware persistence will be redirected into an isolated, hidden sandbox directory.

> [!IMPORTANT]
> Utilizing `overlay` modes requires OverlayFS file system support at the Linux kernel level (included in the standard Ubuntu kernel build) as well as unprivileged user namespaces enabled either in the profile or via command-line flags.

**1.** We launch the application while persisting all modifications to an overlay layer:
```bash
firejail --overlay-dir=~/.sandbox_overlay --seccomp --nonewprivs telegram-desktop
```
*(The `--overlay-dir=` parameter specifies the directory path where absolutely all changes made by the application during its execution will be recorded).*

> [!TIP]
> If you require a completely ephemeral session that instantly wipes all traces upon closing the application (without persisting anything to disk), use the `--overlay` flag without specifying a directory:
> ```bash
> firejail --overlay --seccomp --nonewprivs telegram-desktop
> ```
> In this case, the virtual layer is constructed exclusively in RAM (`tmpfs`) and vanishes without a trace once the process terminates.

**2.** After closing the application, we can open the generated directory and manually inspect its structure:
```bash
ls -la ~/.sandbox_overlay
```
We can directly observe which hidden files the utility attempted to create or modify inside `/etc`, `/var`, or our home profile!

**3.** If we confirm that the software behaved safely, we can keep the overlay layer for subsequent launches. However, if the utility exhibited suspicious activity, we completely purge all traces of its actions from the operating system with a single command:
```bash
rm -rf ~/.sandbox_overlay
```

<br>

## Installing Rkhunter and Hunting Rootkits

Next, we will focus on internal operating system security—protecting and scanning the environment for hidden malware and rootkits. Rootkits represent a dangerous class of malicious software that embeds deeply into the operating system kernel and disguises its presence by replacing standard system utilities.

To scan for rootkits and monitor file integrity, we will use the `Rkhunter` utility. To detect viruses and classic threats, we will deploy `ClamAV`—a battle-tested open-source antivirus engine that does not telemetry-transmit private user files to third-party corporate servers. For maximum security, we will run both utilities headless, launching them directly from the console.

**1.** We install the rootkit scanning utility:
```bash
sudo apt install rkhunter -y
```

**2.** In the blue pseudo-graphical `debconf` installer menu that appears, we forcibly select **"No configuration"** and press **"Enter"**. This completely blocks background mail services from initiating automated report delivery, eliminating stealth de-anonymization of the host network matrix.

**3.** We open the main configuration file:
```bash
sudo nano /etc/rkhunter.conf
```

Inside the file, we locate and modify the following parameters to configure proper database updates via secure mirrors:
```ini
UPDATE_MIRRORS=1
MIRRORS_MODE=0
AUTO_X_DETECT=0
WEB_CMD=""
```

To prevent the scanner from throwing false positive warnings on our forcibly purged system bloatware (`snapd`) and our custom security rules (the YubiKey Kill Switch), we navigate to the absolute end of the file and append strict security exceptions:
```ini
# Whitelist purged Snap directories so the utility does not inspect empty paths
EXISTWHITELIST="/var/lib/snapd/*"
EXISTWHITELIST="/snap"

# Whitelist our custom emergency session termination udev rule
FILEWHITELIST="/etc/udev/rules.d/80-yubikey-kill.rules"

# Disable false positive checks on specific hidden Ubuntu desktop shell scripts
SCRIPTWHITELIST="/usr/bin/egrep"
SCRIPTWHITELIST="/usr/bin/fgrep"
```

We save the configuration in `nano` by pressing **"Ctrl + O"** → **"Enter"**, followed by **"Ctrl + X"** to return to the console.

**4.** We verify that the application version is current:
```bash
sudo rkhunter --versioncheck
```

**5.** We download and apply the latest signature databases and current check rules:
```bash
sudo rkhunter --update
```

**6.** We generate an initial property snapshot of known clean system files:
```bash
sudo rkhunter --propupd
```
This step builds the baseline hash database for the target environment.

**7.** We execute an interactive audit of the operating system:
```bash
sudo rkhunter --check --sk
```
The `--sk` (*skip-keypress*) flag automatically bypasses prompts to press **"Enter"** after completing each testing section, running the scan in a single pass.

To prevent the utility from causing unnecessary resource overhead and executing silently without user awareness, we disable automated background cron checks.

**8.** We open the daily task configuration file:
```bash
sudo nano /etc/default/rkhunter
```

**9.** We locate the `CRON_DAILY_RUN` directive and explicitly set it to an inactive state:
```ini
CRON_DAILY_RUN="false"
```

We save the configuration in `nano` by pressing **"Ctrl + O"** → **"Enter"**, followed by **"Ctrl + X"** to exit.

> [!IMPORTANT]
> Note that `Rkhunter` relies on heuristic analysis, which carries a baseline rate of false positives. If the utility alerts on a suspicious file (*Possible rootkit*) on a freshly installed system, it is a false alarm with 99% probability.
> 
> Strict AppArmor hardening, telemetry removal, and the Snapd purge executed in previous steps significantly alter the structure of system configuration paths inside `/etc`. The initial scan will flag these modifications and trigger several warnings—this is legitimate software behavior and should not cause concern.
> 
> We must document the baseline results of this clean initial scan. If subsequent routine audits reveal unexpected hash modifications, that signals a requirement for a thorough manual investigation. Keep in mind that `Rkhunter` operates strictly as a scanner—it does not remove malicious software. In the event of a genuine breach, purging malicious kernel modules requires manual remediation per specialized incident response documentation.
> 
> Paying strict attention to `sudo rkhunter --propupd` is essential. This command creates a baseline hash snapshot of all core system binaries (stored in the `/var/lib/rkhunter/db/rkhunter.dat` database). Maintain an operational rule: execute `sudo rkhunter --propupd` immediately after every legitimate system upgrade performed via `sudo apt upgrade`.
> 
> Skipping this step causes the subsequent `Rkhunter` run to throw a massive avalanche of critical warnings across standard system utilities (such as `ls`, `ps`, and `top`), as their cryptographic hashes legitimately changed during official package updates. The correct operational lifecycle is: update system → verify stability → deploy `sudo rkhunter --propupd` to update the baseline snapshot in the database.

<br>

## Installing and Configuring the ClamAV Antivirus Scanner

#### Introduction:

ClamAV is a full-featured open-source antivirus engine. On Linux-based operating systems, we deploy it primarily to inspect incoming mail flow, audit external encrypted USB media, or scan network downloads for hidden Windows-targeted malware, ensuring we eliminate accidental cross-platform threat vector propagation to adjacent workstations.

#### Installing ClamAV:

**1.** We install the core ClamAV antivirus engine along with its background system daemon:
```bash
sudo apt install clamav clamav-daemon -y
```

**2.** We verify deployment integrity and confirm the active release version of the scanner engine:
```bash
clamscan --version
```

**3.** Installing the official Graphical User Interface (GUI) is an optional step for operators who prefer working within a visual container:
```bash
sudo apt install clamtk -y
```

**4.** We launch the graphical shell of the antivirus scanner:
```bash
clamtk
```

#### Updating Signature Databases and Bypassing Network Blocks:

The background automated updater daemon may hit network errors or upstream geographic IP blocks (returning a `403 Forbidden` system code). To ensure guaranteed, secure delivery of fresh signature databases, we suspend the automated daemon and execute manual database synchronization:

**1.** We temporarily halt the background auto-update service before performing manual database maintenance:
```bash
sudo systemctl stop clamav-freshclam
```

**2.** We launch the standard console-driven database signature update:
```bash
sudo freshclam
```

> [!NOTE]
> **Author's Note:** If the utility returns an access error, Cisco Talos developer servers are actively blocking incoming connection requests. In this scenario, we must manually fetch the latest signature database files (`main.cvd`, `daily.cvd`, `bytecode.cvd`) over a secure proxy tunnel from the official `database.clamav.net` mirror or pull them from trusted community security mirrors. As a high-availability, fast, fully open alternative source, we recommend using the official Microsoft repository mirror: `https://packages.microsoft.com/clamav/`.

Once the download finishes, we open a terminal session inside `~/Downloads` and forcibly move the database assets into the system antivirus directory:

**3.** We copy all three downloaded signature database files in a single pass:
```bash
sudo cp main.cvd daily.cvd bytecode.cvd /var/lib/clamav/
```

**4.** We explicitly transfer ownership of the signature files to the system user `clamav`, without which the antivirus engine physically cannot parse them:
```bash
sudo chown clamav:clamav /var/lib/clamav/*
```

**5.** We re-enable and launch the automated update background service:
```bash
sudo systemctl enable clamav-freshclam --now
```

#### Structuring System Scans:

**1.** We launch a full system root filesystem audit under elevated privileges:
```bash
sudo clamscan -r -i --max-filesize=100M --max-scansize=100M --exclude-dir="^/sys" --exclude-dir="^/proc" --exclude-dir="^/dev" --exclude-dir="^/snap" --exclude-dir="^/run" /
```

Let's break down the filtering parameters of this heavy scan pipeline:
* **`-r`** (*recursive*)—enforces deep directory traversal across nested file structures.
* **`--bell`**—triggers an audible system bell notification upon threat detection.
* **`-i`** (*infected*)—restricts output strictly to infected file hits, keeping the console buffer clean of millions of uninfected file logs.
* **`--exclude-dir`**—forcibly excludes virtual kernel pseudo-filesystems (`/sys`, `/proc`, `/dev`) and container mounts (`/snap`, if not purged in previous hardening chapters) to prevent infinite system interface loop locks.

**2.** We execute a fast audit of the active user's home directory (personal documents and user data):
```bash
clamscan -r /home/$USER
```

**3.** We display a concise interactive summary of available operational flags:
```bash
clamscan --help
```

**4.** We pull up the comprehensive official system manual detailing configuration flags and engine options:
```bash
man clamscan
```

If the antivirus component is no longer required, we perform a clean, complete purge of the software along with all leftover configuration profiles in a single operation:

**5.** We completely purge ClamAV and its graphical interface wrapper:
```bash
sudo apt purge clamav clamav-base clamav-daemon clamav-freshclam clamtk -y && sudo apt autoremove --purge -y
```

#### Multithreaded Scanning (Hardening):

By default, the standard `clamscan` binary operates strictly single-threaded. Auditing high-capacity system drives can take 5 to 8 hours while maxing out a single CPU core at 100%. To multiply throughput, we deploy the multithreaded daemon `clamdscan`, backed by the running `clamav-daemon` service. It parallelizes the workload across all available processor cores, accelerating file inspection by 4x–6x!

**1.** We launch a multithreaded system-wide filesystem audit:
```bash
sudo clamdscan -m --fdpass --stream --config-file=/etc/clamav/clamd.conf /
```
The `-m` (*multiscan*) flag handles parallelized core execution.

> [!WARNING]
> Exercise extreme caution when executing the aggressive `--remove` flag for instant physical destruction of flagged malware. In the event of a false positive, the engine can permanently obliterate critical operating system files, instantly destabilizing system integrity.

If we need to isolate potential threats into a secure, restricted quarantine area rather than destroying them, we first establish a target directory and transfer ownership permissions to the antivirus daemon:

**2.** We establish the isolation quarantine directory:
```bash
sudo mkdir -p /var/lib/clamav/quarantine
```

**3.** We grant ownership rights over the quarantine path to the antivirus daemon:
```bash
sudo chown clamav:clamav /var/lib/clamav/quarantine
```

Only after securing the quarantine zone do we initiate high-speed multithreaded scanning with automated threat isolation:

**4.** We execute a multithreaded drive scan, routing flagged threats straight into quarantine:
```bash
sudo clamdscan -m --fdpass --move=/var/lib/clamav/quarantine --stream /
```

> [!NOTE]
> Passing the `--fdpass` (*file descriptor passing*) flag in multithreaded scan commands is strictly mandatory. It forces the terminal process to pass target file descriptors to the background daemon, enabling seamless inspection of protected system paths that the unprivileged `clamav` system user lacks direct read access to by default.

<br>

## Installing and Configuring the VirtualBox Virtualization Environment

VirtualBox serves as an ideal framework for spinning up isolated virtual machines and safely testing third-party operating systems (such as Kali Linux, Parrot OS, Windows, etc.). To maintain maximum stability, we deploy the official engine build directly from Oracle's repositories.

**1.** We prevent critical package manager desynchronization. Because we enforced strict PAM stack hardening and disabled biometric authentication in previous chapters, routine updates to fingerprint reader libraries will trigger a permanent runtime deadlock at the 78% mark. We forcibly unlock, purge from the host, and clean up residual configuration artifacts for both the biometric daemon and automated background update services:
```bash
sudo apt-get purge fprintd libfprint-2-2 libfprint-2-tod1 libpam-fprintd unattended-upgrades --allow-change-held-packages -y
```

**2.** We execute a clean index refresh and upgrade system modules across the host WITHOUT risking interactive terminal hangs:
```bash
sudo apt update && sudo apt upgrade -y
```

**3.** We install base compilation tools (`gcc`, `make`) alongside the `dkms` utility, which is required to automatically rebuild VirtualBox kernel modules during routine Linux kernel updates:
```bash
sudo apt install wget dkms build-essential -y
```

**4.** We integrate Oracle's official repository into the `apt` sources configuration. To completely eliminate dependency on vendor-side cryptographic desyncs (short 32-bit PGP key collisions) and bypass stuck signature checks under strict 4x4 host isolation, we forcibly inject the `[trusted=yes]` mandatory flag. Packages will be securely pulled over a protected HTTPS TLS channel directly from Oracle's official domain.

For **Ubuntu 24.04 LTS** (Noble Numbat), we target the `noble` branch:
```bash
echo "deb [arch=amd64 trusted=yes] https://download.virtualbox.org/virtualbox/debian noble contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
```

For **Ubuntu 26.04 LTS** (Resolute Raccoon), we lock the release path to the stable parent LTS base `noble`, as a dedicated release directory for the 2026 tree is not present on Oracle servers:
```bash
echo "deb [arch=amd64 trusted=yes] https://download.virtualbox.org/virtualbox/debian resolute contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
```

**5.** We update system package indexes. The `[trusted=yes]` directive instructs the package manager to bypass vendor signature checks and cleanly commit repository metadata into runtime:
```bash
sudo apt update
```

> [!NOTE]
> Because we deliberately bypassed importing legacy Oracle keyrings, `apt` will reliably display warnings during index refreshes such as: `W: GPG error...` or `Signed file isn't valid, got 'NODATA'`. We disregard these notifications entirely. The mandatory `[trusted=yes]` flag forces the subsystem to bypass warnings, maintain pipeline execution, and ingest the `contrib` package lists for deployment.

**6.** We install the current stable VirtualBox release, optimized for modern Linux kernel trees (the package manager pulls the legitimate binary over a secure HTTPS TLS channel):
```bash
sudo apt install virtualbox-7.2 -y
```

**7.** We append the active user account to the virtualization management group, granting guest operating systems direct pass-through access to host USB ports (the `$USER` variable automatically resolves the local account username):
```bash
sudo usermod -aG vboxusers $USER
```

> [!NOTE]
> Upon initial VirtualBox installation on physical hardware with Secure Boot enabled, the inline module builder compiles kernel objects in an uncompressed `.ko` format, placing them inside `/lib/modules/$(uname -r)/misc/`.
> 
> Due to kernel dependency map indexing delays, running standard verification commands like `modinfo -n vboxdrv` may return a false-positive error: `ERROR: Module vboxdrv not found`. There is no reason for alarm—the utility simply hasn't reindexed the new paths yet.
> 
> The sole, absolute indicator that Secure Boot successfully ingested the MOK key and kernel modules were legally injected into Ring 0 is active memory inspection:
> ```bash
> lsmod | grep vbox
> ```
> If output streams confirm `vboxdrv`, `vboxnetflt`, and `vboxnetadp` loaded into memory, the hypervisor is autonomous, hardware-isolated, and ready to host guest workloads safely.

Upon system reboot, the blue-grey **Perform MOK management** screen will trigger. Rapidly press any key and complete MOK enrollment via the following sequence: **Enroll MOK** ➔ **Continue** ➔ **Yes** ➔ enter the password (configured during `mokutil` setup) ➔ **Reboot**.

**8.** We initiate host reboot to complete MOK enrollment steps:
```bash
systemctl reboot -i
```

**9.** We build and initialize low-level virtualization drivers inside the Linux kernel core:
```bash
sudo /sbin/vboxconfig
```

**10.** We disable startup services for automatic virtual machine provisioning and the web API management service:
```bash
sudo systemctl disable --now vboxautostart-service && sudo systemctl disable --now vboxweb-service
```

> [!WARNING]
> Never set a virtual machine's network adapter to **Bridged Adapter** mode unless out-of-band direct network routing without host VPN encapsulation is explicitly required. Under Bridged mode, the guest OS (whether a unvetted Windows image or a Kali Linux testing build) receives an uncontained local IP address on the physical host LAN. It directly exposes the local router, network storage, and adjacent LAN nodes, introducing a major attack surface into local network security.
> 
> Always verify settings: configure virtual machine network adapters strictly to **NAT** or **Host-only** modes. **NAT** mode isolates guest traffic inside the host environment, forcing outbound flows through the UFW firewall Kill Switch and the secure `tun0` VPN tunnel configured in prior chapters.
> 
> **The sole exception** to this operational rule is deploying the specialized anonymous OS suite *Whonix*. Its architecture relies on two isolated virtual machines with custom interface topologies:
> 
> * **Whonix-Gateway:** Interface 1 faces outbound networks via secure **NAT** mode (automatically routed through host VPN and UFW firewall boundaries), while Interface 2 is explicitly assigned to **Internal Network** mode using the designated segment name `whonix`.
> * **Whonix-Workstation:** The single network adapter is identically configured to **Internal Network** mode mapped to the same isolated `whonix` virtual segment.
> 
> This architecture ensures that the workstation physically lacks direct access to host networks or local gateway routers, forcing 100% of outbound traffic through the Tor anonymity network via the isolated gateway node.

<br>

## Shrinking and Optimizing VDI Virtual Disks

#### Introduction:

During active operation, virtual machine disk files continuously expand. Installing software packages or downloading files inside a guest OS naturally inflates the size of the dynamic virtual disk (`*.vdi`) on the host's physical storage. However, subsequently deleting those files within the guest OS does not automatically shrink the host `*.vdi` file.

This occurs because the guest operating system's file system merely marks disk sectors as "free" without physically clearing their contents. For the VirtualBox hypervisor, these blocks remain populated with legacy data. To reclaim free gigabytes on the real SSD, disk zeroing and optimization must be executed manually.

#### Sanitizing a Windows Guest Virtual Machine:

1. Launch the target Windows virtual machine.
2. Download the official `SDelete` CLI utility from the legitimate Microsoft Sysinternals repository (`microsoft.com`).
3. Extract the `sdelete64.exe` binary (for 64-bit architectures) directly into the root directory of drive `C:\`.
4. Open Command Prompt (`cmd.exe`) with mandatory administrative privileges and execute:
```cmd
C:\sdelete64.exe -z C:
```

5. Await task completion (the utility forcibly overwrites unallocated disk space with zero-byte patterns), then issue a full shutdown of the Windows guest.

> [!IMPORTANT]
> The `-z` flag of `SDelete` populates unallocated space strictly with zeros, which is mandatory for subsequent VirtualBox disk compression. However, if the operational goal is forensic data destruction rather than storage optimization, deploy the `-c` flag instead.
> 
> The `-c` parameter overwrites free space using random patterns per the US Department of Defense *DoD 5220.22-M* standard. Note: after applying `-c`, the VirtualBox compression algorithm will be unable to reduce the size of the `*.vdi` file, as random bits are parsed as valid payload data. For storage reduction, enforce `-z` exclusively.

#### Sanitizing a Linux Guest Virtual Machine (Ubuntu/Kali Linux):

Instead of running slow, aggressive zero-fill operations via `dd` (which degrades physical host SSD lifespan by churning hundreds of gigabytes of empty payload), deploying the specialized `zerofree` utility under Linux guest environments is significantly more efficient. It targets only modified blocks containing deleted file references, zeroing them in seconds without inflicting unnecessary write amplification on the host drive.

To execute `zerofree`, the guest filesystem must be unmounted or remounted in Read-Only mode. Achieving this is most straightforward via Recovery Mode. We configure the GRUB bootloader parameters directly from the active OS:

**1.** Inside the guest Linux environment, we open the bootloader configuration file:
```bash
sudo nano /etc/default/grub
```

**2.** We locate `GRUB_TIMEOUT=0` and adjust the parameter to `5` (allowing a 5-second window at boot to access the menu). Additionally, if `GRUB_TIMEOUT_STYLE=hidden` is active, comment out the directive by prefixing it with a `#` symbol. Save the file in `nano` via **"Ctrl + O"** → **"Enter"**, and exit using **"Ctrl + X"**.

**3.** We update the system bootloader configuration:
```bash
sudo update-grub
```

**4.** We reboot the virtual machine. As the system initializes, the textual GRUB menu displays. We navigate via arrow keys to the second entry: **"Advanced options for Ubuntu"**, press **"Enter"**, and select the kernel entry appended with **"(recovery mode)"**.

**5.** The system boots into the graphical recovery menu. Select the **"drop to root shell prompt"** option and press **"Enter"**.

**6.** A root shell initializes at the bottom of the screen. We execute the command to remount the root filesystem read-only:
```bash
mount -o remount,ro /
```

**7.** We execute immediate zero-filling across unallocated filesystem blocks:
```bash
zerofree -v /dev/sda1
```

> [!TIP]
> **Author's Note:** You can identify the exact target block device (e.g., `/dev/sda1` or `/dev/nvme0n1p2`) prior to reboot from the active system via `df -h`. Upon task completion, power off the virtual machine completely.

#### Final Virtual Disk Compaction on the Host Machine:

Now that unallocated storage within the virtual disks is zeroed out, we open a terminal session on our primary Ubuntu host system. Navigate to the directory housing the target virtual machine files (e.g., `~/VirtualBox VMs/`), and initiate the final compaction workflow.

> [!IMPORTANT]
> **Attention!** Linux terminals enforce strict case sensitivity. The VirtualBox control utility binary must be invoked precisely as `VBoxManage`.

**1.** We display detailed metadata for all registered virtual storage media along with their unique UUID descriptors:
```bash
VBoxManage list hdds
```

**2a.** Compaction utilizing the disk UUID: if the target drive UUID reads `21e5b710-6ed1-412f-6313-ac7e6251b3f3`, we execute:
```bash
VBoxManage modifymedium --compact 21e5b710-6ed1-412f-6313-ac7e6251b3f3
```

**2b.** Compaction directly referencing the target file path:
```bash
VBoxManage modifymedium --compact "Target_Machine.vdi"
```

Upon task completion, the virtual disk files instantly drop in size—reclaiming gigabytes to tens of gigabytes of host capacity (proportional to previously purged guest files) and restoring physical host SSD storage!

<br>

## Installing and Configuring the Docker Containerization Platform

#### Introduction:

The VirtualBox virtualization domain, which we rigorously architected in the previous chapter, is ideal for running heavy guest operating systems. However, in modern offensive and defensive security operations, containerization via Docker is deployed far more frequently for spinning up isolated utilities, vulnerable target ranges (DVWA, WebGoat), or automated OSINT scrapers.

A core principle to internalize: vanilla Docker out of the box is a massive architectural security hole in a paranoid desktop environment. Without aggressive, low-level hardening, running it inside a secured system is outright operational suicide.

> [!NOTE]
> Personally, I still favor full OS virtualization via virtual machines, so Docker stress-testing under Ubuntu 26.04 was executed purely superficially! Container deployments were tested strictly on Ubuntu 24.04.4.

#### What Is the Hidden Danger of Default Docker?

* **The Omnipotent Root Daemon:** By default, the background Docker service (`dockerd`) executes at the highest kernel level with full `root` privileges. Containers spawn under superuser context. If a zero-day or critical flaw hits software running inside a container, an attacker can execute a Container Escape and immediately take full control of our guest kernel.
* **Network Hijacking Bypassing UFW:** The most critical OPSEC flaw. Upon initialization, Docker provisions its own network bridge and injects routing rules directly into the top of the Linux kernel's `iptables/nftables` chains, completely circumventing UFW rules. If we fire up any containerized service and map a port (e.g., `-p 80:80`), Docker exposes that socket to the open internet, bypassing our Kill Switch and UFW restrictions. Traffic hits the container directly through the physical interface, completely bypassing our active `tun0` VPN tunnel. This is a textbook, purebred OPSEC failure in action.

To neutralize these threat vectors, we execute a two-tier hardening strategy: shift Docker into a unprivileged Rootless Mode and strictly lock down its ability to tamper with the host network stack.

To maintain absolute environment purity, we utilize the standard APT package manager while strictly pinning Canonical's official, secure update mirrors to ensure the system never pulls rogue software from third-party PPA repositories. Keep track of release codenames: **24.04 LTS is Noble Numbat** (`noble`), while the upcoming **26.04 LTS is Resolute Raccoon** (`resolute`).

#### Deploying Docker in Rootless Mode:

Rootless Mode forces the Docker daemon and all child containers to execute entirely inside isolated User Namespaces. The daemon runs under an unprivileged user context. Even if an attacker breaches a container and gains "root" inside the sandbox, to the host OS they remain an unprivileged user with zero access to system files.

**1.** To pin official mirrors in modern Ubuntu releases, we open the DEB822-formatted repository configuration file using a text editor with superuser rights:
```bash
sudo nano /etc/apt/sources.list.d/ubuntu.sources
```

**2.** We verify that the `URIs` field references exclusively official endpoints (`http://archive.ubuntu.com/ubuntu/` and `http://security.ubuntu.com/ubuntu/`) matching our OS codename (`noble` for 24.04 or `resolute` for 26.04), fully locking down third-party attack vectors.

**3.** We update the local APT index and pull the upstream Docker engine along with essential user-space networking components, network encapsulation tools, and `curl` from Canonical's trusted mirror:
```bash
sudo apt update && sudo apt install docker.io docker-buildx docker-compose-v2 docker-doc uidmap dbus-user-session slirp4netns fuse-overlayfs curl -y
```

**4.** We forcibly disable and purge the system-wide root Docker service from auto-start so it never initializes at the host kernel level:
```bash
sudo systemctl disable --now docker.service docker.socket
```

**5.** We apply hard masking to the root service and its socket, binding them with symlinks to a digital black hole to prevent rogue system triggers from invoking the root daemon:
```bash
sudo systemctl mask docker.service docker.socket
```

**6.** We bypass the new restrictions in Ubuntu 24.04/26.04 LTS by disabling the global kernel block on unprivileged user namespaces, persisting the setting in the host's sysctl configuration to survive system reboots:
```bash
sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0 && echo 'kernel.apparmor_restrict_unprivileged_userns=0' | sudo tee /etc/sysctl.d/99-rootless-docker.conf
```

**7.** We execute the official rootless setup script directly from the upstream source (run this command strictly as our standard unprivileged user without `sudo`):
```bash
curl -fsSL https://get.docker.com/rootless | sh
```

**8.** We inject the paths for isolated rootless binaries and our new user-space Docker socket into our shell config—dynamically mapping the current user ID via `$UID`—and refresh our terminal environment:
```bash
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc && echo 'export DOCKER_HOST=unix:///run/user/$UID/docker.sock' >> ~/.bashrc && source ~/.bashrc
```

**9.** We instruct the operating system to keep our user-space processes running in the background even after closing the terminal session:
```bash
loginctl enable-linger $USER
```

**10.** We reload systemd user-configuration files and place our isolated rootless Docker service on active duty in auto-start:
```bash
systemctl --user daemon-reload && systemctl --user enable --now docker.service
```

**11.** We run a verification check on the containerization engine to confirm Docker officially acknowledges our rootless status:
```bash
docker info | grep -i rootless
```

#### TTaming the Network and Binding Docker to UFW:

Now for the critical security enforcement: we completely revoke Docker's ability to manipulate kernel routing tables and force its network traffic to obey our UFW firewall. At this stage, we can re-enable the network interface in NetworkManager.

**1.** We create a hidden configuration directory and open the Docker daemon config file under our user profile:
```bash
mkdir -p ~/.config/docker/ && nano ~/.config/docker/daemon.json
```

**2.** We insert the JSON block to strip Docker of `iptables/nftables` modification privileges while locking in privacy-focused, non-logging Quad9 DNS servers. Save via **"Ctrl + O"** → **"Enter"** and exit with **"Ctrl + X"**:
```json
{
  "iptables": false,
  "dns": ["9.9.9.9", "149.112.112.112"]
}
```

**3.** We restart our user-space Docker daemon to apply these strict network restrictions:
```bash
systemctl --user restart docker.service
```

**4.** We selectively allow UFW packet forwarding (`FORWARD`) exclusively for the isolated Docker subnet based on our active network architecture:

* **If operating WITH an active VPN via `tun0`:**
```bash
sudo ufw route allow in on lo out on tun0 from 172.17.0.0/16
```
* **If operating DIRECTLY via physical NIC (replace `enp0s1` with your interface name):**
```bash
sudo ufw route allow in on lo out on enp0s1 from 172.17.0.0/16
```

**5.** We open UFW's low-level post-routing and filtering rule file:
```bash
sudo nano /etc/ufw/before.rules
```

**6.** We scroll to the bottom, add a single blank line right after the final default `COMMIT` keyword (which closes the filter table), and append an isolated NAT rule block that masquerades the Docker subnet and forces its traffic through the designated interface. Save and close:

* **If routing traffic STRICTLY through the `tun0` VPN interface to prevent IP leaks:**
```ini
# Route and masquerade Rootless Docker traffic STRICTLY through VPN (tun0)
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 172.17.0.0/16 -o tun0 -j MASQUERADE
COMMIT
```
* **If testing the setup DIRECTLY without VPN via host physical NIC:**
```ini
# Route and masquerade Rootless Docker traffic DIRECTLY through physical NIC (replace enp0s1 with your interface name)
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 172.17.0.0/16 -o enp0s1 -j MASQUERADE
COMMIT
```

**7.** We reload UFW to apply our low-level modifications, isolate the subnet, and reload routing tables:
```bash
sudo ufw reload
```

**8.** We force Ubuntu's NetworkManager to re-read our physical network interface configuration to restore the hypervisor gateway connection post-firewall activation (replace `enp0s1` with your interface name):
```bash
sudo nmcli device reapply enp0s1
```

**9.** We verify outbound WAN stability by sending an application-layer TCP request through the firewall and Portmaster eBPF filters (raw ICMP/ping is intentionally avoided here as paranoid network drivers drop it for CLI tools):
```bash
curl -I https://google.com
```

**10.** We restart Portmaster to immediately apply eBPF socket-interception rules and establish full control over unprivileged daemon activity at the kernel level:
```bash
sudo systemctl restart portmaster
```

**11.** We manually launch the Portmaster GUI from the application menu (**"Show Apps"**); otherwise, the kernel eBPF filter remains in a hard-lock state and drops all outbound system traffic until the GUI session initializes.

Click "Allow" on Portmaster's pop-up prompt. We now hold absolute perimeter control: UFW masquerades and routes Docker traffic strictly through the chosen interface (mandatorily bound to the VPN in operational mode), Portmaster intercepts telemetry in real time, and Docker is physically locked inside host rules—incapable of opening any external ports on its own.

#### Hardened Container Deployment in Practice:

Stripping root privileges and locking down the network covers baseline security. However, when spinning up individual containers, we must apply additional "paranoia flags" to restrict process privileges inside the sandbox as tightly as possible.

**1.** We deploy a reference Nginx web server container in maximum isolation mode. Note that the `127.0.0.1:` prefix attached to the port is our primary network shield, locking the socket strictly to localhost. We also set the container filesystem to read-only (`--read-only`), block privilege escalation at the hardware level, and mount temporary in-memory directories:
```bash
docker run -d --name secure_web -p 127.0.0.1:8080:80 --read-only --security-opt=no-new-privileges --tmpfs /tmp --tmpfs /var/cache/nginx --tmpfs /run nginx
```

**2.** We inspect active network sockets on the host to verify that our security setup held, the socket bound strictly to localhost, and its owner lists as `rootlesskit`:
```bash
ss -tulpn | grep 8080
```

#### Experimental Proof of Security (Verifying Non-Root Execution):

To prove that the container is fully isolated and possesses zero superuser rights on the host, we conduct a practical security validation experiment. We will simulate an attacker trying to compromise the host system by creating files under a fake container "root" account.

**1.** We create a clean local directory on the host machine to capture our test results:
```bash
mkdir -p ~/host_share
```

**2.** We launch an isolated Alpine Linux container, mount the local folder into the sandbox using the volume flag `-v`, and generate a test file from within the container's "root" context:
```bash
docker run --rm -v ~/host_share:/tmp/container_share alpine touch /tmp/container_share/evil_payload.txt
```

**3.** We inspect real file permissions directly on the host machine's drive:
```bash
ls -l ~/host_share/evil_payload.txt
```
*And there it is—the fundamental security mechanics of User Namespaces in action! Output shows file ownership as `user user`. The Linux kernel remapped the UIDs: "fake root" inside the container is, to the underlying host OS, an unprivileged process unable to write files with superuser rights! A container escape from this setup is technically impossible.*

**4.** We completely purge all artifacts of our security test from disk:
```bash
rm -rf ~/host_share
```

> [!NOTE]
> **Orchestration Architecture Note:** Unlike an isolated Nginx instance, the Portainer management UI requires persistent disk writes for logs and database maintenance; thus, `--read-only` cannot be applied. Instead, Portainer security relies on strict localhost binding, blocking privilege escalation, and executing via the current user's unprivileged rootless socket.

**5.** We deploy the Portainer web management dashboard in high-security mode—strictly bound to localhost (`127.0.0.1:`), blocking all privilege escalation attempts, and dynamically passing the user socket via `$UID`:
```bash
docker run -d --name portainer --restart always -p 127.0.0.1:9443:9443 --security-opt=no-new-privileges -v /run/user/$UID/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

**6.** We verify host network ports once more to ensure Portainer's web UI (port 9443) is locked inside `127.0.0.1` and completely hidden from external LAN discovery:
```bash
ss -tulpn | grep 9443
```

> [!WARNING]
> If we port this configuration from an isolated guest VM to a bare-metal host, the threat model shifts fundamentally. To avoid compromising a hardened host environment, strictly observe these three rules:
> 
> 1. **Never use `sysctl=0` on the host:** Globally disabling kernel protections via `sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0` on your primary machine is strictly forbidden. Doing so creates an attack vector for local malware. Host rootless setups must be launched *exclusively* via targeted AppArmor profiles for `rootlesskit`.
> 2. **Directory Mount Hygiene (`-v` flag):** Never mount the system root (`/`) or the user home directory (`~`) inside containers. In the event of a container escape, an attacker—even if bound by Rootless Mode—gains immediate read, write, and purge capabilities over all personal files, SSH keys, and credentials on the physical machine.
> 3. **User-Level Isolation:** The optimal host security architecture is creating a dedicated system account (e.g., `isolated-docker`) without admin rights and running Rootless Docker strictly inside its environment. This isolates containerized workloads completely from your primary operational environment.

<br>

## Installing and Configuring the AIDE File Integrity Monitoring System

#### Introduction:

A powerful tool for host internal security management is AIDE (*Advanced Intrusion Detection Environment*) — an advanced host-based intrusion detection system (HIDS). It performs continuous monitoring of file system changes across Linux and is deployed to detect stealthy malware, rootkits, and unauthorized adversary activity in real time.

The architecture of AIDE relies on generating a digital baseline snapshot (a cryptographic hash database) of a clean operating system state, against which current file attributes are evaluated. This allows us to pinpoint exactly which binaries or configuration files were modified, deleted, or introduced. To calculate these baselines, the system leverages strong hashing algorithms including SHA-256 and SHA-512.

> [!IMPORTANT]
> Deploying and initializing the primary AIDE database must be executed at the absolute end of host provision — strictly after installing and fully hardening all necessary tooling (VPN, Portmaster, VeraCrypt, Firejail). This guarantees that legitimate binaries and configs are indexed into the reference "clean" system snapshot, completely preventing a flood of false positives during routine integrity checks.

#### Installing and Configuring AIDE:

We open a terminal as an unprivileged user and initiate the installation workflow.

**1.** We install the file integrity monitoring package:
```bash
sudo apt update && sudo apt install aide -y
```

**2.** We create a custom configuration snippet to specifically exclude noisy runtime paths from global host monitoring:
```bash
sudo nano /etc/aide/aide.conf.d/99_custom
```

**3.** Inside the empty file, we append our native security exclusions. We explicitly prohibit AIDE from scanning rapidly shifting temporary directories, caches, system logs, and Portmaster eBPF firewall databases to completely neutralize False Positives:
```ini
!/var/log/.*
!/var/log/portmaster/.*
!/var/lib/aide/.*
!/var/lib/apt/.*
!/var/lib/dpkg/.*
!/var/lib/portmaster/.*
!/var/cache/.*
!/run/.*
!/tmp/.*
!/proc/.*
!/sys/.*
!/var/tmp/.*
!/var/run/.*
!/var/log/journal/.*
!/var/lib/NetworkManager/.*
!/var/lib/systemd/.*
!/var/lib/upower/.*
```

To save our configuration in `nano`, press **"Ctrl + O"** → **"Enter"**, and exit using **"Ctrl + X"**.

In AIDE's native configuration syntax, exclusion rules (negation rules) must be written strictly without spaces! Placing a space between the exclamation mark `!` and the leading slash `/` breaks the engine parser, causing an immediate syntax crash dump.

**4.** We compile the global system configuration from the active snippets and trigger the initial baseline snapshot generation (on high-capacity drives, computing SHA-512 cryptographic hashes can take substantial time):
```bash
sudo aideinit
```

**5.** We copy the newly generated database to production baseline status (the `-p` flag preserves original file ownership and permissions):
```bash
sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
```

Under Ubuntu, AIDE database artifacts must remain gzipped and carry the `.gz` file extension.

**6.** We run a dry-run integrity check across the host:
```bash
sudo aide -c /etc/aide/aide.conf --check
```

In a completely pristine setup, the command returns a green status reporting zero integrity violations, confirming the dynamic state matches our baseline snapshot. However, on active workstations with multiple background dependencies, runtime drift occurs naturally. Modifications will show up in `/home/$USER/` and its subdirectories: `/.config/dconf/*`, `/.config/tiling-assistant/*`, `/.local/share/`, `.bash_history`...

#### Executing a Penetration Test (Validating Defense Mechanisms):

Let us verify that our host intrusion detection system responds correctly under attack scenarios. We simulate a stealthy backdoor payload drop into a restricted superuser system path:

**1.** We drop a fake backdoor payload into the restricted `/root` directory:
```bash
sudo touch /root/test_virus.txt
```

**2.** We re-run system integrity inspection:
```bash
sudo aide -c /etc/aide/aide.conf --check
```

AIDE instantly flags the unauthorized directory tree modification, isolates the suspicious file artifact, highlights the warning string, and outputs the exact creation timestamp to the log.

When legitimate OS modifications occur (e.g., intentional package upgrades or installing new binaries via APT), we must update our cryptographic hash database:

**3.** We trigger a baseline recalculation to generate an updated database snapshot:
```bash
sudo aideinit
```

**4.** We promote the updated system snapshot as our new operational baseline:
```bash
sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
```

**5.** We lock down the baseline file by setting the immutable attribute (prohibiting modifications or deletion even by `root`):
```bash
sudo chattr +i /var/lib/aide/aide.db
```

**6.** We unlock the immutable flag when performing authorized system maintenance or updating baselines post-`apt upgrade`:
```bash
sudo chattr -i /var/lib/aide/aide.db
```

> [!WARNING]
> We must account for the fundamental architectural limitation inherent to local integrity monitoring systems. If an adversary bypasses our outer defensive perimeter (UFW, AppArmor, Firejail) and escalates privileges to full `root`, they can trivially disarm local AIDE protections. An attacker can simply execute `sudo aide --update` immediately after dropping a payload, effectively legitimizing malicious state changes inside the local database.
> 
> To guarantee uncompromising integrity enforcement for the baseline data, immediately after executing Step 4, back up your primary `/var/lib/aide/aide.db.gz` file onto a physically isolated, hardware-configured **Write-Protect** USB drive.

During routine integrity sweeps, we mount this write-protected drive in read-only mode and execute inspection by passing the path of the isolated external database:

**7.** We execute an integrity sweep pointing strictly to our air-gapped, write-protected media:
```bash
sudo aide --config=/media/user/secure_flash/aide.conf --check
```

Replace `/media/user/secure_flash/` with your real mount path. This offline verification strategy renders any local attempt by an attacker to overwrite or tamper with local baseline logs entirely useless.

> [!NOTE]
> Out of the box, Ubuntu's default AIDE detection rules enforce aggressive security baselines (using `Hbrps` and `High` macro policies). The engine verifies not just file size changes, but tracks `inode` shifts, hard link counts, extended permission attributes (`Mtime`/`Ctime`), and most critically, SHA-256/SHA-512 cryptographic hashes. This completely neutralizes Trojan Horse attacks where critical system binaries (such as `/usr/bin/sudo` or `/bin/ls`) are swapped with rogue variants while spoofing original file sizes.
  
<br>

## Automated System Security Auditing with Lynis

To put the final touch on our deep base OS hardening workflow, we must execute a comprehensive, independent security audit of our active deployment. To accomplish this, we utilize Lynis, an automated enterprise-grade security auditing tool. Installing the `lynis` package via standard `apt` repositories is strongly discouraged—distro-maintained database indexes age rapidly, triggering false positives while missing cutting-edge attack vectors. Instead, we pull the scanner direct from the developers' official Git repository, ensuring maximum signature acuity alongside total OS package sterility.

Since the scanner deploys temporary runtime binary modules during execution, we must completely purge the framework immediately post-audit and securely sanitize all local diagnostic artifacts using `shred`.

**1.** We launch our unprivileged user terminal session to provision a dedicated configuration path, embedding a custom desktop-hardened profile in a single monolithic command. This blinds the scanner to server bloat, false-positive GRUB triggers, and password rotation metrics, focusing runtime analysis exclusively on real workstation vulnerabilities:

```bash
mkdir -p ~/.config/lynis && nano ~/.config/lynis/custom.prf
```

**2.** We populate the file with explicit exclusions tailored to disarm server-centric checks:
```ini
# --- Desktop Exclusions for YubiKey & LUKS Architectures ---

# Disable password expiration enforcement (90-day rotation checks are irrelevant on hardened desktops)
skip-test=AUTH-9222
skip-test=AUTH-9226
skip-test=AUTH-9282
skip-test=AUTH-9286

# Disable brute-force account lockout requirements (faillock/tally handling)
skip-test=AUTH-9230

# Ignore false GRUB alert (GRUB is hardened via custom.cfg)
skip-test=BOOT-5122

# Bypass server-side ban daemons, PAM restrictions, and limits (obsolete with hardware keys)
skip-test=DEB-0880
skip-test=AUTH-9229
skip-test=KRNL-5820

# Partitioning rules (irrelevant for unified LUKS desktop builds)
skip-test=FILE-6310

# Disable USB port lockout (unusable for workstation environments reliant on hardware tokens)
skip-test=USB-1000

# Obscure network protocols
skip-test=NETW-3200

# Console legal login banners (unnecessary for personal workstations)
skip-test=BANN-7126
skip-test=BANN-7130

# Remote SIEM log forwarding
skip-test=LOGG-2154

# Total process accounting daemons (causes severe CPU overhead and battery drain on laptops)
skip-test=ACCT-9622
skip-test=ACCT-9626
skip-test=ACCT-9628

# Domain DNS validation
skip-test=NAME-4028

# Automation management engines (Ansible/Puppet—irrelevant for standalone hosts)
skip-test=TOOL-5002

# Compiler restrictions (blocks legitimate user-space software compilation)
skip-test=HRDN-7222

# Pre-install APT bug notifications (frequent spam vectors)
skip-test=DEB-0810
skip-test=TIME-3104
skip-test=PKGS-7394
skip-test=PKGS-7396

# Disable kernel module loading restrictions (preventing hardware token/Ledger blinding)
skip-test=KRNL-5788
skip-test=KRNL-5622

# Bypass iptables checks—firewall logic is handled externally
skip-test=FIRE-4513

# Bypass generic desktop file permission checks—already hardened throughout our setup
skip-test=FILE-7524

# Ignore default AIDE checksum check—our configuration enforces the H macro for max coverage
skip-test=FINT-4402

# Disable deep audit of systemd service configurations (unnecessary overhead for desktop builds)
skip-test=SRV-2300

# Disable server-centric update notifications and service restart triggers
skip-test=PKGS-7394
skip-test=PKGS-7396

# Disable suggestions for scheduled cron-based debsums execution
skip-test=PKGS-7370
```

> [!NOTE]
> This custom Lynis exclusion profile is meticulously tuned for desktop environments backed by YubiKey hardware authentication and full-disk LUKS encryption. Filtering out server-side metrics (password lifespans, USB disables) and heavy audit frameworks directs scanner intelligence straight to actionable workstation vulnerabilities.

**3.** We clone the latest upstream release of Lynis from its official repository into an isolated `/tmp/` host path:
```bash
sudo apt update && sudo apt install git && git clone [https://github.com/CISOfy/lynis.git](https://github.com/CISOfy/lynis.git) /tmp/lynis
```

**4.** We elevate to an interactive `root` session to grant the scanner low-level visibility across kernel interfaces and system logs:
```bash
sudo -i
```

**5.** **Critical OPSEC Step:** Because the source repository was cloned under an unprivileged user context, Lynis's strict internal security checks will trip an ownership error (Fatal error) when invoked as `root`. We explicitly reassign directory ownership of the temporary path to the superuser:
```bash
chown -R root:root /tmp/lynis
```

**6.** We enter the working directory and launch an interactive full-system audit, explicitly feeding our custom desktop profile into the scanner engine:
```bash
sh -c "cd /tmp/lynis && ./lynis audit system --profile /home/$SUDO_USER/.config/lynis/custom.prf"
```

*(The `$SUDO_USER` variable dynamically resolves your primary account name, mapping the exact path to your custom configuration).*

During execution, the scanner streams real-time telemetry to the console. Interpreting status indicators is straightforward:
* **Green Indicators** (*OK/Success*) — Security controls are properly hardened; no vulnerabilities detected.
* **Yellow Indicators** (*Warnings/Suggestions*) — Non-critical alerts or debatable parameters requiring review.
* **Red Indicators** (*Critical/Danger*) — Severe security vulnerabilities requiring immediate remediation.

Upon completing the scan, Lynis computes a normalized **Hardening Index** metric percentage and outputs a prioritized list of actionable **Suggestions**, each assigned a unique numeric identifier. Quoting these reference IDs into the search engine at `https://cisofy.com` provides vendor-backed step-by-step remediation procedures.

Once we review the audit metrics, we purge the scanner framework and all diagnostic output from the host to prevent leaving a digital blueprint of our security posture.

> [!WARNING]
> Leaving raw audit logs and scan reports unencrypted on disk is a severe operational security hazard. Should an attacker compromise user-space access, these detailed technical logs serve as an attacker-ready map detailing every defense gap across your host.

**7.** We terminate the privileged superuser shell, dropping back to our standard unprivileged user session:
```bash
exit
```

**8.** We destroy all local diagnostic artifacts, system logs, and the scanner tree via a 3-pass `shred` sweep before unlinking the temporary workspace entirely:
```bash
find /tmp/lynis/ -type f -exec shred -v -u -z -n 3 {} \; && rm -rf /tmp/lynis
```

> [!IMPORTANT]
> Even after completing rigorous kernel, file permission, and network hardening, Lynis will still output several yellow or red alerts (*Suggestions*) at the conclusion of the run. This is expected and legitimate scanner behavior. The Lynis platform was natively architected to audit high-exposure, enterprise-grade Linux servers.
> 
> Consequently, on a hardened desktop environment, the engine natively complains about missing local mail transfer agents (*Postfix/Sendmail*) or the absence of centralized log collectors (*Syslog-ng*). On a defensive workstation, spawning these background daemons introduces unnecessary attack surface by binding extra network sockets. This is precisely why we omitted them.
> 
> Our operational goal is driving the desktop **Hardening Index past the 75% threshold**, which represents an elite security posture for a local workstation.

At this stage, the base system security architecture and kernel hardening workflow for our Ubuntu Desktop host is complete. In the next section of the guide, we move on to provisioning isolated environments, running guest operating systems inside VirtualBox, and securely passing through hardware crypto wallets like the Ledger.
 
<br>

## Configuring Ubuntu/Xubuntu/Lubuntu Guest Systems in VirtualBox

#### Installing Guest Additions:

Following successful deployment and initial boot of an Ubuntu or lightweight variant (Xubuntu/Lubuntu) guest OS inside a virtual machine, installing official Guest Additions (*VirtualBox Guest Additions*) is the top priority. This enables video hardware acceleration, fluid GUI responsiveness, bidirectional shared clipboard support, and dynamic automatic display resolution scaling upon window resizing.

In the top menu bar of the VirtualBox management window, navigate to: **"Devices"** → **"Insert Guest Additions CD image..."**. Then open a system terminal inside the guest OS and execute the following sequence:

**1.** We update local repository indexes and install core compilation utilities, alongside the `bzip2` archiver (forcing a dependency update):
```bash
sudo apt update && sudo apt install -y gcc make perl dkms tar build-essential libbz2-1.0 bzip2
```

**2.** We dynamically fetch matching kernel headers for the active Linux kernel (using standard environment variable expansion to guarantee copy-paste compatibility):
```bash
sudo apt install -y linux-headers-$(env uname -r)
```

> [!WARNING]
> Modern distributions mount virtual optical drives and home directories with a restrictive `noexec` flag (prohibiting execution of binary assets) or outright block superuser script execution for operational security. Running the installer directly causes the Linux kernel to return a deceptive and misleading *«failed to open/No such file or directory»* error, even when the file resides right in front of us. To reliably bypass this system control, we must copy the installer into memory-backed temporary storage at `/tmp` and forcibly execute it from there using the `sh` interpreter:

**3.** We identify the block device identifier assigned to our Guest Additions drive (typically `sr0`):
```bash
lsblk
```

**4.** We unmount stale mountpoints (if present), forcibly mount the optical drive to `/mnt`, copy the additions installer to the system sandbox via `sudo`, switch context, and trigger driver compilation:
```bash
sudo umount /mnt 2>/dev/null; sudo mount /dev/sr0 /mnt && sudo cp /mnt/VBoxLinuxAdditions.run /tmp/ && cd /tmp/ && sudo sh ./VBoxLinuxAdditions.run
```
*(Note: Explicit `sudo` invocation during copying is required to access the contents of the mounted media, which is owned by `root` by default; execution from `/tmp` guarantees bypassing the `noexec` restriction).*

**5.** We issue a mandatory virtual machine reboot to fully initialize the newly compiled VirtualBox kernel drivers:
```bash
sudo reboot now
```

#### Installing Mozilla Firefox:

In select minimalist desktop distributions (such as Lubuntu), a pre-installed web browser may be entirely absent. We deploy the official classic binary build of Mozilla Firefox by bypassing native Snap packages and PPA repositories using a direct, isolated deployment methodology:

**6.** We pull the latest stable release archive directly into the root of the home directory:
```bash
wget -O ~/FirefoxSetup.tar.bz2 "https://download.mozilla.org/?product=firefox-latest-ssl&os=linux64&lang=en-US"
```

**7.** We unpack the downloaded archive directly into the current user's home folder (strictly without `sudo` privileges), fully preserving original access controls and filesystem security limits:
```bash
tar xjf ~/FirefoxSetup.tar.bz2 -C ~/
```

Our home directory now hosts a clean `firefox` folder containing the compiled `firefox` binary. The browser stands fully prepared for its initial standalone run and subsequent deep, uncompromising privacy and hardening configuration via the `about:config` engineering menu detailed in prior chapters.

#### Configuring Shared Folders in VirtualBox:

To establish secure configuration, script, and audit log exchange between our isolated guest environment and host OS, we leverage the Shared Folders interface. By default, Ubuntu security policies restrict access to hypervisor-mounted directories.

To grant read and write privileges, we execute the following steps in a terminal **inside the guest machine**:

**1.** We add the current active user to the trusted VirtualBox system group using a universal command:
```bash
sudo usermod -aG vboxsf $USER
```
*(Note: On Windows host architectures, access rights are managed automatically by the hypervisor installer; permission controls are configured strictly inside the guest Linux OS).*

**2.** We reload user group memberships without requiring a full system reboot by re-initializing the active session:
```bash
su - $USER
```

> [!NOTE]
> When defining shared directories within VirtualBox settings, enforce the **"Auto-mount"** and **"Make Permanent"** flags. This ensures the shared directory automatically mounts upon every system boot under `/media/sf_FOLDER_NAME/`.

<br>

#### Installing Ledger Live in VirtualBox with Ubuntu/Xubuntu/Lubuntu:

For ultimate, zero-compromise cryptographic asset management, we deploy the official Ledger Live software client. Open the browser and pull the latest stable Linux build directly from the official developer endpoints: `https://download.live.ledger.com/latest/linux`.

Once the download finishes, open a system terminal in the guest OS and execute the following sequence:
 
**1.** We provision an isolated directory inside the home folder to house our cryptographic software stack:
```bash
mkdir ~/ledger_live
```

**2.** We change directory to the system downloads path where the executable payload landed:
```bash
cd ~/Downloads
```

**3.** We relocate the downloaded binary into our target path (wildcard `*` matching handles any release version tag):
```bash
mv ledger-live-desktop-*-linux-x86_64.AppImage ~/ledger_live/
```

**4.** We enter the target directory and grant execution rights to the binary container:
```bash
cd ~/ledger_live && chmod +x ledger-live-desktop-*-linux-x86_64.AppImage
```

**5.** We download and inject official hardware `udev` rules directly into the Linux kernel for Ledger hardware tokens:
```bash
wget -q -O - https://raw.githubusercontent.com/LedgerHQ/udev-rules/master/add_udev_rules.sh | sudo bash
```

> [!IMPORTANT]
> Without deploying these rules, the operating system and VirtualBox hypervisor cannot physically detect or mount the hardware wallet over USB.

**6.** We install the active user-space filesystem mounting hardware libraries (a mandatory prerequisite for modern Ubuntu 24.04/26.04 LTS environments):
```bash
sudo apt install libfuse2t64 && sudo apt install fuse3 -y
```

> [!NOTE]
> Without this dependency layer, binary containers wrapped in the `AppImage` format cannot initialize or launch across the system.

**7.** We execute Ledger Live inside our fully isolated, sterile guest deployment:
```bash
./ledger-live-desktop-*-linux-x86_64.AppImage
```

> [!WARNING]
> Ensuring Ledger Live recognizes physical hardware devices inside guest environments requires more than `udev` configuration. We must physically attach the Ledger token via USB, input the secret PIN code on the physical hardware interface, and enter the target application context (such as *Bitcoin* or *Ethereum*). 
> 
> Only then do we right-click the USB icon in the bottom-right status tray of the active VirtualBox window and select the listed Ledger hardware entry. The hypervisor will detach the token from the host and securely pass through a direct hardware tunnel into the isolated virtual host.

<br>

#### Running Ledger Live on the Primary Ubuntu Host OS

If we need to run Ledger Live directly on the primary host operating system rather than inside a virtual machine, we download the Linux build of Ledger Live via browser from `https://download.live.ledger.com/latest/linux` into the `Downloads` home directory.

**1.** We deploy additional Fuse dependencies:
```bash
sudo apt install libfuse2t64
```

**2.** We launch the Ledger Live AppImage container:
```bash
./ledger-live-desktop-*-linux-x86_64.AppImage --no-sandbox
```

On this strong cryptographic note, we put the final touch on engineering our personal, hardened computing environment.

**Stay tuned and Hack the Planet!!!** 🚀

<br>
<br>
<br>

## About the Author and Legal Information

**Guide Author:** EugeXo  
**Specialization:** Information Security, Linux Hardening, OPSEC.

#### Contact Information and Community Resources:

* **GitHub:** `https://github.com/EugeXo/`
* **Telegram:** `@EugeXoSecurity`
* **Jabber:** `eugexo@paranoici.org`
* **Email:** `eugexo@proton.me`

> [!NOTE]
> This work represents an entirely independent, non-commercial Open-Source initiative. This guide was authored not out of financial incentive, but to consolidate hands-on field experience and equip the InfoSec community with a vetted, deterministic blueprint for establishing trusted digital environments.
> 
> All materials are distributed freely and transparently. If this guide saved you time, spared you sleepless nights, and helped safeguard your personal data, then writing this book was worth every effort!