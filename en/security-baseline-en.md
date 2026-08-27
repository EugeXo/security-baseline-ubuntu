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
  * [Core Philosophy](#core-philosophy)
* [Baseline Protection: 12 Rules of Operational Hygiene](#baseline-protection-12-rules-of-operational-hygiene)
* [Understanding Anonymity, Privacy, and Security](#understanding-anonymity-privacy-and-security)
* [Installing Ubuntu 24.04/26.04 LTS](#installing-ubuntu-24042604-lts)
  * [Introduction](#introduction)
  * [Hardware Preparation Protocol](#hardware-preparation-protocol)
  * [Selecting the Distribution](#selecting-the-distribution)
  * [Step-by-Step Installer Walkthrough](#step-by-step-installer-walkthrough)
* [First Boot](#first-boot)
* [System Configuration](#system-configuration)
* [Getting Started with the Console](#getting-started-with-the-console)
  * [Initial Setup](#initial-setup)
  * [Disabling Automounting and Optional Tweaks](#disabling-automounting-and-optional-tweaks)
  * [Managing Console Shell History](#managing-console-shell-history)
  * [Configuring a Secure sudo Session Timeout](#configuring-a-secure-sudo-session-timeout)
  * [Creating the Checks Passed Verification File](#creating-the-checks-passed-verification-file)
* [Network and VPN Configuration](#network-and-vpn-configuration)
  * [For Ethernet (Wired Connection)](#for-ethernet-wired-connection)
  * [For Wi-Fi (Wireless Connection)](#for-wi-fi-wireless-connection)
  * [NetworkManager Hardening: Suppressing Local mDNS, LLMNR, Hostname Leaks, and Securing DNS](#networkmanager-hardening-suppressing-local-mdns-llmnr-hostname-leaks-and-securing-dns)
  * [Setting Up a VPN Connection](#setting-up-a-vpn-connection)
  * [Purging Compromising Bluetooth Components](#purging-compromising-bluetooth-components)
* [Security Configuration and GRUB Bootloader Hardening](#security-configuration-and-grub-bootloader-hardening)
  * [Setting a Password to Protect GRUB](#setting-a-password-to-protect-grub)
  * [Software IOMMU Hardening: Protecting RAM Against Kernel-Level DMA Attacks](#software-iommu-hardening-protecting-ram-against-kernel-level-dma-attacks)
* [Configuring the UFW Firewall With and Without a Kill Switch](#configuring-the-ufw-firewall-with-and-without-a-kill-switch)
  * [Setting Up the Firewall with a Kill Switch](#setting-up-the-firewall-with-a-kill-switch)
  * [Important Addition on Managing Rule Priority](#important-addition-on-managing-rule-priority)
  * [Alternative Configuration Setup (Without VPN / For Guest OS)](#alternative-configuration-setup-without-vpn--for-guest-os)
* [Kernel Tuning, Access Control, and Purging Unnecessary System Services](#kernel-tuning-access-control-and-purging-unnecessary-system-services)
  * [Protecting the Network Stack and Kernel Memory Subsystem](#protecting-the-network-stack-and-kernel-memory-subsystem)
  * [Low-Level sysctl Hardening: Mitigating TCP Timestamp Fingerprinting](#low-level-sysctl-hardening-mitigating-tcp-timestamp-fingerprinting)
  * [Blocking Rare Network Protocols and Legacy Filesystems](#blocking-rare-network-protocols-and-legacy-filesystems)
  * [Filesystem Access Control Hardening](#filesystem-access-control-hardening)
  * [Securely Mounting Shared Memory](#securely-mounting-shared-memory)
  * [Configuring Wi-Fi to Default Off on Boot](#configuring-wi-fi-to-default-off-on-boot)
  * [Cutting Off Video Streams and Audio Recording](#cutting-off-video-streams-and-audio-recording)
  * [Removing Printing Services and Local Network Discovery Services](#removing-printing-services-and-local-network-discovery-services)
  * [Masking Geolocation and Timezone](#masking-geolocation-and-timezone)
* [Configuring Repositories and System Updates](#configuring-repositories-and-system-updates)
  * [Updating the System](#updating-the-system)
  * [Deploying the NVIDIA Graphics Stack in Isolated Mode](#deploying-the-nvidia-graphics-stack-in-isolated-mode)
* [Terminal Environments in Ubuntu](#terminal-environments-in-ubuntu)
  * [Replacing Gnome Terminal and Ptyxis with Ghostty](#replacing-gnome-terminal-and-ptyxis-with-ghostty)
  * [Optional! Ubuntu 26.04 — Restoring Gnome Terminal and Removing Ptyxis](#optional-ubuntu-2604--restoring-gnome-terminal-and-removing-ptyxis)
* [Removing and Blocking Snap and Telemetry](#removing-and-blocking-snap-and-telemetry)
  * [Purging Snap](#purging-snap)
  * [Ripping Out Canonical Telemetry](#ripping-out-canonical-telemetry)
  * [Purging the Background Firmware Tracker fwupd](#purging-the-background-firmware-tracker-fwupd)
* [Installing Security Utilities: libpam-tmpdir, debsums, and the Btop System Monitor](#installing-security-utilities-libpam-tmpdir-debsums-and-the-btop-system-monitor)
  * [The libpam-tmpdir Security Utility](#the-libpam-tmpdir-security-utility)
  * [The debsums Utility](#the-debsums-utility)
  * [Btop: A Streamlined Resource Monitor](#btop-a-streamlined-resource-monitor)
  * [Monitoring Network Ports and Active Connections](#monitoring-network-ports-and-active-connections)
* [Creating Golden Restore Points: Deploying and Configuring Timeshift](#creating-golden-restore-points-deploying-and-configuring-timeshift)
  * [Introduction](#introduction-1)
  * [Timeshift Mechanics in an Encrypted Environment (LUKS + GRUB)](#timeshift-mechanics-in-an-encrypted-environment-luks--grub)
  * [Securely Installing Timeshift](#securely-installing-timeshift)
  * [Initial Configuration and Creating Snapshot #1 (Sterile Baseline)](#initial-configuration-and-creating-snapshot-1-sterile-baseline)
  * [Ongoing Control Strategy: Creating Snapshot #2 (Pre-Operational)](#ongoing-control-strategy-creating-snapshot-2-pre-operational)
  * [Emergency Rollback Protocol (System Compromised or Broken)](#emergency-rollback-protocol-system-compromised-or-broken)
* [Installing a Clean .deb Release of Firefox and Removing the Snap Stub](#installing-a-clean-deb-release-of-firefox-and-removing-the-snap-stub)
* [Installing and Hardening Privacy Settings in Mozilla Firefox](#installing-and-hardening-privacy-settings-in-mozilla-firefox)
  * [Preparing the System for Tuning](#preparing-the-system-for-tuning)
  * [Initial GUI Privacy Configuration (Mandatory for Everyone)](#initial-gui-privacy-configuration-mandatory-for-everyone)
  * [Configuring Private DNS Providers (DNS over HTTPS)](#configuring-private-dns-providers-dns-over-https)
  * [Hardening Automation: Creating the user.js Configuration File](#hardening-automation-creating-the-userjs-configuration-file)
  * [Deploying Ultimate Security Extensions](#deploying-ultimate-security-extensions)
* [Installing and Configuring the Portmaster Interactive Network Firewall](#installing-and-configuring-the-portmaster-interactive-network-firewall)
  * [Introduction](#introduction-2)
  * [Preparation, Initial Kernel Initialization, and Upgrading](#preparation-initial-kernel-initialization-and-upgrading)
* [Guaranteed Data Destruction and Sterilizing Your Digital Footprint](#guaranteed-data-destruction-and-sterilizing-your-digital-footprint)
  * [Introduction](#introduction-3)
  * [Anatomy of a Digital Footprint: Why Deleting Files Is Useless Without Metadata Sanitization](#anatomy-of-a-digital-footprint-why-deleting-files-is-useless-without-metadata-sanitization)
  * [Installing and Sanitizing Metadata with MAT2](#installing-and-sanitizing-metadata-with-mat2)
  * [Secure and Irreversible File and Directory Destruction](#secure-and-irreversible-file-and-directory-destruction)
  * [Operational Parameters for the shred Utility](#operational-parameters-for-the-shred-utility)
  * [Global Wiping of Unallocated Disk Space](#global-wiping-of-unallocated-disk-space)
* [Steganography, Obfuscation, and Anti-Forensics Trace Hiding in Ubuntu](#steganography-obfuscation-and-anti-forensics-trace-hiding-in-ubuntu)
  * [Introduction](#introduction-4)
  * [Linux Steganography: Concealing Files Within Media Content](#linux-steganography-concealing-files-within-media-content)
  * [The steghide Command-Line Utility](#the-steghide-command-line-utility)
  * [Stealth Concealment via the Advanced StegoForge Tool](#stealth-concealment-via-the-advanced-stegoforge-tool)
  * [Archive Concatenation (Quick Hack Without Third-Party Software)](#archive-concatenation-quick-hack-without-third-party-software)
  * [Text Obfuscation: Bypassing Automated Inspection Systems (DPI)](#text-obfuscation-bypassing-automated-inspection-systems-dpi)
  * [Analyzing Hidden Threats: File Extension Spoofing (BiDi Attacks)](#analyzing-hidden-threats-file-extension-spoofing-bidi-attacks)
* [Installing and Configuring the VeraCrypt Cryptographic Suite](#installing-and-configuring-the-veracrypt-cryptographic-suite)
  * [Introduction to VeraCrypt and Installation](#introduction-to-veracrypt-and-installation)
  * [Deep Security Tuning: RAM Key Protection (Paranoia Mode)](#deep-security-tuning-ram-key-protection-paranoia-mode)
  * [A Fundamental Security Tool: Creating Hidden Volumes](#a-fundamental-security-tool-creating-hidden-volumes)
  * [Ultimate Hardening: Configuring PIM and Hardware Keyfiles](#ultimate-hardening-configuring-pim-and-hardware-keyfiles)
  * [Real-World Threat Modeling: Why Paranoia Must Be Systemic](#real-world-threat-modeling-why-paranoia-must-be-systemic)
* [Using Yubico Security Keys](#using-yubico-security-keys)
  * [Introduction](#introduction-5)
  * [Installation](#installation)
  * [Implementing a Hardware Kill Switch via Kernel udev Rules](#implementing-a-hardware-kill-switch-via-kernel-udev-rules)
* [Installing and Configuring USBGuard](#installing-and-configuring-usbguard)
  * [Introduction](#introduction-6)
  * [Installation and Setup](#installation-and-setup)
* [Installing the KeePassXC Local Password Manager](#installing-the-keepassxc-local-password-manager)
  * [Introduction](#introduction-7)
  * [Vault Protection Scenarios](#vault-protection-scenarios)
  * [Installing the Software Suite](#installing-the-software-suite)
  * [Creating and Hardware-Securing the Database](#creating-and-hardware-securing-the-database)
  * [Deep Hardening of Internal Security Settings](#deep-hardening-of-internal-security-settings)
  * [Secure Data Entry via Protected Clipboard](#secure-data-entry-via-protected-clipboard)
* [Installing and Running the Wireshark Network Analyzer](#installing-and-running-the-wireshark-network-analyzer)
  * [Introduction](#introduction-8)
  * [Installing and Launching Wireshark](#installing-and-launching-wireshark)
  * [Critical Security Concept: Packet Capture Subsystem Security](#critical-security-concept-packet-capture-subsystem-security)
  * [Stealth Traffic Capture (Headless Console Mode)](#stealth-traffic-capture-headless-console-mode)
  * [Practical Wireshark Field Guide](#practical-wireshark-field-guide)
* [Installing and Managing the AppArmor Security System](#installing-and-managing-the-apparmor-security-system)
  * [Introduction](#introduction-9)
  * [A New Security Paradigm: Kernel Automation](#a-new-security-paradigm-kernel-automation)
  * [Practical Hardening of the AppArmor Subsystem](#practical-hardening-of-the-apparmor-subsystem)
* [Installing and Configuring the Firejail Isolated Sandbox](#installing-and-configuring-the-firejail-isolated-sandbox)
  * [Introduction](#introduction-10)
  * [Installing Firejail and Preparing the Sandbox](#installing-firejail-and-preparing-the-sandbox)
  * [Core Firejail Filtering Options (Reference)](#core-firejail-filtering-options-reference)
  * [Creating a Dedicated Hardened Firefox Profile](#creating-a-dedicated-hardened-firefox-profile)
  * [Airtight PDF Vault: Safely Opening Files in an Isolated Offline Mode](#airtight-pdf-vault-safely-opening-files-in-an-isolated-offline-mode)
  * [Sandboxing Image Viewer for Secure Media Inspection](#sandboxing-image-viewer-for-secure-media-inspection)
  * [KeePassXC Sandboxing Scenario](#keepassxc-sandboxing-scenario)
  * [Installing and Sandboxing the LibreOffice Suite](#installing-and-sandboxing-the-libreoffice-suite)
  * [Installing and Sandboxing GNU Image Manipulation Program (GIMP)](#installing-and-sandboxing-gnu-image-manipulation-program-gimp)
  * [Installing and Sandboxing VS Codium (Development IDE)](#installing-and-sandboxing-vs-codium-development-ide)
  * [Installing and Sandboxing LM Studio Bionic Local AI](#installing-and-sandboxing-lm-studio-bionic-local-ai)
  * [Securing Communications: Mandatory Isolation of Messengers and Crypto Infrastructure (Author's OPSEC Setup)](#securing-communications-mandatory-isolation-of-messengers-and-crypto-infrastructure-authors-opsec-setup)
  * [Installing and Sandboxing Telegram Desktop](#installing-and-sandboxing-telegram-desktop)
  * [Host Cryptographic Foundation: Generating and OPSEC-Protecting GnuPG Keys](#host-cryptographic-foundation-generating-and-opsec-protecting-gnupg-keys)
  * [Installing and Sandboxing the Psi+ Jabber Client](#installing-and-sandboxing-the-psi-jabber-client)
  * [Installing and Sandboxing Thunderbird (Encrypted Email Workflow)](#installing-and-sandboxing-thunderbird-encrypted-email-workflow)
  * [Automating the Defensive Perimeter (Firecfg Utility) and Customizing System Icons](#automating-the-defensive-perimeter-firecfg-utility-and-customizing-system-icons)
  * [Advanced Paranoia Mode: Sandboxing with Session Persistence via Overlay](#advanced-paranoia-mode-sandboxing-with-session-persistence-via-overlay)
* [Installing Rkhunter and Hunting Rootkits](#installing-rkhunter-and-hunting-rootkits)
* [Installing and Configuring the ClamAV Antivirus Scanner](#installing-and-configuring-the-clamav-antivirus-scanner)
  * [Introduction](#introduction-11)
  * [Installing ClamAV](#installing-clamav)
  * [Updating Signature Databases and Bypassing Network Blocks](#updating-signature-databases-and-bypassing-network-blocks)
  * [Structuring System Scans](#structuring-system-scans)
  * [Multithreaded Scanning (Hardening)](#multithreaded-scanning-hardening)
* [Installing and Configuring the VirtualBox Virtualization Environment](#installing-and-configuring-the-virtualbox-virtualization-environment)
* [Shrinking and Optimizing VDI Virtual Disks](#shrinking-and-optimizing-vdi-virtual-disks)
  * [Introduction](#introduction-12)
  * [Sanitizing a Windows Guest Virtual Machine](#sanitizing-a-windows-guest-virtual-machine)
  * [Sanitizing a Linux Guest Virtual Machine (Ubuntu/Kali Linux)](#sanitizing-a-linux-guest-virtual-machine-ubuntukali-linux)
  * [Final Virtual Disk Compaction on the Host Machine](#final-virtual-disk-compaction-on-the-host-machine)
* [Installing and Configuring the Docker Containerization Platform](#installing-and-configuring-the-docker-containerization-platform)
  * [Introduction](#introduction-13)
  * [What Is the Hidden Danger of Default Docker](#what-is-the-hidden-danger-of-default-docker)
  * [Deploying Docker in Rootless Mode](#deploying-docker-in-rootless-mode)
  * [Securing Docker Networking: Preventing UFW Firewall Bypass](#securing-docker-networking-preventing-ufw-firewall-bypass)
  * [Experimental Proof of Security (Verifying Non-Root Execution)](#experimental-proof-of-security-verifying-non-root-execution)
* [Installing and Configuring the AIDE File Integrity Monitoring System](#installing-and-configuring-the-aide-file-integrity-monitoring-system)
  * [Introduction](#introduction-14)
  * [Installing and Configuring AIDE](#installing-and-configuring-aide)
  * [Executing a Penetration Test (Validating Defense Mechanisms)](#executing-a-penetration-test-validating-defense-mechanisms)
* [Automated System Security Auditing with Lynis](#automated-system-security-auditing-with-lynis)
* [Configuring Ubuntu/Xubuntu/Lubuntu Guest Systems in VirtualBox](#configuring-ubuntuxubuntulubuntu-guest-systems-in-virtualbox)
  * [Installing Guest Additions](#installing-guest-additions)
  * [Installing Mozilla Firefox](#installing-mozilla-firefox)
  * [Configuring Shared Folders in VirtualBox](#configuring-shared-folders-in-virtualbox)
  * [Installing Ledger Live in VirtualBox with Ubuntu/Xubuntu/Lubuntu](#installing-ledger-live-in-virtualbox-with-ubuntuxubuntulubuntu)
  * [Running Ledger Live on the Main Host System (Ubuntu)](#running-ledger-live-on-the-main-host-system-ubuntu)
* [About the Author and Legal Information](#about-the-author-and-legal-information)
  * [Contact Information and Community Resources](#contact-information-and-community-resources)

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

Before diving into the hardcore technical hardening of our system, let's establish the foundation. Below are 12 ironclad rules of operational hygiene that must be memorized and followed without exception. Without understanding them, even the most advanced security tools will eventually prove entirely useless:

1. **Eliminate wireless peripherals in the secured perimeter whenever possible:** this includes Bluetooth and wireless tech (headsets, headphones, wireless keyboards, and mice). Any wireless interface expands the attack surface and requires trusting protocol stacks, device firmware, and security implementations.
2. **Ensure mandatory full-disk encryption (FDE)** of the system drive during OS installation. Set the cryptographic passphrase length to at least 24 random characters (including special symbols)!
3. **Perform scheduled periodic rotation of the OS authentication password.** Make the user password unique and sufficiently long (at least 16 characters recommended). When using hardware tokens, the password is not replaced but augmented with an additional defense factor.
4. **Activate password protection for the GRUB bootloader** to completely eliminate unauthorized access to kernel parameters and configuration editing during physical access to the PC.
5. **Implement a hardware token** (YubiKey or its legitimate equivalents) as a mandatory second factor of authentication (2FA) for system login and superuser command authorization.
6. **Purge all redundant software from the system.** This applies especially to closed-source proprietary software. Remember the core rule: fewer third-party services, daemons, and applications mean a smaller attack surface and fewer critical vulnerabilities.
7. **Keep the operating system perpetually updated.** Make it an ironclad rule to regularly check for and install system security updates using console tools.
8. **Continuously monitor network and interface states.** Pay close attention to which remote resources background connections are established with and where network traffic is routed.
9. **Regularly conduct internal host audits.** Periodically inspect the system (preferably 2–3 times a week) for rootkits, viruses, and system file integrity.
10. **Never run questionable executable files in the main system.** For safe testing, always use an isolated `Firejail` sandbox or virtual machines.
11. **Enforce strict protection against dangerous DMA (Direct Memory Access) attacks and password-protect BIOS/UEFI:** In BIOS/UEFI settings, forcibly set Thunderbolt/USB4 ports to maximum authorization mode (*Kernel DMA Protection*) to mitigate attack risks via external device DMA access. Set a password on BIOS/UEFI. Additionally, disable Sleep Mode entirely, as disk encryption keys remain in RAM in plaintext during this state.
12. **Lock the session forcibly whenever leaving the workstation, and shut down the computer completely when leaving for an extended period.**

> [!NOTE]
> The weakest element in any security system is often not software, but human action.
>
> In professional circles, there is a playful saying: "the main vulnerability sits between the chair and the keyboard."
>
> That is precisely why technical hardening must be accompanied by operational discipline: inspecting files before opening them, scrubbing metadata before publication, monitoring network activity, and maintaining a constant awareness of your threat model.

<br>

## Understanding Anonymity, Privacy, and Security

In everyday speech, these concepts are often mixed up, even though they describe distinctly different tasks.

**Anonymity** answers the question: "Can my actions be linked to my real-world identity?"
In an ideal system, an adversary sees the action itself, but cannot link it to a specific person in the physical world under any circumstances.

**Privacy** answers the question: "Do I control what information is collected about me and who gets access to it?"
The adversary knows the individual exists, but the individual controls which portion of the data can be transmitted outward.

**Security** answers the question: "Can I protect my system, data, and device from unauthorized access?"
The user remains in constant combat readiness inside their digital perimeter. The adversary may stand right at the gate, yet lack the capabilities to breach the system and exfiltrate data.

An encrypted laptop with a strong password improves security. However, if the user voluntarily posts all personal data on the internet, privacy is not enhanced. Using anonymization tools may complicate identifying the user, but it does not protect the system from malware. A well-secured system can be non-anonymous, and an anonymous system can be insecure.

**The goal of this guide is not to create an illusion of absolute protection or total online invisibility. The goal is to demonstrate options for building a system where the user understands which risks are being mitigated and which limitations remain.**

<br>

## Installing Ubuntu 24.04/26.04 LTS

#### Introduction:

This chapter covers installing the Linux operating system with security requirements in mind. It also includes the option to deploy the system onto external USB and Thunderbolt storage drives.

Before starting the installation, several critical factors must be taken into account. One of the most common risks is selecting the wrong drive for the bootloader installation.

In Linux, GRUB (GRand Unified Bootloader) typically handles system booting. During installation, it might be placed not on the intended drive, but, for example, on the EFI partition of another disk. As a result, the existing operating system may fail to boot correctly until the bootloader is repaired.

To rule out this scenario entirely, the most reliable method is to physically disconnect all internal HDDs and SSDs not involved in the target Linux installation before starting the process.

For a desktop PC, this usually requires only access to internal components and a standard screwdriver. On laptops, the procedure depends on device design and can be more complex.

Apple devices (especially modern MacBooks with the T2 chip and Apple Silicon) are not recommended for this setup due to hardware platform specifics, boot chain quirks, and Linux compatibility limitations.

> [!NOTE]
> This guide has been fully tested on **Ubuntu 24.04 LTS Noble Numbat (24.04.4)** and **Ubuntu 26.04 LTS Resolute Raccoon (26.04.0)**.
>
> Testing was conducted in **VirtualBox 7.2.x**, **VMware Workstation Pro 26H1**, as well as on bare-metal systems with integrated Intel graphics and discrete NVIDIA graphics adapters.

#### Hardware Preparation Protocol:

* **On a desktop PC:** Remove the side case panel, completely disconnect power from the mains, and unplug all storage drives except the target disk designated for the Linux installation. If M.2 NVMe drives are present, a screwdriver will be required to remove them.

* **On a laptop:** Power off the device completely, disconnect the AC adapter, and disconnect the battery if possible. After removing the bottom cover, disconnect or remove all storage drives except the target drive.

If installing onto an external USB or Thunderbolt drive, keep only that specific drive connected. It will serve as the target media for the system installation.

> [!WARNING]
> Before installing the operating system, enter BIOS/UEFI and verify the graphics subsystem configuration. On laptops equipped with hybrid graphics, enable Hybrid Mode/Optimus to handle the core desktop interface via the CPU's integrated graphics processing unit. This allows using open-source Linux kernel drivers (i915, xe, amdgpu depending on hardware) and avoids unnecessary dependencies on proprietary components.
>
> Where available, set a BIOS/UEFI password and activate hardware-level drive protection (if supported by the specific SSD/HDD model). This mitigates the risk of unauthorized boot setting modifications and complicates attacks requiring physical access to the device.
>
> Check Secure Boot status. If the platform and deployment scenario support its correct operation, keep this feature enabled.
>
> **Keep only the target installation drive connected to the computer or laptop.**
>
> Perform the Linux installation **offline without internet connectivity** — disconnect the LAN ethernet cable and do not join wireless Wi-Fi networks. All necessary packages and updates will be deployed after completing the base system configuration.

Why perform an offline installation?

An offline installation minimizes external variables during the initial system deployment phase:

* Prevents active external network connections during installation;
* Eliminates automatic downloads of third-party components and updates prior to completing core setup;
* Reduces background network services and processes that might launch during the installation phase;
* Simplifies auditing the baseline state of the operating system and tracking initially installed components;
* Minimizes potential external attack vectors prior to completing initial system security hardening.

Once initial configuration and defense mechanisms are applied, re-establish network connectivity within a fully controlled environment.

#### Selecting the Distribution:

All demonstrations throughout this guide use current **Ubuntu 24.04 LTS Noble Numbat** and **Ubuntu 26.04 LTS Resolute Raccoon** releases. They are straightforward to master, resource-efficient, and run stably on PCs with as little as 2 GB of RAM (especially when opting for lightweight flavors like Xubuntu or Lubuntu). Furthermore, they offer extensive global Linux community support and, most importantly, a solid baseline security posture right out of the box.

Performing the installation in English is recommended. Should unexpected errors arise, troubleshooting and sourcing technical data on specialized English-language resources becomes significantly easier. However, this is not a strict requirement, and the final choice of system language remains up to you. This guide utilizes the English (US) localization.

#### Step-by-Step Installer Walkthrough:

**1.** After choosing the system language, proceed to the keyboard layout menu **"Select your keyboard"** and select **English (US)** or another preferred layout.

**2.** In the internet connection step, strictly select **"Do not connect to the internet"**.

**3.** Next, select the **"Interactive Installation"** and **"Default selection"** options — this ensures deploying a minimal software footprint on the system. If additional packages like office suites are needed later, install them manually from official repositories. Minimizing the initial software baseline directly reduces potential attack surface vectors.

**4.** In the following step, skip installing proprietary software.

**6.** **Ubuntu 24.04:** In the **"Disk Setup"** menu, click **"Advanced features..."**, choose **"Use LVM and encryption"**, confirm with **"OK"**, and click **"Next"**.

**Ubuntu 26.04:** Keep the default **"Erase disk and install Ubuntu"** selection and click **"Next"**.

**7.** **Ubuntu 24.04:** The next screen prompts for a master disk encryption passphrase. Create (and memorize) a strong passphrase at least 24 characters long (preferably longer), utilizing uppercase and lowercase Latin letters (A-Z, a-z), numbers (0-9), special characters, and spaces. Click **"Next"**.

**Ubuntu 26.04:** Select **"Encryption with passphrase"**, click **"Next"**, and enter a master disk encryption passphrase on the subsequent menu. Create (and memorize) a strong passphrase at least 24 characters long (preferably longer), utilizing uppercase and lowercase Latin letters (A-Z, a-z), numbers (0-9), special characters, and spaces. Click **"Next"**.

**8.** Next, the **"Create your account"** screen appears. Under **"Your name"**, enter a pre-selected neutral string that does not expose real identity (e.g., `user`). Under **"Computer name"**, assign an arbitrary hostname (e.g., `host-node`), and choose a username in the **"Pick a username"** field. In the **"Choose a password"** field, create a strong password at least 16 characters long using uppercase and lowercase Latin letters (A-Z, a-z), numbers (0-9), special characters, and spaces. Retain **"Require password to login"** and click **"Next"**.

**9.** The next menu presents a timezone map. Select any location (the timezone will be changed to UTC later) and click **"Next"**.

**10.** Review the configuration in the final overview window to ensure all parameters are set correctly, then click **"Install"**.

The operating system will now begin automatic installation and setup. The process completes quickly without requiring further interaction. Upon completion, the installer prompts to remove the installation USB drive and reboot the system. At this stage, installation is complete, and any previously disconnected storage drives can be safely reattached.

> [!IMPORTANT]
> Ubuntu 24.04/26.04 offers two fundamentally different approaches to on-disk data protection: traditional user-passphrase encryption and hardware-mediated encryption using automatic TPM unlocking. While both rely on LUKS as the underlying disk encryption engine, they differ primarily in the key retrieval mechanism.
> 
> This guide intentionally utilizes the traditional LVM + LUKS scheme with a lengthy user passphrase. This aligns with the chosen threat model, where the device owner must explicitly authenticate before decrypting the storage volume.
> 
> This does not imply that TPM-based FDE is inherently "insecure." It caters to a different operational model and carries distinct advantages, including automated platform integrity checks and mitigation against specific boot chain tampering attacks. However, within the scope of this guide, automatic disk unlocking is strictly avoided in favor of manual user authentication using a long LUKS passphrase.
> 
> Thus, choosing traditional LUKS in this book is a deliberate architecture decision based on the stated threat model, rather than a claim that TPM/FDE is generally unsafe.
> 
> Creating a strong manual passphrase via traditional LVM is the sole technically sound defense against physical access attacks on a powered-off machine under this threat model. When relying on automatic TPM unlocking, the user passphrase ceases to be the primary defense factor. In that scenario, security shifts to the trusted platform implementation, bootloader state, and hardware execution integrity. Manually entering a long LUKS passphrase completely eliminates this vector of compromise.

**Chapter Assets:** `_assets/images/1_os_install`

<br>

## First Boot

Log into the system using the disk encryption passphrase followed by the user account password. This account password will subsequently authorize administrative actions via `sudo`. Upon reaching the welcome wizard, click **"Next"**.

In Ubuntu 26.04, the next screen displays **"Location Services"**. The toggle defaults to the disabled position, so click **"Next"**. This menu is absent in Ubuntu 24.04.4.

In Ubuntu 24.04, the subsequent screen prompts to attach an *Ubuntu Pro* subscription — click **"Skip"** in the upper-right corner. This menu is absent in Ubuntu 26.04.0.

On the **"Help improve Ubuntu"** screen, select **"No, don't send system data"** (in 26.04, also ensure the "Share error reports with the Ubuntu team" toggle remains disabled). Click **"Next"** until reaching the final screen, then complete setup by clicking **"Finish"**. This disables transmitting diagnostic and telemetry data to Canonical.

> [!NOTE]
> Even after clicking **"Skip"**, Canonical retains active subscription-checking daemons running in the background. This is expected behavior; these components will be manually purged via the terminal in later steps.

**Chapter Assets:** `_assets/images/2_first_boot`

<br>

## System Configuration

By default, the left side of the desktop features a taskbar known as the **"Dock"**. Click the circular system menu icon in the corner of the panel (**"Show Apps"**) and select **"Settings"** (alternatively, access settings via the top panel: click the status menu in the top-right corner, select the gear icon, and open **"Settings"**).

Inside the system settings menu, toggle both **"Bluetooth"** and **"Wi-Fi"** switches to the off position. This places the system into Airplane Mode and temporarily disables wireless interfaces until permanent blocking is configured.

Next, customize the **"Dock"** panel under **"Ubuntu Desktop"**. For instance, move it to the bottom by setting **"Position on screen"** to **"Bottom"**, and adjust the **"Icon size"** slider. Disabling **"Panel Mode"** makes the **"Dock"** compact and detached, resembling the macOS panel layout. Clear any unneeded default application shortcuts from the panel.

Navigate to **"Privacy & Security"**, then access the **"Diagnostics"**/**"Telemetry"** sub-menu. Under **"Problem Reporting"**, strictly set **"Send error reports to Canonical"** to **"Never"**.

Proceed to the adjacent **"File History & Trash"** section. Here, completely disabling **"File History"** is critical. Enable both **"Automatically Delete Trash Content"** and **"Automatically Delete Temporary Files"** options, setting the retention period to **"1 day"**.

> [!IMPORTANT]
> Automatic trash and cache purging serves as basic surface hygiene. To maintain operational security, sensitive files, passphrases, and logs must always be manually shredded via the terminal using low-level tools like `shred` (covered in detail later). This drastically complicates forensic recovery from storage media. Note that data sanitization varies by storage architecture: while `shred` works for traditional HDDs, modern SSD/NVMe drives are more reliably protected via full-disk encryption and proper cryptographic key destruction.

In the neighboring **"Location"** sub-menu, ensure the toggle is set to **"Off"** — the operating system has no operational need to track physical coordinates.

Under **"Screen Lock"**, configure the **"Blank Screen Delay"** duration. The default interval is 5 minutes, but setting it to 1–2 minutes significantly improves security. Enable the **"Automatic Screen Lock"** toggle. Within the same section, open **"Automatic Screen Lock Delay"** and set it to **"Screen Turns off"**, 30 seconds, or 1 minute at most (initiating a 30-second or 1-minute screen dimming sequence prior to locking). Additionally, enable **"Lock Screen Notifications"** and **"Lock Screen on Suspend"**.

Next, under **"Connectivity"**, disable **"Connectivity Checking"** to reduce automated background network probing performed by the system.

Under **"Thunderbolt"**: disable the controller entirely if no Thunderbolt peripherals are in use.

In Ubuntu 26.04, navigate to the newly introduced **"Cameras"** item under **"Privacy & Security"** and toggle the switch to the off position.

Under **"System"**, access the **"Date & Time"** sub-menu to adjust system time parameters. If preparing the host for high-anonymity workflows over secured VPN tunnels or the Tor network, disable **"Automatic Date & Time"**. Disabling automatic time synchronization and manually setting the timezone fits privacy-focused operational models. This guide enforces UTC as the single time standard throughout subsequent sections.

Under **"Keyboard"**, add required input layouts. The remaining settings tabs cover cosmetic and user-interface preferences, which require no specialized security configuration.

Under **"Sound"**, mute the microphone by clicking the icon next to **"Input Volume"**.

> [!NOTE]
> The **"Privacy & Security"** menu in Ubuntu 24.04/26.04 includes a key sub-menu: **"Device Security"**. This panel provides a visual status readout for **"Secure Boot"**. A green indicator confirms active secure boot state. Secure Boot verifies digital signatures across boot chain components, ensuring only trusted binaries matching UEFI security policies execute during startup.
>
> Warnings indicating an unprotected kernel signal that host hardware defense features are disabled in BIOS/UEFI. Operating without hardware-level protection compromises host security on powered-on or suspended machines, leaving volatile RAM exposed to physical cold-boot or memory acquisition attacks targeting cryptographic keys.
>
> The adjacent indicator displays **"Checks Passed"**/**"Protected"**. A text file will be generated later to inspect entries from this menu via CLI.

**Chapter Assets:** `_assets/images/3_system_settings`

<br>

## Getting Started with the Console

#### Initial Setup:

Launch the terminal via the application menu (**"Show Apps"**). Pin the terminal shortcut to the **"Dock"** panel for quick and convenient command-line access.

Ubuntu is based on Debian and utilizes the same `.deb` package format. Software deployment is handled via the APT package manager from official Ubuntu repositories. Manage and install these packages using APT, and execute administrative operations via `sudo` when necessary.

By default, after successful authentication, `sudo` caches the credentials for 15 minutes. During this window, subsequent `sudo` commands typically bypass the password prompt. This interval is excessive for a system with strict security requirements and will be reduced to 0–2 minutes at the end of the chapter.

Opening the terminal window displays a prompt containing the current username, network hostname, and current working directory, ending with a dollar sign **`$`**. This symbol indicates that the session is running in standard user mode. Prepend the `sudo` prefix to commands (e.g., `sudo apt update`) to execute most configuration tasks.

To drop into a fully interactive `root` superuser shell, use the `sudo -i` or `sudo -s` commands. The `sudo -i` command fully simulates a clean root login, loading its native environment variables, whereas `sudo -s` launches a root shell but retains the standard user's current environment variables. Use `sudo -i` to obtain a fully functional, short-term root session. Unlike `sudo -s`, this mode launches a login shell with the `root` environment, making it optimal for prolonged administrative operations. During normal operation, prefer executing isolated commands via `sudo` rather than transitioning into a persistent root session unnecessarily.

After successful password entry, the **`$`** symbol in the prompt changes to a hash mark **`#`**. This indicates the system has transitioned into superuser mode with maximum administrative privileges. Modification of any files, including kernel parameters, is permitted here, so proceed with extreme caution.

> [!IMPORTANT]
> Memorizing basic Linux terminal commands will make system navigation fast and efficient.

**GNOME Terminal Ubuntu 24.04**

The terminal in Ubuntu 24.04 offers convenient visual customization directly via the GUI menu. It supports Transparency and allows setting a precise color palette with Custom shade selection, making prolonged terminal workflows highly comfortable aesthetically.

Before starting core tasks, configure the terminal's appearance. In the upper-right corner of the window, next to the magnifying glass icon, click the **"Hamburger menu"** (three horizontal lines) and navigate to **"Preferences"**. In the opened **"Profiles"** tab, select the default **"Unnamed"** profile. Adjust colors, fonts, workspace dimensions, and window transparency to fit personal preferences.

The drawback is reliance on the older GTK3 stack and the absence of certain modern isolation and security mechanisms available to GTK4 applications.

**Ptyxis Ubuntu 26.04**

Before shifting to Ptyxis for regular use, configure it for better ergonomics. In the upper-right corner of the window, click the **"Hamburger menu"** (three horizontal lines) and navigate to **"Preferences"**. This opens the **"Appearance"** menu directly, offering pre-built visual presets for subsequent workflows. First, scroll down slightly and deactivate the **"Use System Font"** toggle, then select the required font size. A selection of color palettes is pre-installed; at the very top of **"Appearance"**, click the **"Show All Palettes"** dropdown and select the most suitable color scheme. For deeper color and font customization, direct editing of configuration files is required.

**Custom profile variant for Ptyxis.** 

**1.** Open the console and create a directory containing the custom profile file:
```bash
mkdir -p ~/.local/share/org.gnome.Ptyxis/palettes && nano ~/.local/share/org.gnome.Ptyxis/palettes/my-homebrew.palette
```

**2.** Paste the modified lighter dark-gray/deep-blue background parameters for the profile:
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

To save the configuration in the `nano` editor, press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**3.** Add slight transparency to the window. A value of `0.00` means full transparency, while `1.00` means completely opaque. Select the most appropriate value:
```bash
gsettings set org.gnome.Ptyxis.Profile:/org/gnome/Ptyxis/Profiles/$PTYXIS_PROFILE/ opacity 0.95
```

Next, close the console and relaunch it. The created profile should appear in the **"Palettes"** section. Via the **"Hamburger menu"** (three horizontal lines), navigate to **"Preferences"** -> **"Appearance"** -> **"Show All Palettes"**, locate the **"My Homebrew"** profile, and select it.

> [!IMPORTANT]
> It is important to understand that when comparing Ptyxis and GNOME Terminal, the former better aligns with the security model adopted in this book due to its advanced workspace isolation capabilities. Therefore, replacing Ptyxis with the more familiar GNOME Terminal means sacrificing some of these features and acts primarily as a compromise in this scenario.
> 
> Ghostty will also be examined later as an alternative terminal emulator. Its installation and basic configuration will be covered separately, allowing readers to compare it against Ptyxis and GNOME Terminal to select the most suitable option for their system.

#### Disabling Automounting and Optional Tweaks:

**1.** Disable automatic mounting of removable media (prevents automatic mounting while still permitting manual mounting by the user or an application):
```bash
gsettings set org.gnome.desktop.media-handling automount false && gsettings set org.gnome.desktop.media-handling automount-open false
```

**2.** Center newly launched application windows on the screen. This layout improves workflow, particularly inside virtual machines:
```bash
gsettings set org.gnome.mutter center-new-windows true
```

If this window placement proves undesirable, execute the same command replacing `true` with `false`.

**3.** Revert the keyboard layout switching shortcut to the classic `Shift + Alt` combination using two rapid system commands instead of navigating graphical menus:
```bash
gsettings set org.gnome.desktop.input-sources xkb-options "['grp:alt_shift_toggle']" && gsettings set org.gnome.desktop.wm.keybindings switch-input-source "['<Shift>Alt_L', '<Alt>Shift_L']"
```

#### Managing Console Shell History:

By default, Bash retains a command history of limited size: older entries are eventually displaced, and multiple concurrently open terminals can create race conditions during history preservation. Furthermore, history is typically written to disk upon shell termination rather than after each individual command. In the event of an unexpected system shutdown, recently executed commands might fail to commit to the history file, which is undesirable for auditing workflows.

Configure Bash to record command history immediately and expand its capacity to prevent data loss regarding executed actions.

**1.** Open the `.bashrc` configuration file in the home directory:
```bash
nano ~/.bashrc
```

**2.** Jump to the end of the file using **`Alt + /`** and append the following lines:

```bash
# Unlimited history size
export HISTSIZE=-1
export HISTFILESIZE=-1

# Immediately append command to history file after pressing Enter
export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"

# Ignore consecutive duplicates only
export HISTCONTROL=ignoredups

# Log exact execution timestamp
export HISTTIMEFORMAT="%F %T "

# Append commands to file instead of overwriting
shopt -s histappend
```

Save the file via **`Ctrl + O`** -> **`Enter`**, then exit via **`Ctrl + X`**.

* `HISTSIZE=-1` and `HISTFILESIZE=-1` — Remove all limits on history line counts.
* `history -a` — Forces appending the executed command to disk immediately after execution.
* `ignoredups` — Filters out sequential duplicate commands while retaining commands preceded by spaces.
* `HISTTIMEFORMAT` — Captures timestamps, which is critical for incident response and forensic audits.
* `shopt -s histappend` — Merges logs across parallel open terminal instances.

**3.** Apply settings to the current session without restarting the terminal:
```bash
source ~/.bashrc
```

**4.** Verify that the updated logging mechanism is active:
```bash
history
```

The shell now maintains a unified, persistent chronology with precise timestamps for every executed command.

**5.** Clear terminal screen clutter:
```bash
clear
```

**6.** If sensitive data (such as a passphrase or API token) is inadvertently entered into the console during operation, it must not remain in the logs. To purge only the single last erroneous entry, execute:
```bash
history -d $(history | tail -n 1 | awk '{print $1}')
```

**7.** To completely purge the active session history and overwrite the log file on disk, execute a combined clear-and-write sequence:
```bash
history -c && history -w
```
The `-c` flag flushes the active terminal's in-memory history buffer, while `-w` forcibly writes this empty state to the history file on disk, erasing prior logs.

Even with real-time, persistent history recording configured, a standard user (or an adversary with session access) can still manually purge the log file via `history -c && history -w` or remove it entirely using `rm ~/.bash_history`.

Modifying standard file permissions via `chmod -w` is ineffective here: revoking write access completely prevents the Bash shell from appending new commands. The file must be configured as *append-only*, explicitly blocking *overwriting or deletion*.

Linux file system attributes (`chattr`) resolve this requirement.

**8.** Elevate to superuser mode, as modifying file system attributes requires root privileges:
```bash
sudo -i
```

**9.** Assign the `+a` (append-only) attribute to the history file. Using the `$SUDO_USER` system variable dynamically references the unprivileged user account while operating inside the root shell:
```bash
chattr +a /home/$SUDO_USER/.bash_history
```

**10.** Should administrative maintenance require purging or editing this log file in the future, strip the protective attribute using:
```bash
chattr -a /home/$SUDO_USER/.bash_history
```

Re-apply the `+a` attribute immediately upon completing maintenance.

> [!IMPORTANT]
> The `append-only` attribute is not an absolute barrier. Any user with root privileges can strip the attribute and modify or delete the history log. Treat this control as a supplementary hardening layer rather than an immutable audit log.

#### Configuring a Secure sudo Session Timeout:

To enforce a custom password timeout duration in the terminal, create a dedicated configuration snippet. Editing the main system file `/etc/sudoers` directly is discouraged to avoid syntax errors that could lockout administrative access.

**1.** Open the `nano` text editor to create a isolated drop-in configuration file:
```bash
nano /etc/sudoers.d/99_sudo_timeout
```

**2.** Insert the following directive into the blank file:
```ini
Defaults timestamp_timeout=2
```

The value `2` instructs `sudo` to cache successful authentication credentials for two minutes. Once this interval expires, subsequent `sudo` invocations prompt for the password again. Setting this value to `0` forces `sudo` to require a password on every invocation, providing maximum credential isolation for hardened hosts.

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the root shell.

**3.** Restrict file permissions on the newly created configuration snippet:
```bash
chmod 0440 /etc/sudoers.d/99_sudo_timeout
```

> [!WARNING]
> Prior to closing the terminal or exiting the root shell, verifying configuration syntax with the following command is mandatory:
> ```bash
> visudo -c
> ```
> A response returning `...parsed OK` confirms zero syntax errors and a safe configuration state. If the utility flags a syntax error, reopen the file immediately via `nano` to correct it. Failing to fix errors prior to closing the session breaks administrative access via `sudo`!

**Author's Note:** The `visudo` utility validates syntax exclusively for the privilege delegation framework (`/etc/sudoers` and drop-in files inside `/etc/sudoers.d/`). When modifying other system files (such as network configurations, Firefox `user.js` files, firewall rules, or GRUB parameters), running `visudo -c` is unnecessary and serves no purpose.

**4.** Exit superuser mode and drop back into the standard unprivileged user session:
```bash
exit
```

**5.** A helpful operational tip: to instantly invalidate the active `sudo` authentication token without waiting for the two-minute timeout to expire, execute:
```bash
sudo -k
```

Executing `sudo -k` immediately revokes active `sudo` credentials, ensuring the next `sudo` invocation requires password authentication.

#### Creating the Checks Passed Verification File:

**1.** Create a text file to log the **"Privacy & Security"** -> **"Device Security"** -> **"Checks Passed"** overview:
```bash
touch ~/Downloads/checks_passed.txt
```

**2.** Open the newly created file in the `nano` editor:
```bash
nano ~/Downloads/checks_passed.txt
```

**3.** Paste the contents copied to the clipboard into `checks_passed.txt`:
```ini
COPIED CLIPBOARD VALUES
```

To save the file in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit.

> [!NOTE]
> Resolving failed checks depends on specific machine hardware and operational goals. For instance, **Intel GDS Mitigation: !Fail (Not Enabled)** indicates that defenses against the Gather Data Sampling (GDS) vulnerability are currently inactive. This state typically stems from CPU microcode, kernel parameters, or system configurations. Enabling this mitigation performance penalties in specific workloads, so decision-making should align with processor architecture, usage profile, and threat model requirements.
> 
> The **Linux Swap: !Fail (Not Encrypted)** line may initially cause concern. However, if swap resides inside a LUKS-encrypted volume, swap data on disk remains fully encrypted. Consequently, this warning does not indicate that swap data sits unencrypted on the physical drive.
> 
> Verify swap placement and path using the following command:
> ```bash
> swapon --show
> ```
> 
> If the output references `/swap.img`, swap is operating as a file located inside the root file system. Because the root file system sits inside a LUKS-encrypted volume under this deployment model, all contents written to the swap file inherit that underlying encryption.

**Chapter Assets:** `_assets/images/4_start_terminal`

<br>

## Network and VPN Configuration

#### For Ethernet (Wired Connection):

Without connecting the network cable, navigate to system **"Settings"** and select the **"Network"** tab. Locate the **"Wired"** entry and click the **"Network Options"** gear icon. Inside the opened window, navigate to the **"Details"** tab and immediately uncheck both **"Make available to other users"** and **"Connect automatically"**.

Navigate to the **"Identity"** tab. Under the **"MAC Address"** dropdown, select the active network interface. Take note of its interface name displayed alongside (e.g., `enp0s1`, `ens33`, or similar), as recording this exact identifier is critical for subsequent firewall and network hardening steps.

Transition to the **"IPv4"** tab to enforce custom DNS resolution and bypass ISP-provided DNS servers. Toggle the **"DNS"** switch from **"Automatic"** to **"Off"** and enter Quad9 resolvers separated by a comma: `9.9.9.9, 149.112.112.112`. This routes name resolution outside the local provider's infrastructure.

Under the **"IPv6"** tab, set the **"IPv6 Method"** strictly to **"Disable"**. Click **"Apply"** after making all adjustments.

> [!IMPORTANT]
> Disabling IPv6 via the GUI applies exclusively to the selected network profile. To prevent potential real IP leaks over the IPv6 protocol (IPv6 Leak) across all VPN configurations, IPv6 will be forcibly disabled globally at the kernel level via `sysctl.conf` in a subsequent chapter.

> [!NOTE]
> **Note:** The exact network interface name can also be verified from the CLI using the `ip a` command.

Under the **"Cloned Address"** field, physical address spoofing can be configured. Specifying a MAC address like `08:00:27:E5:CA:C1`, for example, causes the interface to mimic a VirtualBox virtual machine. However, selecting **"Random"** provides superior daily operational privacy by generating a new MAC address upon every profile connection. If deploying Ubuntu inside a virtual machine, leave **"Cloned Address"** blank.

In Ubuntu 24.04/26.04, NetworkManager profile settings map through the Netplan backend; precise MAC address spoofing rules can be explicitly set via NetworkManager configurations directly when required.

#### For Wi-Fi (Wireless Connection):

**1.** Check and record the network interface identifier (required for subsequent configuration tasks):
```bash
ip a
```

After executing this command, jump to the **Bare-Metal PC or Laptop Configuration (Full Randomization)** section below, follow those steps sequentially, and then return to this section.

Access **"Settings"** via **"Show Apps"**, select the **"Wi-Fi"** section, and toggle the main switch to the active position. Nearby active Wi-Fi access points or the target network will appear. Click the target network name. In the authentication prompt, click **Cancel**, which surfaces a gear icon next to the network name. Under the **"Details"** tab, uncheck both **"Make available to other users"** and **"Connect automatically"**.

Navigate to the **"Identity"** tab. Under **"MAC Address"**, select the active network interface, and set **"Cloned Address"** to **"Random"**.

Transition to the **"IPv4"** tab to enforce custom DNS resolution and bypass ISP-provided DNS servers. Toggle the **"DNS"** switch from **"Automatic"** to **"Off"**, then enter non-logging Quad9 resolvers in the input field: `9.9.9.9` (alternative: `149.112.112.112`).

Under the **"IPv6"** tab, set the **"IPv6 Method"** strictly to **"Disable"**.

Access the **"Security"** tab and enter eight arbitrary random characters into the passphrase field, which activates the **"Apply"** button. Click **"Apply"** to save all configured parameters simultaneously. Entering the authentic network password is also acceptable, as active network connections remain blocked. However, entering arbitrary characters provides an extra precaution until preparing the initial connection for system updates.

Disable Wi-Fi by toggling the main switch to the inactive position.

* **Bare-Metal PC or Laptop Configuration (Full Randomization)**

For physical hardware, generating a completely new randomized MAC address upon every network connection provides optimal operational security. Configuration files inside `conf.d` parse in lexicographical order, so the `99-...` filename prefix ensures these directives override standard configuration parameters.

**1.** Elevate to superuser mode:
```bash
sudo -i
```

**2.** Create a high-priority configuration drop-in file:
```bash
nano /etc/NetworkManager/conf.d/99-macrandom.conf
```

**3.** Insert the following directive block to enable automatic address spoofing:
```ini
[device]
wifi.scan-rand-mac-address = yes

[connection]
ethernet.cloned-mac-address = random
wifi.cloned-mac-address = random
```

Save the file in `nano` via **`Ctrl + O`** -> **`Enter`**, then exit via **`Ctrl + X`**.

**4.** Restart the network service to apply configuration changes immediately:
```bash
systemctl restart NetworkManager
```
The system will now generate a new random MAC address upon establishing every new network connection.

**5.** Perform final verification following the service restart (replace `enp0s1` with the actual target interface name):
```bash
ip link show enp0s1
```

> [!TIP]
> To avoid typing full interface identifiers manually, enter the initial letter of the target interface type (`e` for wired ethernet, `w` for wireless) and press **`Tab`** to trigger command-line auto-completion.

A successful execution returns output displaying `link/ether "generated MAC" brd ff:ff:ff:ff:ff:ff permaddr "hardware MAC"` on the final line.

Note: When configuring Wi-Fi connections, return to the **Wireless Connection (Wi-Fi)** setup section.

* **Virtual Machine Configuration (Strict Vendor Spoofing)**

In virtualized environments running Ubuntu 24.04/26.04, the Netplan and NetworkManager stack blocks automatic MAC address randomization via the GUI, resetting the interface address back to the hypervisor's factory prefix (e.g., `00:0c:29:...` for VMware) upon every system reboot. This behavior immediately exposes virtual machine usage.

To permanently mask the system as physical desktop hardware while preserving full desktop environment functionality, enforce early boot-stage kernel MAC address overrides using the `rc.local` automation script.

**1.** Elevate to superuser mode:
```bash
sudo -i
```

**2.** Create the low-level system configuration script:
```bash
nano /etc/rc.local
```

**3.** Insert the following execution block (replace `enp0s1` with the actual target interface name):
```bash
#!/bin/bash
# Kernel-level strict MAC spoofing executed during boot (replace enp0s1 with target interface name)
ip link set dev enp0s1 down
ip link set dev enp0s1 address 28:80:8A:8F:32:7D
ip link set dev enp0s1 up
exit 0
```
Save the file in `nano` via **`Ctrl + O`** -> **`Enter`**, then exit via **`Ctrl + X`**.

> [!NOTE]
> The Linux kernel prohibits modifying the MAC address of an active network interface. Consequently, the script momentarily disables the interface, injects a legitimate Intel hardware MAC address, and immediately re-enables the interface prior to handing control to the graphical network manager.
>
> The Intel MAC address can be replaced with any valid MAC address corresponding to real physical hardware:
>
> * Example MAC: `00:E0:4C:A1:22:33` — Realtek chipset spoofing (prefixes: `00:E0:4C`, `FC:93:4E`, `50:3E:AA`, `00:13:70`, `00:23:CD`, etc.)
> * Example MAC: `04:92:26:BC:55:66` — ASUS laptop spoofing (prefixes: `04:92:26`, `04:D4:C4`, `04:D9:F5`, `08:60:6E`, `08:BF:B8`, etc.)
> * Example MAC: `28:80:8A:8F:32:7D` — Intel chipset spoofing (prefixes: `28:80:8A`, `28:7F:CF`, `28:C5:D2`, `14:85:7F`, etc.)
> * Example MAC: `3C:50:02:DC:1E:55` — Apple laptop spoofing (prefixes: `3C:50:02`, `60:81:10`, `A4:83:E7`, `00:1C:B3`, `00:17:F2`, etc.)
> * Example MAC: `00:14:22:F1:A8:D3` — Dell chipset spoofing (prefixes: `00:14:22`, `00:15:C5`, `00:21:70`, `74:86:7A`, `D0:94:66`, etc.)

**4.** Enforce strict permissions (**Critical**). Mark the script executable at the OS level to ensure execution by the kernel during system boot:
```bash
chmod +x /etc/rc.local
```

**5.** Reboot the virtual machine to test automated execution:
```bash
reboot
```

**6.** Open the terminal after system startup and run final verification (replace `enp0s1` with the actual target interface name):
```bash
ip link show enp0s1
```
The output line starting with `link/ether` must display the static Intel/Realtek spoofed MAC address, while the original hypervisor factory prefix remains hidden under the `permaddr` attribute. Graphical network control and VPN import capabilities remain fully functional.

#### NetworkManager Hardening: Suppressing Local mDNS, LLMNR, Hostname Leaks, and Securing DNS:

By default, `NetworkManager` may utilize mDNS (Multicast DNS) and LLMNR (Link-Local Multicast Name Resolution) mechanisms designed for local device discovery and hostname resolution within local network segments.

On public networks—such as those in cafes, co-working spaces, or hotels—these protocols can expose the host machine's hostname and reveal device presence to local network peers. These query broadcasts are particularly unwanted when a VPN tunnel is not active or temporarily drops, allowing local network traffic to route unencrypted via the primary interface.

Furthermore, dynamic network configuration can accept DNS server addresses pushed via DHCP by local routers. Depending on network configuration, this setup forces reliance on the access point or ISP's DNS infrastructure. To minimize local network query emissions and eliminate dependence on auto-assigned parameters, set static custom DNS servers and disable superfluous local name resolution mechanisms.

Create a dedicated `NetworkManager` configuration file to enforce these parameters.

**1.** Open the terminal and create the privacy hardening drop-in file:
```bash
sudo nano /etc/NetworkManager/conf.d/99-privacy-hardening.conf
```

**2.** Insert the following configuration block bound to local interface definitions:
```ini
[device-privacy]
match-device=file:/sys/class/net/e*,file:/sys/class/net/w*
# Completely disable mDNS across network connections
mdns = 0
# Suppress the LLMNR protocol entirely
llmnr = 0

[connection-privacy]
match-device=file:/sys/class/net/e*, file:/sys/class/net/w*
# Prevent DHCP deanonymization (suppress hostname transmission to local routers)
ipv4.dhcp-send-hostname = false
ipv6.dhcp-send-hostname = false
ipv4.dhcp-fqdn = none
ipv6.dhcp-fqdn = none
# Enforce ignoring DNS parameters pushed by the local router
# (Mitigates DNS traffic interception via rogue DHCP servers)
ipv4.ignore-auto-dns = yes
ipv6.ignore-auto-dns = yes
```
Save the file in `nano` using **`Ctrl + O`** -> **`Enter`**, then exit using **`Ctrl + X`**.

**3.** Restart the network service to apply privacy policies immediately:
```bash
sudo systemctl restart NetworkManager
```

**4.** For Netplan setups, execute `nmcli` referencing the exact target connection name (e.g., `Wired connection 1` or the specific Wi-Fi network SSID):
```bash
sudo nmcli connection modify CONNECTION_NAME ipv4.ignore-auto-dns yes
```

**5.** Set static custom DNS servers (specifying the target connection name):
```bash
sudo nmcli connection modify CONNECTION_NAME ipv4.dns 9.9.9.9
```

**6.** Restrict access permissions on the Netplan `yaml` configuration file:
```bash
sudo chmod 0600 /etc/netplan/01-network-manager-all.yaml
```

**7.** Apply Netplan parameters to enforce configuration changes without requiring a system reboot:
```bash
sudo netplan apply
```

**8.** Verify operational parameters (`-LLMNR`, `-mDNS`, `-DNSOverTLS`, and `DNSSEC=no/unsupported` indicate target hardened state):
```bash
resolvectl status
```

#### Setting Up a VPN Connection:

When utilizing a VPN connection, execute the steps outlined below; skip this section if no VPN is present.

In the same **"Network"** menu, directly beneath the **"Wired"** entry, resides the VPN configuration panel. The status defaults to * "Not set up" *. Click the plus sign to the right and select **"Import from file..."**. Select the pre-configured `.ovpn` profile file (e.g., from an encrypted USB drive) and import it. This completes basic profile deployment.

> [!WARNING]
> **Warning!** Running OpenVPN directly via the terminal in default mode does not protect against traffic leaks if the connection drops unexpectedly or the remote server fails. Enforcing a strict traffic block (Kill Switch) will be configured later using the host's native firewall.
> 
> Following successful import and VPN verification, access the newly created VPN profile settings, navigate to the **"IPv4"** tab, and explicitly set private DNS resolvers belonging to the specific VPN provider (typically an internal gateway such as `10.8.0.1`), or assign independent, privacy-focused, zero-log DNS addresses:
> 
> * *Mullvad DNS:* `194.242.2.2` (standard) or `194.242.2.3` (includes ad and tracker blocking). Maintained by one of the most privacy-focused and reputable VPN providers globally.
> * *Quad9:* `9.9.9.9`. Infrastructure hosted in Switzerland, adhering strictly to European privacy legislation while filtering phishing and malicious domains at the DNS level.
> * *Control D (Uncensored):* `76.76.2.0`. Fully independent, high-speed resolver operating without censorship, logging, or query restrictions.
> 
> **Network Protocol Isolation (Mitigating IPv6 Leaks):**
> Even if global UFW firewall configurations explicitly disable IPv6 processing (via `sudo sed -i 's/IPV6=yes/IPV6=no/' /etc/default/ufw`), the virtual tunnel interface (`tun0`) can override this rule during initialization. If the remote VPN server supports IPv6, the operating system may attempt to route traffic over IPv6, bypassing IPv4 Kill Switch rules.
> 
> To eliminate this data leak vector, immediately after importing the configuration, open the created VPN profile settings, navigate to the **"IPv6"** tab, and set the **"IPv6 Method"** toggle strictly to **"Disable"**.
> 
> **NetworkManager Architectural Security:**
> Upon successful GUI import, NetworkManager extracts all cryptographic keys into isolated system directories. The original `.ovpn` file stored on the USB drive can then be safely deleted.

In modern Ubuntu releases, importing complex configuration files containing specific routes via the standard GUI may fail due to strict security policies enforced by the `network-manager-openvpn` plugin. **If the graphical interface returns an import error, launching the session directly via the terminal is significantly more reliable.**

> [!IMPORTANT]
> Executing OpenVPN directly from user home directories (e.g., the `Downloads` folder) is strictly prohibited. Cryptographic keys and configuration profiles must reside in system directories protected by root-level access permissions; otherwise, compromising the unprivileged user session (e.g., via browser exploits) allows adversaries to exfiltrate VPN access credentials.

#### Purging Compromising Bluetooth Components:

The Bluetooth wireless protocol is rarely utilized; thus, fully disabling and isolating it yields significantly better security than continuously monitoring its over-the-air status. This protocol carries numerous known and zero-day (0-day) vulnerabilities, introducing dangerous attack vectors for proximate remote exploitation. In public spaces such as cafes or co-working environments, adversaries can exploit the kernel's Bluetooth stack to gain unauthorized remote control over the device.

**1.** Apply a software-level block to the Bluetooth transmitter at the kernel level (`soft-block`), preventing the chip from emitting radio signals:
```bash
sudo rfkill block bluetooth
```

**2.** Isolate the user-space Bluetooth stack entirely by disabling automated service execution during boot, appending the `--now` flag to terminate the daemon running in host memory instantly:
```bash
sudo systemctl disable --now bluetooth
```

**3.** Open the kernel module blacklist configuration file:
```bash
sudo nano /etc/modprobe.d/blacklist-hardening.conf
```

**4.** Append the following directives to enforce complete kernel-level Bluetooth driver isolation:
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

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

**5.** Finalize configuration changes by rebuilding the initial RAM filesystem image across all installed kernels:
```bash
sudo update-initramfs -u -k all
```

Following this execution, the Linux kernel cannot load corresponding drivers upon detecting a Bluetooth controller. The host treats the controller as non-functional hardware, preventing background software overrides by malware or covert rootkits.

> [!IMPORTANT]
> This mitigation eliminates 99.9% of remote attack vectors, though the controller remains powered electrically. Absolute isolation against advanced hardware-level rootkits requires physically disconnecting or desoldering the module from the motherboard.

**Chapter Assets:** `_assets/images/5_network_vpn`

<br>

## Security Configuration and GRUB Bootloader Hardening

#### Setting a Password to Protect GRUB:

To prevent unauthorized modification of Linux kernel parameters (*Evil Maid* attack vectors) when physical access is present, set an administrative password for the GRUB bootloader. Without this mitigation, anyone with physical access can alter boot directives, pass `init=/bin/bash` to the kernel, and bypass standard operating system authentication during early boot stages.

Open the terminal and execute the following steps sequentially:

**1.** Launch the hash generation utility. Enter and confirm the master password when prompted (use a strong passphrase at least 16 characters long):
```bash
grub-mkpasswd-pbkdf2
```

The utility outputs a hashed string starting with `grub.pbkdf2.sha512...`. Highlight and copy this string in its entirety.

> [!NOTE]
> On Ubuntu distributions, the primary GRUB configuration compiles dynamically from `/etc/default/grub` and scripts inside `/etc/grub.d/`. Syntax errors within these files can break `grub.cfg` generation when running `update-grub`.
> 
> To avoid modifying default generation scripts, isolate custom parameters inside `/boot/grub/custom.cfg`. GRUB sources this file directly during boot, decoupling user settings from automatically generated configurations.

**2.** Create a dedicated configuration snippet for bootloader authentication at the lowest initialization layer:
```bash
sudo nano /boot/grub/custom.cfg
```

**3.** Insert two lines declaring the superuser account and binding the generated password hash (without quotes or Bash syntax):
```text
set superusers="root"
password_pbkdf2 root COPIED_HASH_FROM_STEP_1
```

To save changes in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

By default, declaring a superuser locks down the entire bootloader, prompting for credentials during standard reboots. To allow the default operating system to launch automatically while prompting for passwords *only* when attempting unauthorized menu editing (key `e`) or accessing the command line interface (key `c`), unrestrict standard kernel entries.

**4.** Open the core generator template:
```bash
sudo nano /etc/grub.d/10_linux
```

**5.** Locate the directive starting with `CLASS=` (typically `CLASS="--class gnu-linux --class gnu --class os"`) and append the `--unrestricted` parameter:
```ini
CLASS="--class gnu-linux --class gnu --class os --unrestricted"
```
Save the file via **`Ctrl + O`** -> **`Enter`**, then exit via **`Ctrl + X`**.

**6.** Apply GRUB configuration updates at the OS level:
```bash
sudo update-grub
```

**7.** Enforce strict permissions on the created `custom.cfg` file, hiding the stored password hash from unprivileged system users:
```bash
sudo chmod 0600 /boot/grub/custom.cfg
```

> [!WARNING]
> Following these adjustments, standard Ubuntu boots bypass the GRUB password prompt, making it easy to forget due to rare usage. However, during emergency recovery (e.g., filesystem repairs or emergency maintenance), the bootloader will demand this passphrase. To prevent total loss of administrative control, record this credential on paper stored in a physical safe or save it inside an offline password manager database (such as KeePassXC). Detailed setup for this software is covered in subsequent chapters.

#### Software IOMMU Hardening: Protecting RAM Against Kernel-Level DMA Attacks:

Because the introduction established the necessity of defending against high-risk DMA (*Direct Memory Access*) attacks, disabling sleep mode and relying on BIOS/UEFI parameters alone is entirely insufficient. On many consumer laptops and motherboards, hardware authorization features for Thunderbolt and USB4 ports are deliberately hidden or completely omitted by manufacturers.

To guarantee uncompromising defense, enforce and configure the **IOMMU** subsystem at the GRUB bootloader level. This forces the CPU to isolate RAM address spaces at the hardware layer, completely blocking external hardware devices from directly accessing host RAM while bypassing the operating system.

> [!NOTE]
> To maintain operational hygiene, Linux kernel initialization parameters should be stored in a dedicated system drop-in directory. This shields low-level flags from accidental overwrite by package management tools during routine system updates.

Open the main host system terminal and execute the following steps sequentially:

**1.** Create an independent kernel security configuration file inside the extension drop-in directory:
```bash
sudo nano /etc/default/grub.d/99_security_baseline.cfg
```

**2.** Insert a single operational line into the opened file containing hardware memory isolation flags suited to your physical CPU architecture.

* **For Intel CPUs:**
```ini
GRUB_CMDLINE_LINUX_DEFAULT="${GRUB_CMDLINE_LINUX_DEFAULT} intel_iommu=on iommu=pt"
```

* **For AMD CPUs:**
```ini
GRUB_CMDLINE_LINUX_DEFAULT="${GRUB_CMDLINE_LINUX_DEFAULT} amd_iommu=on iommu=pt"
```

Save the configuration in `nano` by pressing **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit.

* **`intel_iommu=on/amd_iommu=on`** — Forces the CPU architecture-level IOMMU control driver to initialize during system startup.
* **`iommu=pt`** (*Pass-Through*) — Enables pass-through mode for internal host devices (such as integrated graphics adapters), applying direct address translations exclusively to legitimate built-in buses. This provides maximum default performance and stability.

> [!WARNING]
> When porting settings from this guide to bare-metal hardware (rather than virtual machines), replace `iommu=pt` (trusted pass-through mode) with `iommu=force`.
> This strict flag prevents the Linux kernel from automatically assigning newly attached hot-plugged external devices (especially via Thunderbolt/USB4/PCIe protocols) to trusted mode. The kernel strictly enforces DMA Translation tables across all interfaces without exception.
> **Perform a safe PC hardware verification test first:** Reboot the host, press **E** at the GRUB boot menu (enter the root username and the password configured in the previous step). In the kernel command line, replace `iommu=pt` with `iommu=force`. Press **`Ctrl + X`** to boot. If the desktop environment loads successfully without graphics freezes, Wi-Fi failure, or audio dropping, your hardware is fully compatible with strict hardening. Only after successful testing should this parameter be declared permanently!
> On VirtualBox and VMware virtual environments, the strict isolation flag `force` can trigger a GNOME desktop deadlock by blocking virtual display adapters (VMSVGA).

Save changes in `nano` using **`Ctrl + O`** -> **`Enter`**, then exit via **`Ctrl + X`**.

**3.** Update the bootloader configuration across the operating system to compile and lock in the new low-level directives:
```bash
sudo update-grub
```

**4.** Force a system reboot to apply hardware memory isolation:
```bash
sudo systemctl reboot -i
```

**5.** Following reboot, open the terminal and verify operation. Inspect the `dmesg` ring buffer using `sudo` privileges to verify security deployment and active RAM protection:
```bash
sudo dmesg | grep -E "iommu|IOMMU|dmar"
```

> [!IMPORTANT]
> Access BIOS/UEFI prior to boot and set Intel VT-d (Intel processors) or AMD-Vi/IOMMU (AMD processors) to Enabled. If left disabled, the kernel ignores boot parameters and logs an error.

> [!TIP]
> If terminal output displays entries such as *"DMAR: IOMMU enabled"*, *"DMAR: Intel-IOMMU"*, or confirms successful initialization of CPU hardware address translation tables, your system is hardware-protected against direct RAM exfiltration via rogue DMA attack boards!

> [!NOTE]
> **Optional configuration for Ubuntu 26.04:** If `unattended-upgrades` introduces excessive shutdown or reboot delays (disrupting standard `sudo reboot` operations), override `TimeoutStopSec` via a systemd drop-in without modifying the upstream package unit file.
> 
> Create the directory and configuration drop-in file:
> ```bash
> sudo mkdir -p /etc/systemd/system/unattended-upgrades.service.d && sudo nano /etc/systemd/system/unattended-upgrades.service.d/override.conf
> ```
> 
> Set a one-minute execution timeout:
> ```ini
> [Service]
> TimeoutStopSec=60
> ```
> 
> Reload systemd manager configuration:
> ```bash
> sudo systemctl daemon-reload
> ```
> 
> Verify active unit parameters (should output `TimeoutStopUSec=1min`):
> ```bash
> systemctl show unattended-upgrades.service -p TimeoutStopUSec
> ```

<br>

## Configuring the UFW Firewall With and Without a Kill Switch

#### Setting Up the Firewall with a Kill Switch:

In Ubuntu, while remaining disconnected from the internet, configure the host firewall via the terminal. Execute the following steps sequentially:

First, disable all IPv6 traffic processing in system firewall settings to eliminate covert data leaks.

**1.** Enable the firewall subsystem. It will now launch automatically on every system boot:
```bash
sudo ufw enable
```

**2.** Disable IPv6 support within the UFW configuration file:
```bash
sudo sed -i 's/IPV6=yes/IPV6=no/' /etc/default/ufw
```

**3.** Check firewall status. The service is active, running default rules:
```bash
sudo ufw status verbose
```

**4.** Block all incoming traffic and external connection attempts targeting the host:
```bash
sudo ufw default deny incoming
```

**5.** Enforce a global outbound traffic block. This action converts the firewall into a strict Kill Switch: it terminates data exfiltration across all ports, temporarily disabling internet access on the host:
```bash
sudo ufw default deny outgoing
```

**6.** Block packet forwarding across system interfaces:
```bash
sudo ufw default deny forward
```

**7.** Allow outbound traffic exclusively to the specific VPN server IP address and target port (select `udp` or `tcp` matching your `.ovpn` configuration). Replace placeholders `VPN_IP` and `PORT` with actual connection parameters:
```bash
sudo ufw allow out to VPN_IP port PORT proto udp
```

> [!IMPORTANT]
> If the VPN provider specifies a domain name in the configuration (e.g., `server.mullvad.net`), resolve its numeric IP address first and supply the static IP. Otherwise, the firewall blocks DNS resolution attempts, preventing tunnel establishment.

**8.** Allow outbound DNS traffic (port 53) strictly through the secured VPN interface, typically designated as `tun0`. Specify the corresponding interface name if your VPN uses a different identifier:
```bash
sudo ufw allow out on tun0 to any port 53 proto udp
```

**9.** Allow outbound HTTP traffic (port 80) routed exclusively through the VPN tunnel interface:
```bash
sudo ufw allow out on tun0 to any port 80 proto tcp
```

**10.** Allow outbound HTTPS traffic (port 443) routed through the VPN tunnel interface:
```bash
sudo ufw allow out on tun0 to any port 443 proto tcp
```

**11.** Display all active rules with assigned numerical IDs for straightforward management:
```bash
sudo ufw status numbered
```

**12.** Enable network activity logging. Available modes include `low`, `medium`, `high`, and `full`. The `medium` setting provides optimal balance for anomaly tracking without flooding system disks:
```bash
sudo ufw logging medium
```

To enable proper operation for local services and isolated development environments (e.g., VS Code, Portmaster, or LM Studio), append loopback interface (`localhost`) rules:

**13.** Allow all incoming loopback traffic within the host:
```bash
sudo ufw allow in on lo to any
```

**14.** Allow all outgoing loopback traffic within the host:
```bash
sudo ufw allow out on lo to any
```

**15.** Open port 853 across physical and virtual interfaces for secure DNS-over-TLS communication (required when utilizing Portmaster):
```bash
sudo ufw allow out to any port 853 proto tcp
```

**16.** Allow high-speed tunnel connections (QUIC/UDP) for traffic filtering engines operating inside the VPN:
```bash
sudo ufw allow out on tun0 from any to any proto udp
```

**17.** Perform a final firewall status verification. Firewall baseline deployment is complete:
```bash
sudo ufw status verbose
```

**18.** Edit UFW kernel runtime parameter rules using `nano`:
```bash
sudo nano /etc/ufw/sysctl.conf
```

**19.** Locate martian logging parameters near the end of the file and toggle their values from zero to one:
```ini
net/ipv4/conf/all/log_martians=1
net/ipv4/conf/default/log_martians=1
```

Save the configuration in `nano` via **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit.

**20.** Reload UFW to enforce updated firewall rules:
```bash
sudo ufw reload
```

**21.** Access the built-in manual page for utility operations (strongly recommended reading):
```bash
man ufw
```

#### Important Addition on Managing Rule Priority:

Occasions arise where blocking a specific malicious IP address or an entire subnet becomes necessary. For instance, while analyzing traffic in the Wireshark network monitor, you might notice persistent outbound connection attempts targeting IP addresses `84.17.56.74` and `84.17.56.91` over port 80. You can choose to block them individually or drop traffic to the entire subnet at once.

Understanding UFW logic is critical: rules process strictly from top to bottom. Simply appending a deny rule to the end of the list places it below the general outbound allow rule for port 80 (rule #9), causing the firewall to ignore the block and pass the packet. To enforce the restriction, insert it at the top of the chain using `insert N`, where `N` represents the target index number:

**1.** Enforce a hard connection block targeting a specific IP address on port 80. The rule takes index 1 and receives top evaluation priority:
```bash
sudo ufw insert 1 deny out to 84.17.56.74 port 80
```

**2.** Block outbound traffic targeting the entire `84.17.56.0/24` subnet on port 80:
```bash
sudo ufw insert 1 deny out to 84.17.56.0/24 port 80
```

**3.** Reload UFW to enforce updated firewall rules:
```bash
sudo ufw reload
```

To purge an erroneous rule, target its assigned numerical ID. Deleting a rule shifts the entire table upward, reindexing all subsequent rule numbers. Always query the updated numbered list before executing additional deletion commands:

**4.** Display the active rule table with current numerical IDs:
```bash
sudo ufw status numbered
```

**5.** Delete a rule assigned to index 5:
```bash
sudo ufw delete 5
```

#### Alternative Configuration Setup (Without VPN / For Guest OS):

If configuring a system without a VPN tunnel (e.g., inside an isolated guest OS in VirtualBox where traffic is already secured on the host machine), port authorization commands will utilize the `any` keyword. The complete deployment workflow proceeds as follows:

**1.** Enable the firewall subsystem:
```bash
sudo ufw enable
```

**2.** Disable IPv6 protocol support within the UFW configuration file:
```bash
sudo sed -i 's/IPV6=yes/IPV6=no/' /etc/default/ufw
```

**3.** Block all incoming traffic globally:
```bash
sudo ufw default deny incoming
```

**4.** Block all outgoing traffic globally:
```bash
sudo ufw default deny outgoing
```

**5.** Block all packet forwarding:
```bash
sudo ufw default deny forward
```

**6.** Allow outbound UDP DNS traffic (port 53) to any destination server:
```bash
sudo ufw allow out to any port 53 proto udp
```

**7.** Open standard outbound HTTP access (port 80) to any destination server:
```bash
sudo ufw allow out to any port 80 proto tcp
```

**8.** Open secure outbound HTTPS access (port 443) to any destination server:
```bash
sudo ufw allow out to any port 443 proto tcp
```

**9.** Allow all incoming loopback connections on the `lo` interface:
```bash
sudo ufw allow in on lo to any
```

**10.** Allow all outgoing loopback connections on the `lo` interface:
```bash
sudo ufw allow out on lo to any
```

**11.** Open outbound port 853 to any destination server for secure DNS-over-TLS protocol operation:
```bash
sudo ufw allow out to any port 853 proto tcp
```

**12.** Enable medium-level network activity logging:
```bash
sudo ufw logging medium
```

**13.** Verify the final active state of the configured firewall:
```bash
sudo ufw status verbose
```

**14.** Edit UFW kernel parameter configurations using `nano`:
```bash
sudo nano /etc/ufw/sysctl.conf
```

**15.** Locate martian packet logging directives near the bottom of the file and toggle values from zero to one:
```ini
net/ipv4/conf/all/log_martians=1
net/ipv4/conf/default/log_martians=1
```

Save the configuration in `nano` via **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit.

**16.** Reload UFW to enforce updated firewall rules:
```bash
sudo ufw reload
```

> [!IMPORTANT]
> Starting with Ubuntu 22.04, the legacy `iptables` framework is deprecated in favor of the high-performance `nftables` engine. The UFW utility serves strictly as a high-level frontend abstraction for `nftables`. To inspect raw low-level kernel rulesets, execute the modern command instead of legacy `sudo iptables -L`:
> ```bash
> sudo nft list ruleset
> ```

**17.** Audit local port posture:
```bash
ssh localhost
```

The terminal should output an explicit error: *"Connection refused"*. This confirms the remote management daemon is inactive, target ports remain closed, and system security state is verified.

<br>

## Kernel Tuning, Access Control, and Purging Unnecessary System Services

#### Protecting the Network Stack and Kernel Memory Subsystem:

Prior to connecting to the global network, execute critical hardening routines targeting the operating system kernel, baseline file permissions, and remote access service activity.

Harden the kernel network stack and memory subsystem. To achieve this, create a dedicated, isolated configuration file inside the `sysctl.d` directory. Execute all parameters strictly with elevated root privileges:

**1.** Enter an interactive root superuser session:
```bash
sudo -i
```

**2.** Create and open a new configuration drop-in file using `nano`:
```bash
nano /etc/sysctl.d/99-security-hardening.conf
```

Populate the newly created file with the following low-level kernel security directives:
```ini
# Buffer overflow protection (enabling ASLR)
kernel.randomize_va_space = 2

# IP spoofing protection via Reverse Path Filtering
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1

# Disable IP Source Routing
net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.default.accept_source_route = 0

# Ignore malicious broadcast ICMP requests and bogus error responses
net.ipv4.icmp_echo_ignore_broadcasts = 1
net.ipv4.icmp_ignore_bogus_error_messages = 1

# Log packets with impossible (spoofed) source addresses (Martian Packets)
net.ipv4.conf.all.log_martians = 1
net.ipv4.conf.default.log_martians = 1

# Fully disable IPv6 protocol at the kernel level to minimize attack surface
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

# SYN-Flood DoS mitigation
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_synack_retries = 3

# Disable ICMP redirect transmission (Host is not a router)
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0

# Restrict writing to untrusted FIFOs in world-writable sticky directories
fs.protected_fifos = 2

# Restrict writing to files owned by other users in world-writable sticky directories
fs.protected_regular = 2

# Append process PID to core dumps to prevent log overwrites
kernel.core_uses_pid = 1

# Hide kernel pointer addresses in /proc/kallsyms even from root to prevent exploit offset calculations
kernel.kptr_restrict = 2

# Restrict unprivileged access to the kernel log buffer
kernel.dmesg_restrict = 1

# Restrict unprivileged access to the kernel performance subsystem (perf) to block side-channel attacks
kernel.perf_event_paranoid = 3

# Disable SysRq magic key combinations to prevent physical access memory dumps or forced reboots
kernel.sysrq = 0

# Harden ptrace restrictions to protect active processes against unauthorized memory tracing
kernel.yama.ptrace_scope = 2

# Disable unprivileged eBPF execution and enforce JIT hardening (blinding) against modern BPF exploits
kernel.unprivileged_bpf_disabled = 1
net.core.bpf_jit_harden = 2
```

Save the configuration in `nano` via **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit.

**3.** Terminate the root superuser session and return to standard user privilege level:
```bash
exit
```

**4.** Because remote desktop management is unused, disable the service entirely:
```bash
sudo systemctl disable --now gnome-remote-desktop.service
```

**5.** Disable services managing cellular modems and mobile broadband networks:
```bash
sudo systemctl disable --now ModemManager.service
```

#### Low-Level sysctl Hardening: Defense Against TCP Timestamp Fingerprinting:

Even with a strict UFW firewall active and OS signatures suppressed, the Linux kernel leaks its identity at the network layer through TCP packet parameters. One of the most dangerous passive deanonymization techniques is **TCP Timestamp Fingerprinting (RFC 1323)**.

When establishing a network connection (SYN packet), the Linux kernel includes a timestamp (`TSval`) in the TCP header by default. This counter increments at a fixed frequency (often based on kernel system jiffies).

By analyzing this parameter (e.g., via passive traffic sniffing or Nmap scanners), a remote server or ISP can:

* Calculate the exact **uptime** of your operating system since its last boot.
* Perform session correlation: if you switch VPNs or IP addresses but the uptime and TCP timestamp tick rate remain identical, the remote host instantly correlates the traffic to the same physical machine.
* Identify hidden devices operating behind a NAT router.

To eliminate this attack vector, force the kernel network stack to disable timestamp generation.

**1.** Open the previously created kernel security configuration file:
```bash
sudo nano /etc/sysctl.d/99-security-hardening.conf
```

**2.** Navigate to the end of the file and append the following directives:
```ini
# Disable TCP timestamps to mitigate fingerprinting and uptime tracking
net.ipv4.tcp_timestamps = 0

# Prevent replay attacks (RFC 1323) when TCP timestamps are disabled
net.ipv4.tcp_tw_reuse = 0
```

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

> [!IMPORTANT]
> **Author's Note:** Disabling `tcp_timestamps` effectively obfuscates the system by stripping its unique time fingerprint. However, on gigabit links and under extreme network load, this may theoretically reduce throughput slightly because the kernel loses access to the PAWS (Protect Against Wrapped Sequence numbers) algorithm. For a hardened, isolated host, this trade-off is fully justified and necessary.

To apply all newly added network stack and kernel parameters instantly without rebooting the system, run:

**3.** Reload all system kernel configuration files without a reboot:
```bash
sudo sysctl --system
```

> [!TIP]
> **Validation Check:** Carefully inspect the command output. At the bottom of the applied parameters list, verify that your custom `99-security-hardening.conf` file successfully loaded and overridden previous default parameters.

#### Blocking Rare Network Protocols and Legacy Filesystems:

Block the kernel from loading rare network protocols and unused legacy filesystems to completely eliminate potential attack vectors targeting vulnerabilities in their binary kernel modules:

**1.** Open the configuration file for the previously created kernel module blacklist:
```bash
sudo nano /etc/modprobe.d/blacklist-hardening.conf
```

**2.** Insert the following configuration directives:
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

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, and then press **`Ctrl + X`** to exit.

**3.** Update the initial RAM filesystem image to embed the new configuration directly into early boot stage:
```bash
sudo update-initramfs -u -k all
```

#### Filesystem Access Control Hardening:

By default, Ubuntu operating systems create files with a `UMASK 022` permission mask. This allows other unprivileged local users (and potentially compromised background system daemons) to freely read newly created files. Change this global policy to the most restrictive profile:

**1.** Open the global user account parameters configuration file:
```bash
sudo nano /etc/login.defs
```

Locate `UMASK 022` and `USERGROUPS_ENAB yes` inside the file and forcibly update their values to `UMASK 077` and `USERGROUPS_ENAB no`. If the `UMASK 022` directive is missing, append `UMASK 077` to the end of the file.

To save changes in `nano`, press **`Ctrl + O`** -> **`Enter`**, and then press **`Ctrl + X`** to exit.

This guarantees that any new files or directories generated by applications or users will default exclusively to owner-only access (`600` permissions for files and `700` for directories).

Now, lock down access to the current home directory against unauthorized local inspection:

**2.** Enforce strict permissions on the personal user home directory:
```bash
chmod 0700 /home/$USER
```

**3.** Restrict access permissions on custom `sudoers` rule directories:
```bash
sudo chmod 750 /etc/sudoers.d && sudo chmod 640 /etc/sudoers.d/* 2>/dev/null || true
```

#### Securely Mounting Shared Memory:

Configure secure mounting parameters for virtual shared memory (`shared memory`), a vector frequently leveraged by attackers for covert fileless malware execution:

**1.** Open the host filesystem table:
```bash
sudo nano /etc/fstab
```

> [!WARNING]
> Applying the `noexec` mount option to the `/dev/shm` shared memory partition is a classic recommendation to mitigate malware execution directly from RAM. However, in modern Linux distributions, this memory sector is critical for web browsers (Firefox, Chromium), which rely on it for process IPC interaction and rapid interface rendering.
> 
> Enforcing the `noexec` flag on `/dev/shm` triggers an immediate crash in Chromium-based browsers (*«Aw, Snap!»*) at launch. While Firefox will start and handle basic web browsing, its internal tab isolation sandboxes fall back to a degraded mode. Complex web content—hardware-accelerated streaming video, WebAssembly (WASM), or WebGL graphics—will cause open tabs to crash.
> 
> Avoid resolving this issue by downgrading the desktop to the legacy **Xorg (X11)** display server. Although Xorg tolerates the `noexec` flag, its 1980s architecture completely lacks window isolation. Any unprivileged application running under Xorg can log keystrokes across other windows, capture screenshots, and synthesize input events, neutralizing host security controls.

If the target system requires full capability for media playback and local LLM execution, deploy **Option 2A** using `rw,nosuid,nodev` flags. Code execution security should be enforced higher up the stack via native AppArmor profiles, container isolation, and strict application execution policies.

Navigate to the bottom of the file and append one of the following configuration options based on system role.

**Balanced Profile (Recommended for Daily Desktop Use):**

**2A.** Preserves complete operational stability for modern web browsers during video streaming and WebAssembly processing without breaking internal IPC communication mechanisms. The host remains protected against block device node creation and privilege escalation via setuid/setgid bits:
```ini
tmpfs /dev/shm tmpfs rw,nosuid,nodev 0 0
```

**Paranoid Profile (Maximum Isolation):**

**2B.** Suited for CLI servers and dedicated desktop systems running defined workloads (terminal applications, text editors, local administration, Docker/VMware environments) where rendering dynamic web content is not required. The `noexec` flag blocks third-party binary execution from RAM, mitigating *Fileless Malware* attack vectors:
```ini
tmpfs /dev/shm tmpfs defaults,noexec,nosuid,nodev 0 0
```

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

> [!NOTE]
> Unlike Chromium-engine browsers that crash instantly on launch under `noexec`, Firefox will launch and render simple websites. Issues manifest when rendering complex content: tabs crash when initializing WebAssembly (WASM) or WebGL graphics, and internal sandbox isolation operates in a degraded, less secure state.

#### Configuring Wi-Fi to Default Off on Boot:

To guarantee that wireless modules do not emit hidden over-the-air network probes during system boot, block them at the system daemon level. This completely eliminates probe request leaks and prevents accidental deanonymization of the factory MAC address in public spaces:

**1.** Open the unit configuration file in a text editor:
```bash
sudo nano /etc/systemd/system/rfkill-block-early.service
```

**2.** Insert the following blocking directives:
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

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit.

**3.** Create a unit file to enforce alignment with NetworkManager policies:
```bash
sudo nano /etc/systemd/system/wifi-off.service
```

**4.** Insert the following service directives:
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

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

**5.** Reload systemd manager configuration:
```bash
sudo systemctl daemon-reload
```

**6.** Enable the early boot RfKill block and Wi-Fi suppression services:
```bash
sudo systemctl enable rfkill-block-early.service && sudo systemctl enable wifi-off.service
```

**7.** Reboot the host system:
```bash
sudo systemctl reboot -i
```

The system preserves this state within kernel parameters, ensuring radio transmitters remain disabled via RFkill by default on subsequent boots.

> [!WARNING]
> This deployment sequence covers 99.9% of practical threat scenarios, leaving an imperceptible exposure window that cannot be exploited by standard software.
> The sole mitigation yielding zero risk of RF exfiltration requires cutting power to the wireless controller entirely. Achieve this via BIOS/UEFI firmware toggles (Hardware Disable) or physical kill switches found on legacy laptops. Standard keyboard hotkeys such as Fn+F2, Fn+F5, or Fn+F8 (featuring antenna or airplane icons) act strictly as software triggers. Activating them emits an ACPI event caught by the OS kernel (observable via `sudo journalctl -f`), which then instructs software to mute the transmitter. However, if the host is compromised by rootkits, these software restrictions can be bypassed regardless of physical key state.

#### Cutting Off Video Streams and Audio Recording:

While a physical camera slider or tape over the lens prevents visual espionage, the microphone can still capture ambient audio in the background.

**1.** Open the configuration file:
```bash
sudo nano /etc/modprobe.d/blacklist-hardening.conf
```

**2.** Enforce absolute isolation over the kernel multimedia stack, blocking camera drivers (UVC) and Intel sound subsystems:
```ini
blacklist uvcvideo
install uvcvideo /bin/true
blacklist snd_hda_intel
blacklist snd_hda_codec_realtek
install snd_hda_intel /bin/true
install snd_hda_codec_realtek /bin/true
```
To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

**3.** Apply changes by embedding the updated configuration into the initial boot stage:
```bash
sudo update-initramfs -u -k all
```

> [!NOTE]
> The `uvcvideo` module manages integrated webcams, while `snd_hda_intel` and `snd_hda_codec_realtek` handle sound card and microphone initialization. The host is now operating as a fully air-gapped audio-visual terminal. Covert eavesdropping on room ambient audio or capturing video streams from within the OS is rendered impossible.

**4.** If speakers and microphones are required for voice recording, audio processing, or media playback, adjust the configuration file as follows. Keep the camera strictly blocked, while commenting out the audio chip directives using a hash `#` symbol (followed by a space) so the Linux kernel ignores them and leaves the audio hardware active:
```ini
blacklist uvcvideo
install uvcvideo /bin/true
# blacklist snd_hda_intel
# blacklist snd_hda_codec_realtek
# install snd_hda_intel /bin/true
# install snd_hda_codec_realtek /bin/true
```
To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the console shell.

**5.** Rebuild the initial RAM filesystem image to finalize the security perimeter:
```bash
sudo update-initramfs -u -k all
```

> [!IMPORTANT]
> Microphones should not remain active continuously. To toggle input rapidly, most laptops provide a hardware hotkey combination (typically Fn+F4 displaying a crossed-out microphone icon). If the target device lacks a dedicated key, utilize native operating system controls. Navigate to system **«Settings»**, select the **«Sound»** tab, and inside the **«Input»** section, click the microphone icon next to the **«Input Volume»** slider to instantly mute input (*Mute* tooltip). Clicking it again toggles the device back to active status (*Unmute* tooltip).

#### Removing Printing Services and Local Network Discovery Services:

Next, forcibly disable the `avahi-daemon` service. This background daemon manages automatic local network resource discovery via the mDNS protocol, broadcasting your host's hostname in the `hostname.local` format. Furthermore, the utility maintains open network ports 5353 (UDP) and 32768 (TCP). Active open ports in public local networks allow adversaries to rapidly identify and target your device, which is entirely unacceptable:

**1.** Purge the Avahi service from the system completely, wiping residual configuration files:
```bash
sudo apt purge avahi-daemon -y && sudo apt autoremove -y
```

Next, disable and uninstall the `cups` service, which manages background network printer discovery and print queue operations. Unless printer access is required on the host, this subsystem must be eliminated completely:

**2.** Terminate and disable the network printer scanning service immediately:
```bash
sudo systemctl disable --now cups-browsed
```

**3.** Purge CUPS daemons and printing packages completely without cascading package upgrades:
```bash
sudo apt purge cups cups-daemon cups-browsed hplip hplip-data -y
```

**4.** Clean up remaining orphaned package dependencies:
```bash
sudo apt autoremove --purge -y
```

**5.** Enforce a hard quarantine over the printing subsystem at the GNOME desktop shell level (Desktop Lockdown). This prevents the desktop environment from spawning background device discovery threads, frees host RAM from phantom notification daemons, and permanently blocks multicast probe requests targeting the router (`239.255.255.250:3702`):
```bash
gsettings set org.gnome.desktop.lockdown disable-printing true
```

**6.** Disable multicast support at the physical network interface layer on the host card. This cuts off system IGMP multicast traffic sent by the OS kernel to `224.0.0.22` (replace `enp0s1` with your actual Netplan interface name):
```bash
sudo ip link set dev enp0s1 multicast off
```

#### Masking Geolocation and Timezone:

Completely purge the `Geoclue` geolocation service from the operating system to prevent covert background tracking of host physical coordinates:

**1.** Terminate and mask the geolocation service immediately, completely blocking its invocation via the system D-Bus:
```bash
sudo systemctl stop geoclue.service && sudo systemctl mask geoclue.service
```

Finally, force the system clock to a neutral timezone to scrub the operating system's regional digital fingerprint:

**2.** Set the system timezone to Coordinated Universal Time:
```bash
sudo timedatectl set-timezone UTC
```

Verify that the new timezone parameters were applied successfully:

**3.** Display current system time status:
```bash
timedatectl
```
The output string `Time zone:` must explicitly show: `UTC (UTC, +0000)`.

<br>

## Configuring Repositories and System Updates

Starting with version 24.04, `/etc/apt/sources.list` has fully migrated to `/etc/apt/sources.list.d/ubuntu.sources`. In Ubuntu 26.04, the «Software & Updates» GUI is absent, requiring command-line verification instead.

**1.** Open the system repository configuration file in `nano`:
```bash
sudo nano /etc/apt/sources.list.d/ubuntu.sources
```

**2.** Edit the configuration to remove `multiverse` and `restricted`:
```ini
Types: deb
URIs: http://archive.ubuntu.com/ubuntu/
Suites: resolute resolute-updates resolute-backports
Components: main universe
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: http://security.ubuntu.com/ubuntu/
Suites: resolute-security
Components: main universe
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

For Ubuntu 24.04, using the GUI is still an option. Configure repositories via the graphical interface as follows:

Navigate to **«Show Applications»**, launch **«Software & Updates»**, and under the **«Ubuntu Software»** tab (*Downloadable from the Internet*), uncheck **«Software restricted by copyright or legal issues (multiverse)»**. If running hardware without proprietary Nvidia or AMD graphics cards, uncheck **«Proprietary drivers for devices (restricted)»** as well. From a security standpoint, these repositories are closed-source, leaving their binary contents non-auditable and vendor-opaque.

To significantly boost host privacy, set **«Download from:»** to **«Main server»**. This eliminates potential geographic location leaks caused by update queries hitting local mirrors and protects against ISP-level traffic analysis.

Click **«Close»**, then click **«Reload»** in the prompt to refresh the local package cache. This completes the baseline GUI security hardening sequence.

**Chapter Assets:** *_assets/images/6_software_updater*

<br>

#### Updating the System:

With initial operating system hardening complete, perform a full system update. Connect to the physical network by attaching an Ethernet cable or enabling the Wi-Fi adapter (though abandoning wireless networks in favor of traditional wired connections is strongly recommended wherever technically feasible).

> [!WARNING]
> **If using a VPN!** Because a strict Kill Switch was configured in UFW during the previous chapter, internet access will remain blocked immediately after connecting via cable or Wi-Fi. You must manually establish your encrypted VPN tunnel; otherwise, the firewall will drop all outbound packets.
> 
> Bring up the tunnel using one of two methods:
> 
> * **Graphical Method (Recommended):** Click the system status menu in the top-right corner of the screen (the GNOME panel housing battery, audio, and network icons). From the drop-down menu, select **«Wired»** to connect to the local network, then select **«VPN»** and click to connect.
> * **Terminal Method (Fallback if GUI fails):** Open a terminal shell and forcibly initiate the tunnel directly via OpenVPN:
> ```bash
> sudo openvpn --config /path_to_file/profile.ovpn
> ```

**1.** Refresh local repository indexes, then download and apply the latest security patches and core system updates:
```bash
sudo apt update && sudo apt upgrade --with-new-pkgs -y
```

> [!NOTE]
> Output showing `Summary: Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: N` (where N is a number of held packages, e.g., 5).
> 
> Running `apt list --upgradable` will likely display: `Not upgrading yet due to phasing`. This indicates phased rollout delivery, a standard Ubuntu deployment mechanism rather than a package manager failure. **For testing environments**, force immediate installation using:
> 
> ```bash
> sudo apt -o APT::Get::Always-Include-Phased-Updates=true full-upgrade
> ```

**2.** Purge obsolete packages, remove orphaned dependencies, and clear downloaded package caches to reclaim storage space:
```bash
sudo apt autoremove --purge -y && sudo apt clean
```

**3.** Reboot the host to finalize kernel updates and restart background system services:
```bash
sudo systemctl reboot -i
```

#### Deploying the NVIDIA Graphics Stack in Isolated Mode:

This subsection is required strictly under two scenarios: when deploying a local AI environment for neural network workloads (LM Studio) or when hardware-accelerated heavy graphics rendering is critical. If building a system dedicated solely to text-based OPSEC (confidential email, secure messaging, basic web browsing), skip this step entirely.

If GPU hardware performance is required, execute a temporary gateway strategy: activate the repository, pull the necessary components, freeze their versions at the kernel layer, and remove the repository branch from the system completely. This yields full graphics stack performance while restoring the operating system to a state of complete "package silence."

**1.** Temporarily activate the official proprietary `restricted` repository component and update package indexes:
```bash
sudo add-apt-repository restricted -y && sudo apt update
```

**2.** Launch the driver auto-installation utility to pull the latest stable branch targeting your kernel:
```bash
sudo ubuntu-drivers install
```

If Ubuntu 24.04 returns a message stating `All the available drivers are already installed.`, launch **«Software & Updates»** and navigate to the **«Additional Drivers»** tab. Select the current active driver, for example, *Using NVIDIA driver metapackage from nvidia-driver-580 (proprietary)*. Click **«Apply Changes»**, then select **«Restart...»** once installation completes.

During reboot in Ubuntu 24.04, verify settings on the user password login screen: click the gear icon in the lower-right corner to check session status. If set to Ubuntu on Xorg rather than Wayland, switch it back to the secure Wayland session before logging in.

**3.** Freeze current versions of all installed NVIDIA packages on the system. This prevents the `apt` package manager from modifying them, eliminating display session breakage after repository removal:
```bash
dpkg -l | grep nvidia | cut -d' ' -f3 | xargs -r sudo apt-mark hold
```

**4.** Remove the `restricted` repository branch from the system:
```bash
sudo add-apt-repository --remove restricted -y && sudo apt update
```

To update drivers in the future, replace `hold` with `unhold` and re-enable the `restricted` repository.

> [!NOTE]
> Applying `apt-mark hold` locks the driver stack in its current stable state. Scheduled distribution updates will no longer touch or break the display driver stack, while completely removing the `restricted` repository ensures the system ceases all connection attempts to third-party proprietary mirrors.

**5.** Reboot the host machine to initialize locked driver modules at the Linux kernel level:
```bash
sudo systemctl reboot -i
```

> [!IMPORTANT]
> **Ubuntu 24.04 Only**. The Wayland display server enforces window isolation at the display server layer, blocking malware from logging keystrokes or snooping on the system clipboard. However, the Ubuntu display manager (`gdm3`) contains an automated fallback trigger that silently downgrades the session to legacy X11 (Xorg) upon detecting potential instability with modern NVIDIA drivers or the Ubuntu 24.04 kernel.
> 
> If the session falls back to X11 following a reboot during verification, execute the following recovery procedure using GRUB configuration overrides and udev rules masking.
> 
> **Without enabling internet access**, open a host terminal shell immediately following reboot and audit the active display session:
> ```bash
> echo $XDG_SESSION_TYPE
> ```
> * If the output returns `wayland`, the security perimeter remains intact; proceed with the chapter.
> * If the output returns `x11`, the display server was downgraded. Do not proceed until the Wayland session is forcibly restored.
>
> **Forced Wayland Restoration Procedure for NVIDIA GPUs on Ubuntu 24.04:**
> 
> **1.** Open the bootloader configuration file in a text editor:
> ```bash
> sudo nano /etc/default/grub
> ```
> **2.** Locate the line `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` and append the kernel KMS mode setting flag `nvidia-drm.modeset=1` inside the quotes:
> ```ini
> GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvidia-drm.modeset=1"
> ```
> Save the file in `nano` via **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the terminal.
> 
> **3.** Write configuration changes to the host boot sector:
> ```bash
> sudo update-grub
> ```
> **4.** Neutralize Ubuntu's system udev rule that forcibly disables Wayland when proprietary drivers are detected by overriding it with an empty symlink target:
> ```bash
> sudo ln -sf /dev/null /etc/udev/rules.d/61-gdm.rules
> ```
> **5.** Reboot the host machine to enforce parameters:
> ```bash
> sudo reboot
> ```

**Chapter Assets:** *_assets/images/6_software_updater*

## Terminal Environments in Ubuntu:

#### Replacing GNOME Terminal and Ptyxis with Ghostty

Installing the highly discussed Ghostty terminal emulator, written in Zig and created by well-known IT figure Mitchell Hashimoto.

**Installation for Ubuntu 24.04 LTS (Noble Numbat) users:**

**1.** Perform a dry-run purge to verify dependency removal and ensure critical packages are not inadvertently removed:
```bash
apt -s purge gnome-terminal
```

**2.** Install Ghostty:
```bash
sudo add-apt-repository ppa:maksberg/ghostty-ubuntu && sudo apt update && sudo apt install ghostty
```

**3.** Purge GNOME Terminal:
```bash
sudo apt purge gnome-terminal
```

**4.** Perform a dry-run autoremove to inspect orphan packages targeted for cleanup:
```bash
apt -s autoremove
```

If no essential system packages are targeted, proceed with final cleanup.

**5.** Purge lingering GNOME Terminal dependencies:
```bash
sudo apt autoremove
```

**Installation for Ubuntu 26.04 LTS (Resolute Raccoon) users:**

**1.** Perform a dry-run purge to verify dependency removal and ensure critical packages are not inadvertently removed:
```bash
apt -s purge ptyxis
```

The package manager will likely target `apport-gtk*` and `ptyxis*` for removal, which is expected. The `apport-gtk*` utility manages crash report popups and telemetry submission in Ubuntu; removing it prevents crash diagnostic prompts from launching.

**2.** Install Ghostty:
```bash
sudo apt update && sudo apt install ghostty
```

Execute all remaining tasks directly from within the Ghostty terminal emulator window.

**3.** Purge Ptyxis:
```bash
sudo apt purge ptyxis
```

**4.** Perform a dry-run autoremove to inspect orphan packages targeted for cleanup:
```bash
apt -s autoremove
```

If no essential system packages are targeted, proceed with final cleanup.

**5.** Purge lingering Ptyxis dependencies:
```bash
sudo apt autoremove
```

**Ghostty Configuration Options for Ubuntu 24.04 / 26.04:**

Access configuration settings in Ghostty by opening the **burger menu** and selecting **Open Configuration**. Populate the resulting `config.ghostty` file with the following directives:

```ini
# Font family and size
font-family = "Ubuntu Mono Semi-Bold"
font-size = 16

# Foreground text color (hacker green)
foreground = #00ff00

# Window background color (deep dark blue)
background = #0a1128

# Window opacity (0.0 fully transparent, 1.0 fully opaque)
background-opacity = 0.95

# Background blur radius (0 disables blur)
background-blur-radius = 20

# Initial window dimensions in character columns and rows
window-width = 96
window-height = 24
```

#### Optional! Ubuntu 26.04 — Restoring Gnome Terminal and Removing Ptyxis:

To reiterate, **this approach is not recommended** as it introduces inherent security risks and serves purely as an alternative fallback. Executing untrusted or malicious code within this setup carries a near-100% probability of compromising the entire host system. Using a strict `firejail` sandbox is strongly recommended for such workflows instead.

**1.** Perform a dry-run purge to verify dependency removal and ensure critical system packages are not inadvertently targeted:
```bash
apt -s purge ptyxis
```

The package manager will likely target `apport-gtk*` and `ptyxis*` for removal, which is expected. The `apport-gtk*` utility manages crash reporting popups and telemetry submission in Ubuntu; removing it prevents crash diagnostic prompts from launching.

**2.** Install GNOME Terminal:
```bash
sudo apt install gnome-terminal
```

Execute all subsequent commands directly from within the newly installed GNOME Terminal window.

**3.** Purge Ptyxis:
```bash
sudo apt purge ptyxis
```

**4.** Perform a dry-run autoremove to inspect orphan packages targeted for cleanup:
```bash
apt -s autoremove
```

If no essential system packages are targeted, proceed with final cleanup.

**5.** Purge lingering Ptyxis dependencies:
```bash
sudo apt autoremove
```

Audit the package list before executing the final deletion command. If unknown system components appear in the removal queue, abort the process; otherwise, execute the removal command in the terminal shell: `sudo apt autoremove`.

**6.** Purge remaining Ptyxis orphan packages:
```bash
sudo apt autoremove
```

<br>

## Removing and Blocking Snap and Telemetry

#### Purging Snap:

Proceed to strip the `Snapd` subsystem from the operating system entirely, neutralizing its ability to covertly download and update proprietary packages while bypassing host privacy parameters:

**1.** Purge the `Snapd` daemon and its supporting architecture from the host:
```bash
sudo apt purge snapd -y
```

To prevent the package manager from automatically pulling the daemon back as an orphan dependency when updating third-party applications, lock its installation status via hard APT Pinning priorities:

**2.** Create a dedicated pinning configuration file:
```bash
sudo nano /etc/apt/preferences.d/nosnap.pref
```

**3.** Insert the following policy directives into the newly created file:
```ini
Package: snapd
Pin: release a=*
Pin-Priority: -10
```

To save the configuration in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the terminal shell.

> [!IMPORTANT]
> First, in recent Ubuntu releases, the stock *App Center* GUI relies entirely on the Snap backend. Purging the daemon permanently breaks the graphical store executable. This is a net security gain for a hardened host: it eliminates an unneeded attack surface while shifting software management strictly to the clean `apt` CLI package manager. If a graphical package manager is required to handle `.deb` files manually, deploy the legacy Synaptic utility via: `sudo apt install synaptic`.
> 
> Second, Canonical packages the default Firefox browser strictly as a Snap container in modern Ubuntu releases. Running `purge snapd` completely removes Firefox from the host system! To avoid losing web connectivity, ensure a native `.deb` build of Firefox is installed from the official developer repository (Mozilla PPA) prior to purging Snap. Execute this step immediately after completing initial kernel isolation and applying base system updates!

#### Ripping Out Canonical Telemetry:

It is time to execute our comprehensive automated Bash script to purge all built-in telemetry and prevent latent technical metric transmission to Canonical servers. Create this script inside the user's Downloads directory:

**1.** Navigate to the active user's Downloads directory:
```bash
cd ~/Downloads
```

**2.** Create an empty script file:
```bash
touch telemetryoff.sh
```

**3.** Open the script using the `nano` text editor:
```bash
nano telemetryoff.sh
```

> [!WARNING]
> Do not copy automated script code directly from e-reader interfaces (PDF/EPUB/FB2) to avoid hidden encoding errors, replaced whitespace, or accidental insertion of invisible formatting control characters! Type the lines manually or pass them through a plain text editor. Always audit script code carefully!

**4.** Insert the following consolidated telemetry purging script into the open file inside `nano`:
```bash
#!/bin/bash
# Ubuntu 24.04/26.04 Telemetry & Pro Hardening Script (Ultimate Edition)

# Designed for Ubuntu Desktop and its flavors (Xubuntu, Lubuntu)

# Check for root privileges

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
# Mark desktop environments as manually installed so apt does not purge the desktop GUI
apt-mark manual ubuntu-desktop xubuntu-desktop lubuntu-desktop gdm3 lightdm 2>/dev/null

# Remove classic telemetry software and persistent Ubuntu Pro/ESM clients
apt purge ubuntu-report whoopsie popularity-contest ubuntu-pro-client ubuntu-advantage-tools -y

# Safely purge apport without cascading GUI removal

apt purge apport -y --allow-remove-essential 2>/dev/null || apt remove apport -y

# Clear system triggers for ESM update caches that query Canonical servers

rm -f /etc/apt/apt.conf.d/20ubuntu-pro-esm 2>/dev/null

# Automatically clean up orphaned dependencies while verifying GUI integrity
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

To save the file in `nano`, press **`Ctrl + O`** -> **`Enter`**, then press **`Ctrl + X`** to exit back to the terminal shell.

**5.** Enforce strict access permissions on the file: restrict read, write, and execution privileges exclusively to the file owner:
```bash
chmod 0700 telemetryoff.sh
```

**6.** Execute the script with superuser privileges and await successful completion of the host optimization routine. Once complete, the script can be deleted:
```bash
sudo ./telemetryoff.sh
```

**7.** Reboot the system:
```bash
sudo reboot
```

> [!TIP]
> To execute the script immediately without modifying execution bits via `chmod +x`, invoke the Bash interpreter directly:
> ```bash
> sudo bash telemetryoff.sh
> ```
> *Note: If the script file was edited under Windows, strip line endings first via `sed -i 's/\r$//' telemetryoff.sh`.*

After execution, remove `telemetryoff.sh` from `Downloads` via the trash interface or by executing `rm ~/Downloads/telemetryoff.sh`.

**8.** Purge lingering components of the kernel crash reporting and submission framework:
```bash
sudo systemctl stop apport.service  && sudo systemctl disable --now kerneloops.service
```

#### Purging the Background Firmware Tracker fwupd:

Even after completely purging Canonical system telemetry, the hidden `fwupd` (Firmware Updater) daemon remains active by default in the operating system. Upon establishing a network connection, it silently transmits background queries to the global CDN server `cdn.fwupd.org`, leaking unique hardware UUID identifiers for the motherboard, CPU, and NVMe drives under the guise of checking for BIOS/UEFI firmware updates.

Eliminate uncontrolled background exfiltration of host hardware hashes. Perform all critical low-level firmware updates strictly offline and manually, while severing the daemon's network access at the system daemon layer.

**1.** Terminate active services and background update timers:
```bash
sudo systemctl stop fwupd fwupd-refresh.service fwupd-refresh.timer
```

**2.** Forcibly mask unit configuration files in `systemd`. This permanently blocks accidental, background, or dependency-triggered service execution during package operations:
```bash
sudo systemctl mask fwupd fwupd-refresh.service fwupd-refresh.timer
```

> [!NOTE]
> Applying systemd masking unloads the background `fwupd` process from RAM and prevents it from binding network sockets. Covert connections targeting external `cdn.fwupd.org` endpoints are permanently blocked.

**Chapter Assets:** *_assets/images/7_systemcut_telemetry*

<br>

## Installing Security Utilities: libpam-tmpdir, debsums, and the Btop System Monitor

#### The libpam-tmpdir Security Utility:

To eliminate one of the oldest architectural vulnerabilities in Linux, isolate shared temporary directories accessible by default to all system processes. Integrate a specialized authentication module into the kernel to dynamically provision isolated, per-application temporary storage in memory for every active session.

**1.** Deploy the low-level application temporary directory isolation module (`libpam-tmpdir`):
```bash
sudo apt install libpam-tmpdir -y
```

> [!NOTE]
> By default, all running processes, messaging applications, system daemons, and scripts share the global system directory `/tmp` for temporary file storage. From a security perspective, this creates an unmonitored shared surface. Malicious binaries, covert trackers, or unprivileged processes executing inside the system can enumerate `/tmp` contents, spy on temporary files generated by adjacent applications, attempt file tampering, or execute symlink attacks.

#### The debsums Utility:

The `debsums` utility is built for auditing internal system integrity at a granular level. The name stands for Debian checksums.

When deploying packages via the `apt` package manager, a reference manifest containing cryptographic hash digests (typically MD5 or SHA) for every installed file is pulled alongside the binary payload. The `debsums` engine parses these reference manifests and audits them against actual files residing on the disk subsystem. If an adversary, rootkit, or rogue process covertly modifies a system binary (such as replacing `/bin/ls` or `/usr/bin/ssh` with a trojanized binary), the cryptographic hash check fails, triggering an immediate `FAILED` alert status.

**1.** Deploy the package checksum auditing utility:
```bash
sudo apt install debsums -y
```

**2.** Execute a global integrity audit across all installed system packages:
```bash
sudo debsums -s
```

#### Btop: A Streamlined Resource Monitor:

A modern terminal-based resource monitor designed to replace the standard `top` utility. The tool provides a significantly more intuitive, detailed, and interactive graphical dashboard running directly inside the terminal interface.

**1.** Deploy the utility from the official repository:
```bash
sudo apt install btop -y
```

**2.** Launch the resource monitor:
```bash
btop
```

Access the internal keybinding reference menu by pressing **H** (*Help*). Exit the application instantly by pressing **Q** (*Quit*).

<br>

#### Monitoring Network Ports and Active Connections:

Continuous monitoring of network activity is a core operational hygiene requirement. Maintain complete visibility over which internal processes bind sockets and where outbound network traffic is actively routed.

**1.** Audit open network listening ports. This command displays active background daemons and system services listening on local ports for incoming connections:
```bash
sudo ss -tupnl
```

**2.** Display the full active network session table. This command exposes all active network sockets, including established outbound connections (*ESTABLISHED*). Use it to immediately identify remote destination IP addresses processing active traffic:
```bash
sudo ss -tupna
```

While `ss` provides an instantaneous static snapshot of active sockets, sophisticated malware and covert backdoors often operate via short-lived connections—opening a socket for a fraction of a second, exfiltrating encrypted payloads, and immediately severing the pipe. Capturing these transient events manually via periodic command execution is practically impossible.

For continuous real-time socket monitoring, combine `ss` with the native system automation utility `watch`, enforcing dynamic delta highlighting via the `-d` flag:

**3.** Launch real-time continuous socket monitoring:
```bash
sudo watch -n 1 -d 'ss -tupna'
```

This pipeline automatically refreshes the terminal buffer every second (`-n 1`), while the `-d` flag visually highlights any newly spawned inbound or outbound socket transitions on the screen, enabling manual detection of transient background network activity.

To terminate the monitoring loop and return to the shell console, press **`Ctrl + Z`**.

<br>

## Creating Golden Restore Points: Deploying and Configuring Timeshift

#### Introduction:

With initial kernel hardening, privilege isolation, and strict firewall blocking fully established, the host is operating as a clean, hardened, and completely air-gapped system. Before initiating a primary network connection to apply full distribution updates, freezing this sterile state is a critical prerequisite.

Engineered security controls account for worst-case operational failure: applying major package updates, upgrading core kernel images, or building virtualized container stacks can trigger system instability or break configurations. Rather than wasting hours reinstalling the operating system from scratch and repeating manual hardening steps, construct instant system snapshots that enable bare-metal rollback in a few clicks.

Deploy the `Timeshift` system utility to manage state restoration. Operating as a restore-point system, it isolates and protects core system binaries and configurations without altering user data stored inside the home directory, preventing operational document loss during state restoration routines.

#### Timeshift Mechanics in an Encrypted Environment (LUKS + GRUB):

Because the system was deployed on top of an encrypted LVM pool and the `GRUB` bootloader was secured with a password during installation, account for two strict security rules:

1. **No External Software via Live-USB:** Configure `Timeshift` and execute snapshot rollbacks strictly from within the running, decrypted operating system. Using third-party emergency Live USB drives is unacceptable under this OPSEC model, as they bypass established host authorization mechanisms.
2. **Boot Sector Integrity Control:** The encrypted disk layout and password-protected `GRUB` bootloader remain fully secured because `Timeshift` snapshots operate on file states inside logical volumes without modifying the underlying low-level LUKS encryption structure. However, restoring a snapshot can overwrite `GRUB` menu configuration files; the kernel editing password remains active and will not be reset.

#### Securely Installing Timeshift:

Execute the sequence of commands in the terminal with superuser privileges. Bring up the encrypted tunnel, then initiate installation from the official Ubuntu repository:

**1.** Switch to interactive superuser mode (root):
```bash
sudo -i
```

**2.** Refresh the local package index and install the native .deb version of Timeshift directly over the secure connection:
```bash
apt update && apt install timeshift -y
```

**3.** Exit superuser mode and return to the standard user session:
```bash
exit
```

The utility is now successfully deployed on the host, while the protective network perimeter remained continuously enforced without exposure to external traffic.

#### Initial Configuration and Creating Snapshot #1 (Sterile Baseline):

Executing `Timeshift` requires superuser privileges.

**1.** Launch the application:
```bash
sudo timeshift-gtk
```

You can launch the graphical interface via the **«Show Apps»** application menu (the system will prompt for administrative credentials); however, if you subsequently transition to Yubikey authentication, this option must be abandoned in favor of the CLI method.

Upon initial startup, the Setup Wizard will open. Immediately click **«Finish»** without making changes.

Navigate to the **«Settings»** menu item and configure the following parameters:

* **Snapshot Type («Type»):** Select **«RSYNC»** mode exclusively. Since standard file systems run over LVM encryption, this mode creates reliable snapshots using system hard links without consuming redundant storage space for unmodified files.
* **Storage Location («Location»):** The system automatically highlights the active encrypted LVM partition (e.g., dm-1 or dm-0 associated with the root volume group name). Select it. Snapshots are stored on this partition within an isolated system directory at `/timeshift`, restricted to root permissions.
* **Snapshot Schedule («Schedule»):** Uncheck all automated backup triggers **(Daily, Boot, Weekly, Monthly)**. Under this operational hygiene model, background daemons must not execute unprompted disk I/O operations, generate hidden CPU overhead, or degrade drive endurance. Execute all snapshots manually under full operator control.
* **User Directories («Users»):** This tab dictates home directory behavior during system rollback routines. By default, the standard user entry (`user /home/user`) is set to **«Exclude All Files»**—set this parameter to **«Include All Files»** for the initial snapshot. For subsequent snapshots, optionally set it to **«Exclude All Files»** to prevent the utility from overwriting personal databases and credential stores. Enforce setting the root directory entry (`root /root`) to **«Include All Files»**.
* **Directory Filters («Filters»):** Switch to the adjacent tab. Having enabled the administrative directory in the previous step, verify that the global filter entry `/root/**` is highlighted with a green marker (Include). If a duplicate exclusion rule marked with a red symbol persists, select it with the cursor and click the **«Remove»** button at the bottom of the window. The administrative home directory must be backed up and restored alongside the OS kernel. The `home/$USER/**` directory can be included at operator discretion.
* **Miscellaneous («Misc»):** Set the preferred date and time display format.
* Click **«OK»** to save settings and complete initial binding.

Click the **«Create»** button in the main interface window. The application initiates a scanning process and generates the initial baseline snapshot. In the snapshot comment field *Comments (click to edit)*, input the identifier string: `BUILD_01_STERILE_HARDENING`.

> [!WARNING]
> Within **«Settings»**, pay close attention to the **«root /root»** line item. By default, this directory is set to exclusion mode. Under this threat model, that behavior represents an operational flaw: following host compromise, malicious scripts or persistent backdoors placed in the administrator's directory would survive a system rollback. 
> Force the radio button for **«root /root»** to the far right position—**«Include All Files»**.

> [!IMPORTANT]
> This snapshot serves as the primary system recovery baseline ("Sterile Reference"). It captures all low-level kernel hardening configurations, optimized `sysctl` parameters, the enforced `UMASK 077` file creation mask, and the complete removal of native Canonical telemetry—prior to deploying user applications, third-party software repositories, web browsers, or user utilities. If subsequent customization or software testing introduces system instability, restore this hardened baseline configuration instantly.

#### Ongoing Control Strategy: Creating Snapshot #2 (Pre-Operational):

Now that the baseline system security is backed up by the initial snapshot, proceed with daily operational maintenance: apply routine system updates via `apt upgrade`, strip residual telemetry meta-packages, and deploy the native `.deb` build of the Firefox browser.

However, prior to advancing to comprehensive host auditing via `Lynis` or deploying isolated sandbox environments and lightweight Xubuntu/Lubuntu virtual containers inside VirtualBox, creating **Snapshot #2** is a mandatory prerequisite.

The procedure remains identical: prior to executing complex virtualization engines or deep auditing tools, launch `Timeshift` and manually provision a secondary recovery baseline. Assign the following comment string: `BUILD_02_BEFORE_LYNIS`.

#### Emergency Rollback Protocol (System Compromised or Broken):

If operational stability is degraded during isolated container experimentation or through syntax errors introduced into low-level configuration files, execute a safe rollback from within the active operating system environment:

* Launch the graphical Timeshift interface via the application menu (**«Show Apps»**).
* Select the target recovery snapshot from the list (e.g., the baseline `BUILD_01_STERILE_HARDENING`).
* Click the **«Restore»** button.
* In the **«Target Devices»** selection menu, confirm root (`/`) and boot partition (`/boot/efi`) mount paths. Retain default parameters: **«Keep on Root Device»**.
* Click **«Next»**. The utility executes a differential analysis, generates an audit manifest of files queued for overwrite or deletion, and initiates an automated host reboot.

During the reboot sequence, Timeshift executes in an interactive text console to overwrite modified system binaries, restoring system state to the designated recovery baseline.

> [!NOTE]
> Due to underlying LUKS hardware and software encryption abstractions, the host prompts for the master disk passphrase upon reboot as expected. The GRUB bootloader remains locked via the established hashdigest; Timeshift executes strictly inside the decrypted logical volume and cannot modify, erase, or reset outer disk protection layers.

Host security is fully established. Proceed to the next phase of operational hygiene controls!

**Chapter Assets:** *_assets/images/8_timeshift*

<br>

## Installing a Clean .deb Release of Firefox and Removing the Snap Stub:

Because the system was successfully updated over a secure VPN tunnel in the previous step, return the primary work tool to the host—the Firefox web browser. Purging the Snapd subsystem removed the default browser build while leaving residual configuration artifacts behind. The `firefox` package inside standard Ubuntu repositories functions strictly as a dummy transition package (a wrapper script) designed to re-install telemetry and force the Snapd daemon back onto the system.

Prior to deploying a native, un-isolated browser build directly from the upstream Mozilla Team developers, purge all residual metadata from the home directory and enforce strict APT pin-priority overrides.

Execute the following commands in sequence from a standard user shell session:

**1.** Purge residual directories, caches, and legacy profiles left behind by the Snap package build inside the home folder:
```bash
rm -rf ~/snap/firefox ~/.mozilla/firefox
```

**2.** Import the official Mozilla Team PPA repository into the host package manager:
```bash
sudo add-apt-repository ppa:mozillateam/ppa -y
```

**3.** The default `firefox` package in Ubuntu repositories serves as a Snap stub. To bypass this restriction and force the package manager to fetch native binaries directly from the Mozilla Team PPA, enforce a strict pin-priority configuration file:
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

To save the configuration in the `nano` editor, press **`Ctrl + O`** -> **`Enter`**, and then **`Ctrl + X`** to exit.

**4.** Refresh the local package index to apply the newly configured package pinning rules:
```bash
sudo apt update
```

**5.** Install the native, Snap-decoupled desktop build of Firefox:
```bash
sudo apt install firefox -y
```

> [!IMPORTANT]
> The following configuration step is split into two options depending on the operating system version: **Ubuntu 24.04 LTS Noble Numbat** or **Ubuntu 26.04 LTS Resolute Raccoon**. Select and execute only the single command matching the installed distribution.

**6.** Enable the system rule allowing the background unattended-upgrades service to fetch critical security patches for Firefox directly from the Mozilla Team repository:

* **For Ubuntu 24.04 LTS Noble Numbat users:**
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:noble";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

* **For Ubuntu 26.04 LTS Resolute Raccoon users:**
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:resolute";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox
```

> [!WARNING]
> Without configuring automatic origin permissions, the browser will update exclusively during manual `apt upgrade` execution, increasing exposure window risks against zero-day vulnerabilities.

**7.** Perform a final audit. If the command outputs the version string without referencing Snap, deployment was executed successfully:
```bash
firefox --version
```

> [!IMPORTANT]
> Deploying the browser via the official Mozilla Team PPA provides two critical operational advantages:
>
> **Full Compatibility with External Sandboxes:** The browser binary resides at the standard path `/usr/bin/firefox`. This allows constraint mapping under mandatory access control mechanisms via `AppArmor` and execution containment inside `Firejail` sandboxes without conflicting with Canonical's isolated Snap backend.
> **Zero Installer Telemetry:** The build is compiled directly from upstream Mozilla open-source repositories, containing no Canonical transition wrappers or background telemetry submission daemons.

<br>

## Installing and Hardening Privacy Settings in Mozilla Firefox

#### Preparing the System for Tuning:

The native web browser built into the operating system requires rigorous hardening. Deployed exclusively as a clean `.deb` package, disable hidden internal Mozilla telemetry by force, block cross-site tracking, and completely neutralize host deanonymization vectors.

> [!WARNING]
> **Initial browser launch and all configuration steps must occur strictly under complete radio silence—WITHOUT internet connectivity!**
> To avoid a critical OPSEX failure, clicking the Firefox launcher while the host is online is strictly prohibited. On its initial unconfigured startup, an untamed Firefox instance immediately transmits primary telemetry packets over the wire, checks the host IP region, and contacts Mozilla infrastructure. To prevent data leakage, isolate the operating system prior to execution.

Isolating the host can be accomplished easily using one of the following methods:

* **Graphical Method (Simplest):** Click the network connection icon in the system tray and toggle the Ethernet or Wi-Fi interface to **«Off»**.
* **Console Method (CLI):** Completely sever the operational system network stack using a single universal command:
```bash
nmcli networking off
```

With the host isolated inside a clean environment, safely launch Firefox and proceed with step-by-step hardening controls.

> [!TIP]
> Within this framework, "OPSEX" is an intentional tongue-in-cheek term crafted by the author.
> It describes an operational security failure where complex security controls are rendered useless by a simple human mistake.
>
> For example, an operator might configure a hardened environment but inadvertently breach isolation by launching an unhardened browser or transmitting a file containing embedded metadata.
>
> OPSEX serves as a reminder that system security relies on daily operational discipline alongside technical controls.
> Evaluate user workflow habits alongside defensive tooling when securing operational data.
>
> *The term OPSEX was originally formulated by the author of this guide (EugeXo) during risk analysis of personal data exposure vectors caused by user negligence and low digital literacy.*

#### Initial GUI Privacy Configuration (Mandatory for Everyone):

Launch the browser. Input the direct path into the address bar: `about:preferences#privacy`. Enforce the following configuration modifications sequentially:

* **«Enhanced Tracking Protection»** *Section:* Navigate to **«Advanced settings»**. Toggle the protection level to **«Strict»**. Click **«Reload All Tabs»**. This automatically activates Dynamic First-Party Isolation (*dFPI*), blocking advertising trackers from monitoring cross-site navigation.
* **«Browsing Data»** *Section:* Enable the checkbox for **«Clear cookies and site data every time you close Firefox»**.
* **«DNS over HTTPS»** *Section:* Modern browsers execute covert background DNS queries. Scroll down to **«Advanced settings»** to suppress this behavior. Set the provider option to **«Custom»** and manually input the URL of a trusted, no-logs DoH provider.
* **«Connection and software security»** *Section:* Scroll to the bottom of the page to find **«HTTPS-Only Mode»**. Open its advanced options and switch the toggle to **«Enable HTTPS-Only Mode in all windows»** to enforce cryptographic protection across all unencrypted HTTP requests.
* **«Search» Section:** Select this option from the left navigation sidebar. Change the default search provider from the Google telemetry engine to **DuckDuckGo**, a privacy-focused alternative.
* **«Permissions and data»** *Section:* Scroll down to **«Firefox Data Collection and Use»**. Uncheck all telemetry collection checkboxes to prevent the browser from transmitting diagnostic telemetry or stability metrics to Mozilla servers.

#### Configuring Private DNS Providers (DNS over HTTPS):

Select any secure, non-logging DoH server from the provided list.

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

To avoid entering numerous radical parameters manually via the `about:config` interface, create a single automated text file named `user.js`. All settings are added there using the system format `user_pref("parameter", value);`.

Place this file directly into the hidden folder of the currently active Firefox profile in Ubuntu. Upon each launch, the browser will automatically read this file and apply all strict parameters. In the `about:config` engineering menu, these preferences will be highlighted in bold, blocking accidental manual changes.

Find the exact path to the profile, create the `user.js` file there, populate it with content, and strictly restrict access permissions by following these steps in the terminal as a regular user:

**1.** Navigate to the profile directory (in a clean and latest `.deb` version of Firefox, the default profile almost always ends with `.default-release`) and create an empty configuration file:
```bash
cd ~/.config/mozilla/firefox/*-release/ && touch user.js
```

> [!NOTE]
> To write an automation script for different machines and ensure `user.js` is created in the currently active working profile (regardless of its name or the number of folders), use the alternative syntax with the `PROFILE_DIR` variable:
> ```bash
> PROFILE_DIR=$(awk -F= '/^\[Install/ {p=1} p && /^Default=/ {print $2; exit}' ~/.config/mozilla/firefox/profiles.ini) && cd "$HOME/.config/mozilla/firefox/$PROFILE_DIR" && touch user.js
> ```

**2.** Open the created `user.js` in the `nano` editor:
```bash
nano user.js
```

**3.** Copy and paste the following security configuration array in its entirety:
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

To save the configuration file in `nano`, press **`Ctrl + O`** → **`Enter`**, then **`Ctrl + X`** to exit back to the terminal prompt.

If an attacker, malicious script, or automatic Firefox update attempts to modify `user.js` to restore WebRTC or re-enable telemetry, defend the file by configuring read-only permissions at the Linux kernel level immediately after population:

**4.** Set read-only permissions for the file owner within the profile directory:
```bash
chmod 0400 user.js
```

This revokes write privileges to the configuration file for all processes. Even if settings are altered in the graphical user interface, the underlying Gecko engine will re-read the locked `user.js` file upon restart and re-apply these custom parameters.

> [!NOTE]
> To delete `user.js` in the future to reset settings, restore write permissions prior to removal:
> ```bash
> chmod 600 ~/.config/mozilla/firefox/*-release/user.js && rm ~/.config/mozilla/firefox/*-release/user.js
> ```

These hardened Firefox settings ensure personal data is not exposed across the network. Without these modifications, default browser configurations continuously capture user activity and collect telemetry.

**5.** Once telemetry modules, trackers, and structural vulnerabilities are neutralized in the browser core, terminate the application and reconnect the host machine. Re-enable the network toggle in the system tray or execute the following command (replacing `enp0s1` with the active interface name):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

The browser configuration is now fully hardened, anonymized, and encrypted. With strict OpSec maintained, proceed to online tasks and extension deployment.

> [!IMPORTANT]
> If testing resources (Browserleaks/CreepJS) present a static font fingerprint hash after applying these `about:config` parameters, this confirms the protection model is working correctly. Restricting font visibility to level `1` hides local host fonts and forces the browser to expose a fixed base web package. Because input metrics become static, the calculated site hash freezes, preventing anti-fraud systems from tracking unique host characteristics.
> 
> Avoid completely disabling document fonts via `browser.display.use_document_fonts = 0`. That directive blocks CSS fonts entirely, disrupting modern interface rendering and replacing web icon fonts with missing glyph boxes. Furthermore, completely blocking document fonts marks the profile as an anomaly to anti-fraud engines. Setting `layout.css.font-visibility = 1` maintains site usability while isolating local host fonts from signature scanners.
> 
> During privacy audits, the system font hash remains static while the Canvas Fingerprint shifts upon page refresh. This is the expected operation of Firefox's `privacy.resistFingerprinting` module. The Gecko engine applies a dual strategy: it standardizes font visibility while introducing cryptographic pixel noise into Canvas rendering pipelines on the fly. This noise is generated natively within the browser source code, rendering network activity mathematically indistinguishable from users of dedicated anonymity platforms (such as Tor Browser).
> 
> **Firefox configuration keys may change across versions; parameters validated in current releases may require updates in future releases.**

#### Deploying Ultimate Security Extensions:

Since the `privacy.resistFingerprinting` (RFP) parameter we previously enabled flawlessly spoofs and mitigates all key fingerprints at the Gecko engine source-code level, we only need to integrate two fundamental extensions from the official Mozilla Add-ons store:

* **uBlock Origin** (by Raymond Hill) — `https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/`. The industry's top blocker for advertisements, covert miner scripts, tracking domain beacons, and malicious phishing sites. It features superior performance and minimal memory consumption.
* **NoScript Security Suite** (by Giorgio Maone) — `https://addons.mozilla.org/en-US/firefox/addon/noscript/`. The ultimate mandatory access control system for JavaScript execution. It allows users to permit or block script execution on web pages in real time, providing total protection against browser exploits. **Must be run strictly in STRICT mode!**

> [!IMPORTANT]
> Enabling `privacy.resistFingerprinting = true` forces the browser's timezone to UTC (hiding actual physical location), constrains the browser window to standard fixed dimensions (introducing characteristic gray padding borders—*Letterboxing*—when maximized), and reports a generic default GPU to all web resources.
> 
> However, if JavaScript is fully enabled on a visited site, advanced anti-fraud scripts can still measure subtle micro-delays during interface rendering.
> 
> The **NoScript** extension eliminates this vector: if JavaScript is blocked for a given domain, the site cannot execute fingerprinting scripts. To achieve maximum anonymity, disable JS via the NoScript interface by default, enabling it temporarily and selectively only on trusted, essential web resources.
> 
> Blocking JavaScript may cause complex modern websites to render improperly or lose interactive functionality—a necessary trade-off for absolute privacy.

**Chapter Assets:** *_assets\images\9_firefox*

<br>

## Installing and Configuring the Portmaster Interactive Network Firewall

#### Introduction:

Portmaster is a powerful next-generation interactive firewall designed for deep real-time network traffic analysis. The utility packs a rich array of low-level filtering mechanics and granular security policies.

Unlike legacy solutions such as OpenSnitch, Portmaster enforces an out-of-the-box permissive "Allow" posture. It permits host binaries outbound network access by default. Traffic gets dropped only after an operator explicitly blacklists a target application or tightens the engine's global security parameters.

#### Preparation, Initial Kernel Initialization, and Upgrading:

To deploy the current version of Portmaster without cascading kernel panics, UFW conflicts, and endless CPU consumption, apply my proprietary two-stage offline upgrade tactic.

**1.** Open our configured Firefox browser. Navigate to the official developer website `https://safing.io`. Download the full offline installer for Portmaster v2 in `.deb` format (for Debian/Ubuntu systems). Once the download completes, close Firefox entirely.
```text
https://updates.safing.io/latest/linux_amd64/packages/Portmaster_2.2.1_amd64.deb \\ Direct link valid as of August 27, 2026 (release from July 17, 2026).
```

**2.** Open the host terminal. Download the official stable `.deb` installer of the legacy version from Safing update servers to deploy the initial system structures:
```bash
wget https://updates.safing.io/latest/linux_amd64/packages/portmaster-installer.deb
```

**3.** Install the downloaded package via `apt`. The package manager will automatically supply the critical low-level dependency `libnetfilter-queue1` into the Linux kernel:
```bash
sudo apt install ./portmaster-installer.deb -y
```

**4.** Upon completion of the installation, forcibly disable the operating system's network stack. This is required for secure configuration of internal sockets:
```bash
nmcli networking off
```

Launch the Portmaster graphical interface via the system menu *(**"Show Apps"**)*. On the first run, the interface will present a critical alert: **The Portmaster Core is not running**. Click **"START CORE SERVICE"** and enter the `root` superuser password in the authentication popup.

On the **Portmaster Protects Your Privacy** welcome screen, click the blue **"Quick Setup"** button. On the subsequent tracker blocking screen, **Trackers Are Blocked System-Wide**, click **"Next"**.

In the **Secure DNS For All Connections** section, locate the **Customize** dropdown menu. Select a reliable Swiss DNS provider from the built-in list (e.g., select **Set Quad9**). Collapse the dropdown menu and click **"Next"**. On the final screen, **Learn More As You Explore**, click **"Finish"**.

In the left vertical navigation bar, click the gear icon **Settings**. Navigate to the **Privacy Filter** section and locate the **Default Network Action** subsection. Change the dropdown menu setting from the default **Allow** to **Prompt**. The firewall will now block all network activity and request approval for every outgoing packet.

**5.** Briefly restore network connectivity to allow the firewall to download remaining libraries and filter lists (remember to adjust the network interface name):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

**6.** As soon as setup completes and the firewall indicator turns green, disable the network stack once again:
```bash
nmcli networking off
```

> [!IMPORTANT]
> The elegance of this scheme relies on bypassing the initialization pipeline of Safing's Go runtime. Attempting a direct "head-on" deployment of Portmaster v2 on a system with a strict UFW Kill Switch causes its engine to freeze due to an unpopulated local database cache. It continuously generates eBPF hooks, hits blocking UFW tables, enters a dead loop, and spikes CPU cores to 100% due to permanent synchronization errors.
>
> Our two-stage offline extraction bypasses this bug entirely:
>* The legacy base version (1.6.10) deploys the directory structures, configuration files, and skeleton local databases under `/opt/safing/portmaster/` in an offline state without conflicting with UFW.
>* When deploying the standalone v2 (2.2.1) package over the legacy structure, the new firewall core detects the initialized database framework. It hooks into the pre-configured baseline and operates alongside UFW in the shared network stack, consuming only 0–2% CPU resources. Both protective layers function in parallel without interference, maintaining the integrity of our Kill Switch!

**7.** While maintaining radio silence with the network disabled, open a terminal and navigate to the directory containing the full offline package:
```bash
cd ~/Downloads/
```

**8.** Install the offline Portmaster v2 build over the legacy version. The APT package manager will automatically terminate background processes, update executables, and overwrite `systemd` units without attempting outbound network connections:
```bash
sudo apt install ./Portmaster_*.deb -y
```

**9.** Reboot the host to properly initialize the updated eBPF driver within the Linux kernel:
```bash
sudo reboot now
```
> [!NOTE]
> **Important note:** Upon reaching the desktop interface on initial boot, the firewall GUI will request authorization for internal connections to the local loopback interface (`localhost 127.0.0.1`). Grant this action by clicking **Allow**.

**10.** To ensure full functionality for Firefox, temporarily remove the strict read-only lock from its configuration file to modify the DNS resolver operational mode:
```bash
chmod 600 ~/.config/mozilla/firefox/*-release/user.js
```

**11.** Open `user.js` using the `nano` terminal editor:
```bash
nano ~/.config/mozilla/firefox/*-release/user.js
```

**12.** Locate block **16. DNS PROTECTION, NAME ENCRYPTION, AND ENFORCED DoH MODE**. Change the value of the low-level parameter `network.trr.mode` from the isolated value `3` to the default **`0`**:
```javascript
user_pref("network.trr.mode", 0);
```
> [!NOTE]
> **Author's OpSec Analysis:** Setting this parameter to `0` disables Firefox's standalone DoH engine. The browser ceases sending independent encrypted requests, which Portmaster v2 flags as traffic leaks and blocks by default. Firefox then routes DNS queries through the host operating system, where they are intercepted by Portmaster eBPF hooks, evaluated against active filters, and encrypted host-wide.

To save changes in `nano`, press **`Ctrl + O`** → **`Enter`**, followed by **`Ctrl + X`** to exit the editor.

**13.** Lock the `user.js` file against unauthorized modifications by the browser, updates, or malware:
```bash
chmod 0400 ~/.config/mozilla/firefox/*-release/user.js
```

**14.** Remove the installation `.deb` packages from the local directory to prevent digital clutter:
```bash
rm ~/Downloads/Portmaster_*.deb && rm ~/portmaster-installer.deb
```

**15.** Re-enable the operating system network stack. To ensure the link connects (if "Connect automatically" is disabled in Ubuntu settings), launch NetworkManager and activate the target interface using a single command string (replacing `enp0s1` with the active interface name):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

> [!TIP]
> Trusted daily applications (such as our locked Firefox browser) can be granted persistent network permissions.
> 
> Launch Firefox. Navigate to the top GNOME system toolbar (displaying the clock, keyboard layout, and network status) and click the Portmaster icon. In the compact status menu, click **Open App**.
> 
> This opens an interactive network activity monitor displaying the active Firefox process icon in the left panel. Click the icon, navigate to the **Settings** tab, scroll to **Privacy Filter** → **Default Network Action**, and change the default value from **Prompt** to **Allow**.
> 
> Using this workflow, persistent permissions can be granted, set to "Prompt," or revoked for system services, Docker containers, and user utilities directly from the taskbar.

**Chapter Assets:** *_assets\images\10_portmaster*

<br>

## Guaranteed Data Destruction and Sterilizing Your Digital Footprint

#### Introduction:

We will dissect how the `shred` and `wipe` utilities physically overwrite bytes on a storage drive, protecting our host from forensic analysis in the event of device loss or seizure. However, engineering security does not end at the perimeter of your local disk. We must enforce an ironclad rule of operational hygiene: **every file leaving your system and transmitting across the network must be completely sterile**.

#### Anatomy of a Digital Footprint: Why Deleting Files Is Useless Without Metadata Sanitization:

Most users make a fatal mistake. They assume that creating a text document, taking a screenshot of firewall settings, or editing an image in a graphics editor results in a file containing only what is visible to the eye. This is a dangerous misconception.

Every file acts as a "Trojan horse," carrying a hidden array of service information known as **metadata** (EXIF tags for images, document properties for PDF and Office files). Publishing such a file online, transmitting it via a messenger, or uploading it to GitHub voluntarily hands trackers and potential adversaries the following data points:

* **Timestamp Markers:** Precise seconds of file creation and last modification. Analysts can leverage these to calculate your actual physical time zone and build a profile of your daily activity schedule.
* **Software Environment Footprints:** Unique program identifiers (UUIDs), as well as specific graphic or text editor versions. This enables an attacker to immediately identify software vulnerabilities suitable for profiling your system.
* **Host Identification:** Metadata frequently preserves your local system account username, computer hostname, and kernel build versions.
* **Geolocation:** Attaching a photograph taken with a smartphone or a GPS-enabled camera embeds precise geographic coordinates of the capture location down to the meter.

For OSINT specialists or adversaries, collecting metadata represents the initial and easiest step toward de-anonymization. You can construct an impenetrable fortress around Ubuntu using a Kill Switch and encrypted VPN tunnels, yet a single screenshot of "successful configurations" shared without prior sanitization immediately links your network identity to your physical profile.

> [!IMPORTANT]
> The `shred` and `wipe` mechanisms evaluated below address file **destruction** on your local storage media. However, they are entirely ineffective once a file has been transmitted to a remote server!
> 
> Prior to executing a "Send" or "Upload" action, files must undergo total sanitization. Within Linux environments, the industry standard for this task is `mat2` (Metadata Anonymisation Toolkit 2). Rather than merely stripping tags, it reassembles the underlying file structure from scratch, generating a pristine duplicate stripped of historical data.

#### Installing and Sanitizing Metadata with MAT2:

The utility is written in Python, runs completely locally, and requires no file transmission to third-party online services (which would constitute a severe security breach in itself).

**1.** Install the clean CLI version of `mat2` from the official Ubuntu repository:
```bash
sudo apt install mat2 -y
```

**2.** Prior to cleaning a file, inspect its contents to examine what hidden metadata is embedded. Command the utility to display all hidden metadata (for example, within a screenshot):
```bash
mat2 --show screenshot.png
```
The terminal will display a detailed log ranging from graphics editor versions to the exact date and timestamp of the screenshot creation.

Proceed to data sanitization. By default, `mat2` operates in a fail-safe mode: it preserves the original file and generates a sterile copy alongside it appended with the `.cleaned` suffix.

**3.** Sanitize a single document or image:
```bash
mat2 screenshot.png
```
A new file named `screenshot.cleaned.png` will be generated alongside the original. This sanitized file is safe for network transmission. If the original file is no longer required, destroy it immediately using `shred` (commands detailed below).

**4.** To sanitize an entire folder containing reports, screenshots, or logs prior to transmission, execute batch processing across all files in the designated directory:
```bash
mat2 /PATH-TO-FOLDER/*
```

**5.** For high-security requirements where original files must not persist on disk, enforce in-place overwriting using the `--inplace` flag:
```bash
mat2 --inplace screenshot.png
```

**6.** Perform in-place metadata sanitization across all files within a directory:
```bash
mat2 --inplace /PATH-TO-FOLDER/*
```

> [!IMPORTANT]
> When executing the `--inplace` flag, acknowledge that original metadata is permanently removed from the source file. If maintaining original document timestamps is critical for internal archiving, utilize the default mode to generate `.cleaned` duplicates.

With files fully anonymized and stripped of digital tracking markers, external transmission risks are mitigated. To handle remaining operational sources, drafts, and temporary artifacts residing on the encrypted LVM drive, proceed to the tools designed for complete physical destruction within the file system.

#### Secure and Irreversible File and Directory Destruction:

To securely erase private data, directories, and files beyond recovery, use the specialized CLI utility `wipe`, which overwrites information using complex multi-pass algorithms. Alternatively, the standard built-in utility `shred` reliably sanitizes individual files, though it lacks native architectural support for directory structures.

> [!IMPORTANT]
> **Author's Critical Note on Solid-State Drive Operations:**
> On modern Solid-State Drives (SSDs), utilities such as `shred` and `wipe` do not guarantee 100% physical data erasure at the NAND cell level. This limitation stems from internal controller **Wear Leveling** algorithms, which dynamically distribute write operations across varying physical flash memory addresses to extend drive longevity. Furthermore, executing high pass counts (such as the 35-pass Gutmann method) needlessly degrades an SSD's total bytes written (TBW) endurance.
> 
> Because the underlying Ubuntu system is fully encrypted at the kernel level using LUKS, 1 to 3 overwrite passes are sufficient to permanently neutralize data on an SSD. Once a file's metadata inside the encrypted volume is overwritten, recovering leftover data blocks from floating SSD cells becomes mathematically impossible outside the decrypted LUKS container, as unlinked blocks remain rendered as unreadable cryptographic noise.

Open the terminal and execute the following steps:

**1.** Install the data destruction utility `wipe`:
```bash
sudo apt install wipe -y
```

**2.** Recursively purge a target directory along with all contained subitems (replace the `FOLDERNAME` placeholder with the target directory name):
```bash
wipe -rfi FOLDERNAME
```

The `-r` flag enables recursive operation, `-f` suppresses confirmation prompts, and `-i` activates verbose interactive mode to monitor sector overwrite progress.

**3.** Initiate destruction of all files within the active terminal directory (**Execute with caution!**):
```bash
sudo shred -v -u -z -n 3 *
```

> [!WARNING]
> **Warning!** Using the wildcard operator `*` in Linux carries operational risk. The `*` character is expanded by the shell prior to command execution. If nested subdirectories exist within the active path, `shred` will encounter them, throw a system error (*"shred: failed to open for writing: Is a directory"*), and potentially abort the execution chain prematurely.
> 
> To ensure deterministic execution, couple the command with the `find` utility:

**4.** Safely purge all regular files limited strictly to the current working directory level without altering nested folder structures:
```bash
find . -maxdepth 1 -type f -exec shred -v -u -z -n 3 {} \;
```

**5.** Permanently destroy a specific isolated file (replace the `FILENAME` placeholder with the exact case-sensitive filename and extension):
```bash
shred -v -u -z -n 3 FILENAME
```

#### Operational Parameters for the shred Utility:

* **`-v`** (*verbose*) — Display real-time progress of the operation within the console output.
* **`-u`** (*unlink*) — Forcefully truncate and remove the file from the file system, clearing its filename entry after successful overwrite passes.
* **`-z`** (*zero*) — Perform a final pass with zeroes to conceal the fact that data wiping took place.
* **`-n 3`** — Specify the exact number of overwrite passes (for SSD storage media, set a safe and sufficient count of 3).

> [!IMPORTANT]
> By default, Ubuntu operates on the Ext4 file system with active block journaling (`data=ordered`). This mechanism records file metadata and structural fragments into a hidden system journal prior to committing physical drive writes. While utilities like `shred` and `wipe` overwrite a file at its current physical address, they cannot reach leftover data copies residing inside the Ext4 journal—a limitation explicitly highlighted in the official system manual (`man shred`).
> 
> Full-disk LUKS encryption completely mitigates this vulnerability (as the Ext4 journal itself resides inside the encrypted LUKS container). However, when wiping files on an external unencrypted Ext4 flash drive, remain aware that fragments of deleted files may persist within its system journal.

#### Global Wiping of Unallocated Disk Space:

If the operating system has been running for an extended period and sensitive files were deleted using standard graphical methods (pressing **Delete** to move items to the Trash), a vast amount of non-overwritten residual traces remains on the storage device. To permanently eliminate all previously deleted files on an SSD simultaneously—without waiting for random OS overwrites—deploy the specialized `secure-delete` package:

**1.** Install the secure deletion utility suite:
```bash
sudo apt install secure-delete -y
```

**2.** Initiate total sanitization of unallocated space on the current system partition:
```bash
sudo sfill -v -z -l /
```

> [!NOTE]
> The `-l` (*low security*) parameter reduces the overwrite process to two optimal passes. This significantly preserves SSD endurance while guaranteeing that all free disk space—including residual fragments in hidden system journals, temporary directories, and logs—is populated with random data and final zeroes.

<br>

## Steganography, Obfuscation, and Anti-Forensics Trace Hiding in Ubuntu

#### Introduction:

Once metadata is sanitized using `mat2` and temporary files are guaranteed destroyed via `shred` or `wipe`, the next challenge emerges: how to transmit or store critical information so that the very fact of its existence remains deeply hidden.

Under conditions of severe state censorship and pervasive network surveillance, simple data encryption frequently attracts unwanted attention from monitoring systems, as an encrypted file presents itself as suspicious "digital noise." To mitigate this issue, deploy steganography (embedding data within secondary carrier objects) and obfuscation (scrambling information) techniques.

#### Linux Steganography: Concealing Files Within Media Content:

Steganography enables deep embedding within an innocuous container file (such as a photo or audio recording). The cover file maintains full functionality, opens cleanly in standard media players, and remains visually indistinguishable from the original.

> [!IMPORTANT]
> The cover file must be genuine, high-quality, and sufficiently large. Otherwise, injecting secret payloads introduces anomalous discrepancies between the image's physical file size and its visual resolution, triggering suspicion during analysis.

#### The steghide Command-Line Utility:

Start with the classic approach. `steghide` is a fully command-line utility residing in the official Ubuntu repositories. It is ideal for automation within bash scripts (for example, covertly backing up security logs). The utility embeds data into JPEG, BMP, WAV, and AU file formats using robust AES-256 encryption by default.

**1.** Install the package using a single command:
```bash
sudo apt update && sudo apt install steghide -y
```

**2.** Hide the secret file `secret.txt` inside a regular image `photo.jpg`:
```bash
steghide embed -cf photo.jpg -ef secret.txt
```

**3.** Permanently remove the original `secret.txt` file remaining outside the steganographic container:
```bash
shred -v -u -z -n 3 secret.txt
```

The system will prompt for and confirm a strong passphrase. The resulting `photo.jpg` file remains visually identical to its original state.

**4.** To extract the hidden payload from the container, execute:
```bash
steghide extract -sf photo.jpg
```

Enter the secret passphrase defined during creation to extract the original file back to disk.

> [!IMPORTANT]
> The `steghide` utility operates exclusively with legacy formats: **JPEG, BMP, WAV, and AU**. Attempting to process modern formats like **PNG** or **MP3** will fail. This limitation stems from format-specific compression mechanics:
> * PNG uses lossless compression. The `steghide` embedding method disrupts the PNG optimization algorithm, resulting in anomalous file size growth that reveals the covert channel.
> * MP3 uses lossy compression. The MP3 algorithm treats data embedded within audio stream bits as "extraneous digital noise" and strips it during playback or conversion.

#### Stealth Concealment via the Advanced StegoForge Tool:

StegoForge is a dual-use (Red/Blue Team) framework designed both for covertly embedding payloads into media files and detecting hidden containers using integrated forensic analysis algorithms.

Unlike legacy single-format tools, this framework features multi-container support:

* **Images:** Data injection via classic LSB, adaptive LSB, and DCT coefficient manipulation in JPEG. Supports PNG, JPG/JPEG, BMP, and other formats.
* **Audio:** Writing payload data to spectrograms or leveraging psychoacoustic masking within uncompressed PCM formats (audio frequencies imperceptible to the human ear). Supports WAV, FLAC, MP3, and others.
* **Video:** Motion vector modification within MP4 and WebM streams. Also supports AVI, MKV, MOV, and others.
* **Documents:** Injecting data directly into XML structures, utilizing incremental updates and undocumented objects within PDF files, as well as manipulating line spacing and invisible fonts. Supports DOCX, PDF, PPTX, and others.
* **Network Packets:** Concealing data within unallocated protocol header fields (e.g., TCP/IP) contained in network capture files (PCAP).

The framework is engineered to defeat 11 advanced steganalysis modules built directly into its engine for resilience testing. These include statistical evaluation (Chi-square test, RS analysis), signature scanning engines, and convolutional neural networks (ONNX CNN models) trained to detect spatial anomalies in files. To bypass all 11 detection engines, the framework applies adaptive embedding algorithms: rather than writing bits sequentially, payload data is distributed unevenly across the container. Bits are allocated exclusively to noisy image regions or high-motion video frames where modifications exert minimal impact on overall file statistics. Maintaining an un-altered statistical histogram ensures neural and mathematical detection modules return a "No Payload Detected" status.

Payload security relies on cryptography rather than algorithm secrecy. If a container file is discovered, adversaries encounter robust cryptographic defenses:

* **Encryption:** All payloads are encrypted using AES-256 in GCM mode prior to embedding, ensuring confidentiality and data authenticity.
* **Key Derivation:** User passphrases are transformed into cryptographic keys using the memory-hard Argon2 function, neutralizing brute-force attempts.
* **Plausible Deniability:** The utility supports generating two distinct decryption keys for a single container. The decoy (false) key extracts an innocuous text payload, whereas the primary (true) key unlocks the authentic hidden file.

**1.** Download the application binary from the `github.com` repository:
```bash
wget https://github.com/Nour833/StegoForge/releases/download/v1.1.5/stegoforge-linux-x86_64
```

**2.** Create a directory for local user binaries, move the executable file, grant execution permissions, and update system PATH settings:
```bash
mkdir -p ~/.local/bin && mv ~/stegoforge-linux-x86_64 ~/.local/bin/stegoforge && chmod +x ~/.local/bin/stegoforge && grep -qxF 'export PATH="$HOME/.local/bin:$PATH"' ~/.bashrc || echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

**3.** Launch the framework executable:
```bash
stegoforge
```

Upon launching `stegoforge`, the primary console menu renders:

* 1 — Encode ........Hide an encrypted payload inside a selected container file.
* 2 — Decode ........Extract and decrypt a hidden payload.
* 3 — Detect ........Inspect a file for suspected steganographic payloads.
* 4 — CTF Mode ......Run all available detection engines and generate a detailed forensic report.
* 5 — Capacity ......Calculate the maximum payload capacity supported by a container file.
* 6 — Web UI ........Launch a local web interface for browser-based operations.
* 7 — Survival ......Test payload survival against platform processing and container conversions.
* 8 — Dead Drop .....Dead drop tools and key exchange utilities.
* 9 — Update ........Check GitHub for upstream releases and perform an in-place upgrade.
* d — Diff ..........Compare original and modified container files, including pixel heatmap visualizations.
* b — Batch .........Perform payload embedding across multiple container files in a directory.
* q — Quit ..........Exit StegoForge.

Reference this structural guide for routine operational workflows:

* Embed a file → 1 Encode
* Extract an embedded payload → 2 Decode
* Scan a suspicious file → 3 Detect
* Execute full forensic analysis → 4 CTF Mode
* Determine container capacity → 5 Capacity
* Operate outside the terminal → 6 Web UI
* Compare original and modified files → d Diff
* Process multiple files in bulk → b Batch

> [!TIP]
> To streamline operations with StegoForge, utilize the Web UI. It supplies a graphic interface covering core framework utilities while eliminating manual parameter entry. The Web UI runs locally and binds strictly to `http://127.0.0.1:5000/`.
> 
> To launch the interface, open a terminal and execute:
> ```bash
> stegoforge
> ```
> 
> Within the console menu, select option 6 (6 — Web UI). Once initialized, open `http://127.0.0.1:5000/` in your browser.

#### Archive Concatenation (Quick Hack Without Third-Party Software):

This method leverages the structural properties of binary files. Most image viewers parse files from the beginning, whereas archive managers process structure strictly from the end of the file. Merge both components physically using the host terminal.

**1.** Pack secret documents into an encrypted ZIP archive:
```bash
zip -e secret.zip secret.txt
```

**2.** Concatenate the cover image and the archive into a single target file using `cat`:
```bash
cat cat.jpg secret.zip > final_photo.jpg
```

* **Hardening Outcome:** Opening `final_photo.jpg` via standard GUI file managers renders the original cat image cleanly.
* **Extraction Workflow:** Right-click the file ➔ *Open With "Archive Manager"* (or execute `unzip final_photo.jpg` directly in the terminal). The archive utility skips leading image bytes, reading and extracting the hidden archive structure from the end of the file.

#### Text Obfuscation: Bypassing Automated Inspection Systems (DPI):

Automated monitoring systems and Deep Packet Inspection (DPI) appliances continuously scan network traffic, communications, and files for stop-words or prohibited signature markers. Altering text structure enables bypassing automated signature-based filtering mechanisms.

* **Character Homoglyph Insertion:** Replacing specific letters with visually identical characters from alternate alphabets breaks automated signature detection entirely. For instance, the Cyrillic letter `С` and the Latin letter `C` appear identical on-screen, yet contain distinct byte-codes. To an automated scanner, `Секрет` (containing a Latin C) and `Секрет` (containing a Cyrillic C) represent entirely distinct entities, causing the filter to permit text that remains completely legible to a human reader.
* **Zero-Width Character Injection:** Injecting zero-width spaces (`U+200B`) fractures words into discrete fragments for search crawlers while maintaining a continuous, monolithic display within the end-user's rendering engine.

#### Analyzing Hidden Threats: File Extension Spoofing (BiDi Attacks):

For defending teams and high-risk users, understanding how Unicode manipulation is weaponized to bypass vigilance is critical to maintaining operational security.

One primary vector exploits a specialized invisible Unicode control character: **U+202E (RLO — Right-to-Left Override)**. This character instructs the rendering engine to display all trailing text in reverse order (right-to-left).

Embedding this hidden control character into an executable filename causes the GUI environment to invert its ending visually, masking the threat completely:
* **Actual System Filename (Parsed by Kernel):** `document_[U+202E]fdp.exe`
* **Rendered GUI Display (Visible to User):** `document_exe.pdf`

To the operating system, the file remains a fully functional executable binary (`.exe`), whereas the user perceives a benign document (`.pdf`).

**1.** Simulate string rendering with the hidden inversion character embedded:
```bash
echo -e "File_name_\u202Efdp.exe"
```
The terminal executes the layout override, rendering the deceptive output: `Filename_exe.pdf`.

**2.** To detect hidden manipulation, pipe the output into `cat` using the `-v` flag (displaying non-printing and control characters):
```bash
echo -e "File_name_\u202Efdp.exe" | cat -v
```
*The output strips the visual illusion, exposing explicit Unicode control codes (such as `^[[~` or its hex equivalent) and immediately revealing the manipulation.*

> [!WARNING]
> When handling files originating from external or untrusted sources, never rely on file extensions rendered within GUI file managers. Open a terminal and inspect the file using the native `file` utility:
> ```bash
> file name_of_file
> ```
> The `file` utility inspects internal document structures (magic bytes and headers) that cannot be spoofed by simple filename alterations. If an executable Linux (ELF) or Windows (PE) binary is disguised as an image, the utility will report its true format.

<br>

## Installing and Configuring the VeraCrypt Cryptographic Suite

#### Introduction to VeraCrypt and Installation:

VeraCrypt serves as a powerful utility for constructing isolated encrypted containers, as well as executing full-disk encryption across external USB drives and hard disks. The software provides absolute resistance to cryptanalysis and was engineered specifically to meet stringent security standards.

**Installation via Community PPA Repository:**

If automated system-wide package updates are preferred alongside OS maintenance, deploy the popular third-party security repository:

**1.** Integrate the third-party encryption repository into the operating system:
```bash
sudo add-apt-repository ppa:unit193/encryption -y
```

> [!IMPORTANT]
> This PPA repository is maintained by independent community developers. Following fresh Ubuntu releases, compiled packages matching a specific distribution version may temporarily be unavailable, causing the installation command to fail with a *"Package not found"* error.
> 
> If this occurs, purge the PPA from the system using `sudo add-apt-repository --remove ppa:unit193/encryption -y` and proceed strictly with **(Native Method)**.

**2.** Install `VeraCrypt` from the added repository:
```bash
sudo apt install veracrypt -y
```

**3.** Launch the application:
```bash
veracrypt
```

**Installation via Official Distribution Package (Native Method):**

To eliminate dependency conflicts across modern Ubuntu 24.04 and 26.04 LTS environments, deploying the official stable build directly from the IDRIX development team is recommended:

* Open a browser and navigate to the official project site: `https://veracrypt.fr`.
* Download the current installer package for Ubuntu (a `.deb` file for the `amd64` architecture, e.g., `veracrypt-x.x.x-Ubuntu-amd64.deb`).
* Open a terminal within the downloads directory (`~/Downloads`) and execute installation using the following commands:

**1.** Update the local system package index:
```bash
sudo apt update
```

**2.** Install the downloaded `.deb` package (the `apt` package manager automatically resolves all underlying system dependencies):
```bash
sudo apt install ./veracrypt-*.deb -y
```

**3.** Launch the cryptographic platform's graphical user interface:
```bash
veracrypt
```

#### Deep Security Tuning: RAM Key Protection (Paranoia Mode):

By default, when mounting encrypted volumes, VeraCrypt retains master decryption keys in RAM in plaintext. If an adversary gains physical access to a powered-on host, they could attempt to extract these keys using low-level attacks such as a *Cold Boot* attack (freezing and reading memory chips) or via hardware DMA interfaces.

To eliminate this compromise vector entirely, navigate within the VeraCrypt GUI along the following path: **Settings** ➔ **Preferences** (under the **Security** tab) and force-enable the available protection setting:

* **"Wipe cached passwords on exit"** *(Force-purge cached passwords and keyfiles from RAM upon exiting the application)*.

> [!NOTE]
> Unlike bloated Windows builds, the native Linux release of VeraCrypt omits redundant RAM encryption and extended caching toggles. This design stems from core Linux kernel mechanics: mandatory virtual memory access controls isolate runtime memory spaces of non-privileged users at the hardware interface level, preventing unauthorized dump extraction without root privileges. Enabling this single cache-wiping setting upon exit provides complete offline protection for operational master keys.

#### A Fundamental Security Tool: Creating Hidden Volumes:

When operating under elevated threat levels, severe censorship, or the risk of forced device inspection at border checkpoints, a mechanism for **Plausible Deniability** becomes vital. VeraCrypt facilitates this capability through the creation of a **Hidden Volume**.

The operational concept relies on generating a single standard encrypted container file configured with two distinct, independent passphrases:
* **Outer Volume:** Protected by the primary passphrase. This segment holds benign, non-sensitive files whose presence appears legitimate and natural (family archives, public documents, harmless literature).
* **Hidden Volume:** Resides within the unallocated space of the outer volume and is secured by a secondary, secret passphrase. It is cryptographically formatted such that its constituent data blocks are mathematically indistinguishable from random digital noise (unallocated space). No forensic analysis software can prove the existence of this secondary hidden partition inside the container file.

Under coercion or forced passphrase disclosure, supplying the primary (decoy) passphrase mounts the outer volume natively, presenting benign files to inspectors. Proving the existence of the hidden volume remains technically impossible, as the container outwardly presents as a standard encrypted volume containing legitimate data alongside randomized unallocated blocks. True confidential files, keys, and private logs unlock exclusively when mounting the volume with the secondary passphrase in a secure environment.

> [!IMPORTANT]
> By default, modifying data within a container causes the operating system to update the file's last-modified timestamp on disk. If the hidden volume is accessed and updated covertly, internal container headers change while the timestamps visible on the outer decoy file remain static—instantly exposing the use of a hidden volume to forensic experts.
> 
> To eliminate this artifact completely, navigate within the VeraCrypt main menu to **Settings → Preferences** and enable the **"Preserve modification timestamp of file containers"** option within the global settings panel. This instructs the application to lock the container file's timestamp, keeping the hidden structure indistinguishable from standard randomized encrypted data.

#### Ultimate Hardening: Configuring PIM and Hardware Keyfiles:

To defend mission-critical containers against advanced cryptanalysis and targeted brute-force attacks (password-cracking arrays built from multi-GPU clusters), a standard text passphrase is insufficient. Leverage internal VeraCrypt features to achieve maximum security hardening.

By default, during volume creation, VeraCrypt applies a fixed, massive number of cryptographic hash iterations to protect the volume header. This drastically slows down brute-force attempts by adversaries while slightly increasing mount times for the user.

The **PIM** (Personal Iterations Multiplier) parameter allows manual specification of a unique multiplier integer during container setup.

> [!TIP]
> **Security Strategy:** Specifying a high PIM value reduces adversary password-cracking speeds to near zero—compute clusters would require millennia to attempt even basic passphrases. The trade-off: local volume mounting will take several seconds longer.
> 
> Conversely, if container security relies on an extremely long and complex passphrase (exceeding 30–40 randomized characters), the PIM value can be intentionally reduced (below a 4-digit integer) to achieve instantaneous mounting without waiting.

Link one or multiple keyfiles (such as images, audio tracks, documents, or randomly generated binary files) to the container. Mounting the volume then requires providing the correct text passphrase while simultaneously specifying the exact paths to these keyfiles. Without the designated keyfiles, volume decryption remains mathematically impossible even if the passphrase is compromised.

> [!WARNING]
> **Critical Rule for Keyfile Protection in Computer Forensics:**
> Never store keyfiles on the internal drive of the host machine. Keep them exclusively on external portable media—such as a standard SD card equipped with a physical **Lock/Write-Protect** switch.

Before inserting the SD card into a card reader to mount the container, ensure the **Lock** slider is engaged in the write-protected position.

This measure counteracts modern forensic analysis tools that inspect file access timestamps (`atime` attributes) across seized media. Operating a drive in standard read-write mode causes the operating system to overwrite keyfile access metadata automatically when mounting the volume, leaving fresh hidden timestamps.

During forensic inspection, locating a storage card where only a few files among thousands share exact metadata modification timestamps matching suspected user activity allows investigators to pinpoint keyfiles rapidly. Engaging physical write-protection on the SD card ensures the memory controller cannot alter a single bit of metadata, completely concealing the access history and utilization of the keyfile.

## Real-World Threat Modeling: Why Paranoia Must Be Systemic:

To permanently reinforce the concepts of trace sanitization, steganography, encryption, and hidden `VeraCrypt` containers, examine a classic real-world scenario frequently encountered by independent investigators and activists operating under repressive or authoritarian regimes.

Consider a journalist under heavy surveillance by local intelligence services. Having followed security best practices, the host setup is technically flawless: Ubuntu is deployed over a fully encrypted LUKS pool, operational archives reside inside a hidden `VeraCrypt` container protected by a plausible deniability double bottom, the network stack is locked behind a strict firewall Kill Switch, and all outbound traffic routes strictly through chained encrypted VPN tunnels. From a host-hardening perspective, this system is an impenetrable digital fortress. In the event of a raid or physical seizure, the hardware reveals zero actionable data.

However, the investigator commits a single fatal mistake. Mounting the hidden container, they extract an investigative text document or a fresh screenshot of a classified facility and publish it directly to an open channel, a messaging app, or an independent media mirror—assuming their VPN and host encryption guarantee complete protection.

Hours later, an enforcement team arrives.

**How did this happen, and why did the fortress collapse?**

Adversaries did not need to break the LUKS partition or brute-force the VeraCrypt passphrase. They simply downloaded the published file and executed routine forensic metadata analysis (OSINT). The file retained:

* **Hidden Application Metadata:** Local usernames, hostnames, absolute directory paths, revision histories, and document-specific internal property fields.
* **Timestamp Artifacts:** Precise hidden EXIF creation and modification timestamps, which intelligence services immediately correlated against ISP access logs and session timing patterns on targeted network gateways.
* **Hardware Identifiers:** Embedded GPS coordinates and camera sensor serial numbers (in the case of photographic evidence).

This critical failure demonstrates that local disk hardening and network anonymity are completely invalidated if the transmitted object broadcasts host-identifying markers to the external environment. Operational security must encompass the entire data lifecycle without exception.

Operational hygiene tolerates no compromises. Maintain absolute vigilance and inspect every byte.

**Chapter Assets:** *_assets\images\11_veracrypt*

<br>

## Using Yubico Security Keys

#### Introduction:

Integrating hardware authentication factors—physical security keys inserted into computer USB ports (Type-A or Type-C)—serves as a critical component of privacy and local system hardening.

The most widely adopted and proven devices across the cybersecurity industry are manufactured by Yubico. For standard implementation tasks, any model featuring hardware FIDO U2F support is suitable (which encompasses virtually the entire product lineup). The most cost-effective option is the basic *Yubico Security Key*, while more advanced variations include the *YubiKey 5* series (including FIPS-certified editions). From the perspective of PAM subsystem configuration logic, the specific hardware model selected is irrelevant.

#### Installation:

First, install the necessary libraries and utilities for U2F standard integration:

**1.** Download and deploy the U2F PAM module and key generation tools:
```bash
sudo apt update && sudo apt install libpam-u2f pamu2fcfg -y
```

**2.** Enter an interactive root shell to configure system-level parameters:
```bash
sudo -i
```

**3.** Create an isolated directory within the system environment to securely store hardware identifiers:
```bash
mkdir -p /etc/Yubico
```

**4.** Bind the hardware security key to the active user account using the `$SUDO_USER` variable:
```bash
pamu2fcfg -u $SUDO_USER > /etc/Yubico/u2f_keys
```
*Upon executing command #4, the utility polls the hardware bus for 15 seconds. If a key is not currently connected, the terminal displays: "No U2F device available, please insert one now...". Insert the YubiKey into a USB port immediately and touch the flashing gold contact pad on the physical token.*

**5.** Set strict file permissions on the generated keyfile, permitting system read access while prohibiting modifications:
```bash
chmod 644 /etc/Yubico/u2f_keys
```

Next, configure the core PAM subsystem to enforce physical token authentication across administrative terminal commands, session switches, system logins, and GUI authentication prompts:

**6.** Open the global authentication configuration file:
```bash
nano /etc/pam.d/common-auth
```

**7.** Insert the following security rule at the very top of the file, **strictly above the first line of commented text**:
```ini
auth required pam_u2f.so authfile=/etc/Yubico/u2f_keys originuser cue
```

To save configuration changes in `nano`, press **"Ctrl + O"** → **"Enter"**, followed by **"Ctrl + X"** to exit back to the shell.

Before closing the active shell, verify the entire configuration in a parallel session to prevent lockout!

**8.** Leaving the current terminal session active, open a parallel window and test authentication using:
```bash
sudo -i
```

If configured correctly, the terminal prompts with *Please touch the authenticator*, and the YubiKey flashes, requiring a physical touch to open the root shell.

Once verified, safely close all terminal windows—the host perimeter is now fully secured.

> [!WARNING]
> Enforcing a rigid `required` PAM policy using a single physical token introduces significant lockout risk. If the single YubiKey is lost, physically damaged, or suffers connector wear, access to the operating system will be permanently lost. Binding a secondary (backup) security key—stored securely off-site—to the user profile is strongly advised.
> 
> To enroll a backup key, remove the primary token, insert the backup hardware token into a USB port, re-enter the root shell:
> ```bash
> sudo -i
> ```
> 
> Append the backup key identifier directly to the configuration file:
> ```bash
> pamu2fcfg -u $SUDO_USER >> /etc/Yubico/u2f_keys
> ```
> Using the append redirection operator `>>` is critical. This appends the configuration identifier of the secondary token as a new line at the end of the existing file without overwriting primary key records.

#### Implementing a Hardware Kill Switch via Kernel udev Rules:

To achieve ultimate host fortification, construct a kernel-level hardware failsafe using the Linux `udev` subsystem. Upon emergency removal of the security token from a USB port, the system instantly locks the active Ubuntu desktop session, forcibly isolating open runtime sessions and purging active master keys from system RAM.

**1.** Create a custom configuration file for host USB rules:
```bash
sudo nano /etc/udev/rules.d/80-yubikey-kill.rules
```

**2.** Insert the following rule. To ensure the hardware Kill Switch triggers reliably across all token hardware variations (such as flagship YubiKey 5 devices or entry-level Yubico Security Keys) while ignoring transient software interface resets, bind the low-level HID path removal event (`0003:1050`) to a dynamic USB bus query using `lsusb`. Session locking fires strictly when the device physically disconnects from the host ports:
```ini
ACTION=="remove", DEVPATH=="*/0003:1050:*", RUN+="/bin/sh -c '/usr/bin/lsusb -d 1050: || /usr/bin/loginctl lock-sessions'"
```

Save the file in `nano` using **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit.

**3.** Reload udev rules in real time to apply the new kernel trigger immediately:
```bash
sudo udevadm control --reload-rules && sudo udevadm trigger
```

> [!NOTE]
> Under emergency conditions—such as physical intrusion, forced seizure of an active laptop, or unauthorized access to a workstation—pulling the Yubico token from its USB slot triggers protection instantly. The kernel `udev` subsystem intercepts the hardware interrupt within milliseconds and signals `loginctl` to lock all active user sessions.

> [!WARNING]
> Because multi-factor PAM authentication is enforced globally across the operating system, graphical authorization prompts for elevated applications may fail to complete automatically. In these instances, launch elevated utilities manually from a terminal interface (for example: `sudo timeshift-gtk`).

<br>

## Installing and Configuring USBGuard

#### Introduction:

To prevent unauthorized USB devices from connecting to an active Ubuntu host, deploying USBGuard serves as a crucial preventive measure.

Consider a human rights defender operating in an authoritarian country. Fully aware of digital security risks, they prepared their workstation in advance: deployed Ubuntu on an encrypted LUKS partition, configured a VPN, firewall, YubiKey, and other security primitives. They remain convinced that the primary threat stems from network-borne vectors and remote exploitation attempts.

One day, a trusted associate pays a visit. While the defender steps away for literally a few seconds to brew coffee, the associate takes advantage of the moment to insert a pre-configured USB flash drive into the host. The operating system automatically enumerates and accepts the new USB device, triggering malicious software installation.

Shortly after, confidential documents and sensitive assets are compromised.

**Why did security fail?**

Because physical access to an active system was omitted from the threat model. Disk encryption primarily protects assets while the computer is powered off, a VPN secures the network channel, and a YubiKey resolves hardware authentication tasks. None of these mechanisms independently answer the core question: **Which USB devices should the operating system trust by default?**

If connecting an unknown USB device is permitted automatically, an adversary requires only brief physical access to an unlocked host to achieve full compromise.

This exact scenario is what USBGuard addresses. Its objective is to enforce an explicit whitelist of authorized USB devices while denying all non-whitelisted hardware under the core security principle of **"deny everything not explicitly allowed"**.

Furthermore, modifying the persistent policy must remain a strictly administrative operation. An unprivileged user sitting at the workstation must not be capable of simply plugging in an unknown device and approving it via a GUI prompt.

While this does not render the system invulnerable nor eliminate every physical access vector, it effectively seals one of the most accessible attack vectors: weaponizing an unattended active host by inserting unauthorized USB hardware.

Below, we cover the installation and configuration of USBGuard to establish a minimal policy where only explicitly authorized devices are trusted by the OS kernel.

#### Installation and Setup:

**1.** Install USBGuard:
```bash
sudo apt update && sudo apt install usbguard -y
```

**2.** Verify the installed utility version and package information:
```bash
apt policy usbguard
```

> [!WARNING]
> Once USBGuard starts, any new USB devices lacking an explicit allow rule will be blocked automatically. Prior to starting the service, ensure the previously configured YubiKey remains connected (unless a hardware Kill Switch is active). After launching the daemon, test policy enforcement using a secondary USB flash drive or another non-critical device.

**3.** Enable USBGuard to launch at system boot and immediately verify service status:
```bash
sudo systemctl enable --now usbguard && systemctl status usbguard --no-pager
```

**4.** Open the USBGuard configuration file, which defines how the daemon handles existing and newly connected USB hardware:
```bash
sudo nano /etc/usbguard/usbguard-daemon.conf 
```

**5.** Clear the contents of the file using **"Ctrl + K"** and insert the following parameters:
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

**6.** Open the `rules.conf` configuration file to manage rules and add new devices:
```bash
sudo nano /etc/usbguard/rules.conf
```

Carefully inspect which hardware is permitted by the active policy. If necessary, remove devices from the list that do not require access. For instance, an integrated laptop webcam can be blocked simply by removing its corresponding rule entry.

**7.** Verify that an unprivileged user lacks access to the IPC interface:
```bash
usbguard list-devices
```

The terminal must return an access denial error: `ERROR: IPC connect: service=usbguard: Operation not permitted`

Next, consider a straightforward example of authorizing a device while simultaneously verifying USBGuard operation. To do this, insert an unlisted USB flash drive or secondary YubiKey into a USB port.

**8.** Open `rules.conf` for editing:
```bash
sudo nano /etc/usbguard/rules.conf
```

Locate the new device entry blocked by USBGuard due to a missing rule, and change its state parameter from `block` to `allow`.

**9.** Restart the service to apply changes:
```bash
sudo systemctl restart usbguard
```

Following the restart, the newly added device transitions to an authorized state and becomes fully accessible to the system.

<br>

## Installing the KeePassXC Local Password Manager

#### Introduction:

To securely and centrally store all system passphrases, cryptographic keys, GRUB boot passwords, and user account credentials, deploy the offline KeePassXC password manager. The utility operates over an encrypted database container backed by robust AES-256 encryption. Depending on available hardware and operational security requirements, select one of three container protection schemes.

#### Vault Protection Scenarios:

* **Basic Scenario:** Database protection using a master passphrase alone. The primary risk vector remains container theft: if an adversary acquires the `.kdbx` database file and covertly logs the passphrase (e.g., via a hidden keylogger), the vault is fully compromised.
* **Advanced/Two-Factor Scenario:** Hardening the master passphrase with a unique keyfile (*Keyfile*). Virtually any existing file (such as an image, audio recording, or document) can serve as a keyfile, or one can be generated randomly within the application itself.

> [!WARNING]
> Storing the keyfile on a separate external physical medium (such as an encrypted flash drive or SD card) and connecting it strictly when opening the database is the ideal configuration. Keeping the keyfile exposed in the same directory as the `.kdbx` file itself is strictly prohibited! If external media is unavailable, any third-party file deeply buried within the file system that is guaranteed never to undergo modification may be used (e.g., a specific personal photo, PDF manual, or MP3 track). Altering even a single byte or metadata attribute within this file permanently locks the encrypted container. When employing this method, creating an offline backup of the file to independent storage is mandatory to protect against accidental deletion or corruption.

* **Ultimate Scenario:** Hardening the master passphrase via a YubiKey hardware token leveraging the low-level Challenge-Response algorithm. This implementation strictly requires a fully featured *YubiKey 5 Series* (or YubiKey 4) hardware key. The entry-level *Yubico Security Key* lineup (typically blue hardware units) is entirely incompatible, as it lacks the HMAC-SHA1 cryptographic response feature.

#### Installing the Software Suite:

Once network interfaces and secured VPN gateways are successfully configured, and local package indices are updated, open a terminal session to perform the installation.

**1.** Add the developers' official PPA repository to fetch the latest secure build of KeePassXC:
```bash
sudo add-apt-repository ppa:phoerious/keepassxc -y
```

**2.** Install the password manager, token CLI utility, and the secure clipboard sanitization library using a single command (the package index refreshes automatically upon adding the PPA):
```bash
sudo apt install keepassxc yubikey-manager xclip -y
```
> *(The `xclip` package is included preventatively to allow KeePassXC to clear the system clipboard automatically on a set timer following password copy operations, neutralizing background clipboard stealer scripts).*

#### Creating and Hardware-Securing the Database:

**1.** Launch the application via the standard GNOME desktop application menu (or by entering `keepassxc` in the terminal).

**2.** In the welcome GUI window, click **Create new database**.

**3.** Enter an arbitrary database filename (for example, `vault`) and click **Continue**.

**4.** Leave the encryption parameters at their default values on the configuration screen. Click **Continue**.

**5.** In the **Master Password** dialog, set a main database passphrase at least 16–20 characters long (passphrase length may be significantly reduced when combining it with a YubiKey hardware token). Ensure this password is securely memorized.

* If configuring the **Basic Scenario:** Ignore extra parameters, select no additional options, and proceed directly to step 11.
* If configuring the **Advanced/Two-Factor Scenario:** Skip to step 6.
* If configuring the **Ultimate Scenario:** Skip to step 9.

**6.** Check the **Key file** option, click **Add Key File**, and select **Create** from the drop-down menu to generate a new randomized cryptographic key sequence (or select the path to an existing, immutable disguise file on the host).

**7.** Upon generating a new keyfile, the application prompts to save it. Connect an external flash drive or SD card and save the file using a neutral name.

**8.** Click **Continue** and skip to step 11.

**9.** Click **Add YubiKey Challenge-Response**.

**10.** Program Slot 2 for offline challenge-response calculations (or verify its current status). If configuring a brand-new token, initialize Slot 2 first via the terminal using `ykman otp chalresp --generate 2`. If the key is already used for authenticating an existing KeePassXC database via Slot 2, **DO NOT** execute the initialization command again, as it will overwrite the active HMAC secret! The application will detect the USB hardware token immediately. Click **Continue**.

**11.** The application prompts to save the resulting database container file with the `.kdbx` extension. Choose a destination path (for example, the root home directory `~/vault.kdbx`).

> [!NOTE]
> Integrating the YubiKey hardware factor (HMAC-SHA1) fundamentally alters the threat model. Even if the master passphrase is reduced to just 8 characters, offline brute-force attempts using multi-GPU or ASIC arrays become completely futile. Without physical access to the connected hardware token, adversaries are forced to brute-force the chip's hidden 160-bit cryptographic response sequence—a task mathematically impossible prior to the heat death of the universe. In this deployment scheme, the sole remaining attack vector is live password interception via a keylogger on a compromised host, which the hardened 4x4 host defense model is specifically designed to neutralize.

#### Deep Hardening of Internal Security Settings:

Open the menu via **Tools** ➔ **Application Settings** and forcibly enable the following security parameters:

* **Security** tab ➔ **Timeouts** section:
* **Clear clipboard after** — set strictly to *5–10 seconds* (this triggers the `xclip` utility).
* **Lock database after inactivity** — enable and set to a strict limit of 600 seconds (10 minutes).
* **General** tab ➔ **Entry Management** section:
* **Hide window when copying to clipboard** — enable to minimize the application interface to the system tray immediately upon pressing **"Ctrl + C"**.

> [!WARNING]
> Refrain from installing any third-party browser extensions (including the official KeePassXC-Browser) into your Firefox installation. First, browser extensions run within the shared WebExtensions API context, introducing a potential Cross-Site Scripting (XSS) attack vector and risking credential extraction from an unlocked database via plugin vulnerabilities. Second, enforcing strict security controls (`privacy.resistFingerprinting = true`) inside Firefox completely blocks and breaks local Unix socket IPC channels required for extension integration. The standard for a sovereign 4x4 host deployment is utilizing the native **Auto-Type** engine exclusively.

#### Secure Data Entry via Protected Clipboard:

Because the modern graphical subsystem in Ubuntu 24.04/26.04 LTS runs on the **Wayland** protocol, native auto-typing functionality (Auto-Type) is fully restricted by the operating system security architecture at the kernel level (applications are prohibited from injecting simulated keystrokes into foreign windows). By rejecting vulnerable browser plugins entirely, data is safely transferred using the clipboard mechanism protected by the `xclip` utility.

**1.** Configure fast copying: navigate to **Tools** ➔ **Settings** ➔ **General** tab in the main menu. Under the **Entry Management** section, check **Copy data on double clicking field in entry view** and click **OK**.

**2.** Perform credential insertion: open the target site in Firefox, switch to the KeePassXC window, and simply **double-click** the desired password entry.

**3.** The application copies the secret to the clipboard immediately, automatically minimizes to the system tray, and returns focus to the browser window. Press **"Ctrl + V"** inside the site input field to complete the operation.

> [!NOTE]
> Leveraging the previously installed `xclip` system utility, the copied passphrase remains in clipboard memory for strictly **5–10 seconds** (matching the timeout defined in the Security tab). Following this window, host runtime memory reserved for the clipboard is purged completely, neutralizing credential interception risks from hidden stealer scripts.

**Chapter Assets:** *_assets\images\12_keepassxc*

<br>

## Installing and Running the Wireshark Network Analyzer

#### Introduction:

Deep auditing, logging, and real-time network packet analysis are conducted using Wireshark. It allows full inspection of network packet payloads across all layers of the communication stack. It is an extremely powerful tool, and providing a detailed overview of its full feature set and analysis methodologies would require an entire textbook. Within the scope of this deployment guide, analysis focuses on inspecting active connections through its accessible graphical interface. Through the GUI, operators can visually audit exactly which IP addresses and ports are utilized to transmit and receive host traffic. Any suspicious, undocumented, or non-recommended IP destinations should be immediately added to firewall blacklists. Advanced instructions and packet dissection examples are available in specialized technical documentation on verified IT resources, such as `varonis.com`, `sans.org`, or the official reference community `ask.wireshark.org`.

#### Installing and Launching Wireshark:

> [!WARNING]
> **Warning!** Before proceeding, ensure that you have exited the persistent superuser shell (using the `exit` command) and that the standard `$` prompt is displayed in the terminal. The installation must be executed exclusively as an unprivileged user.

**1.** Launch the network analyzer installation:
```bash
sudo apt install wireshark -y
```

During package deployment, the APT package manager displays an interactive terminal dialog raising a critical prompt: *“Should non-superusers be able to capture packets?”* Use the keyboard arrow keys to explicitly select **“Yes”**.

**2.** Append the current user account to the `wireshark` system group:
```bash
sudo usermod -aG wireshark $USER
```

**3.** Applying new group membership without terminating the active user session requires the `newgrp` utility. On Ubuntu 26.04, this binary is provided by the `util-linux-extra` package; install it via:
```bash
sudo apt install util-linux-extra
```

To apply updated group privileges instantly without rebooting the system or restarting the active desktop session, run the group initialization command:

**4.** Refresh group access privileges for the active terminal window:
```bash
newgrp wireshark
```

> [!NOTE]
> **Author's Note:** The `newgrp` command updates access privileges exclusively within the active terminal window. Across newly spawned shell instances, privilege updates take effect automatically only after a full system reboot.

**5.** Launch the analyzer graphical interface under the unprivileged user account:
```bash
wireshark
```

#### Critical Security Concept: Packet Capture Subsystem Security:

The operational rationale for adding the user account to the system `wireshark` group is to completely eliminate running Wireshark via `sudo`. This analytical suite comprises millions of lines of complex C/C++ code, featuring dissectors for hundreds of network protocols. Historically, critical vulnerabilities—including Remote Code Execution (RCE)—are regularly discovered within these dissectors. If the GUI is launched with root privileges, any maliciously crafted packet arriving at the network interface from an external network could instantly execute arbitrary code with maximum system privileges. Running the application strictly as an unprivileged user via an isolated dedicated group is a fundamental global security standard.

#### Stealth Traffic Capture (Headless Console Mode):

If you need to rapidly capture a network activity log without launching a heavy graphical interface (for instance, to avoid exposing monitoring activity to nearby eyes or to conserve system memory resources), leverage the command-line counterpart:

**1.** Install `tshark`, the CLI utility for packet capture and deep network traffic analysis:
```bash
sudo apt install tshark
```

**2.** Initiate silent traffic capture on the secured VPN interface, writing the output directly to a dump file (replace the network interface name if your setup differs or if a VPN is not active):
```bash
tshark -i tun0 -w ~/Downloads/dump.pcap
```

This command silently captures all network traffic passing through the secured `tun0` interface and writes it to the `dump.pcap` file located within the user's Downloads directory. The resulting packet capture file can subsequently be opened and thoroughly dissected inside the Wireshark GUI at any time.

#### Practical Wireshark Field Guide:

Following Wireshark installation, avoid attempting to analyze every packet field immediately. At this initial stage, it suffices to grasp the overall structure of network exchanges and learn to isolate events of interest.

After launching the application, select the active network interface carrying host traffic and initiate packet capture. On a physical system, this typically corresponds to an Ethernet or Wi-Fi interface; when running a VPN, a virtual interface such as `tun0` will additionally appear.

Once capture begins, the packet list pane populates in the upper section of the interface. Each row represents a discrete packet, with primary columns providing immediate context on its origin and destination:

* **No.** — The sequential packet number within the current capture session.
* **Time** — The packet arrival timestamp relative to the start of the recording.
* **Source** — The originating network address of the packet.
* **Destination** — The target network address of the packet.
* **Protocol** — The highest-layer protocol decoded by Wireshark.
* **Length** — The frame payload size in bytes.
* **Info** — A concise summary of packet contents or control flags.

For instance, a single packet row may present as follows:  
*70   40.244944613   192.168.1.119   104.18.32.47   TCP   54 56042 → 443 [ACK] Seq=19884 Ack=1062 Win=802 Len=0*

Deconstructing this entry by field:

* **70** — Sequential packet identifier in the active capture buffer.
* **40.244944613** — Elapsed time in seconds since capture initiation.
* **192.168.1.119** — Source IP address (the local host interface).
* **104.18.32.47** — Destination IP address (the remote endpoint).
* **TCP** — The active Transport Layer protocol.
* **54** — Total frame length in bytes.
* **56042 → 443** — Source and destination TCP ports. Port 56042 represents an ephemeral port allocated by the local OS, while 443 targets standard HTTPS service.
* **[ACK]** — Control packet acknowledging data receipt. This frame carries no upper-layer payload; its sole purpose is confirming previously received segments.
* **Seq=19884** — The TCP sequence number assigned to this segment.
* **Ack=1062** — The next expected byte sequence number from the remote host.
* **Win=802** — The currently advertised TCP receive window size.
* **Len=0** — Zero TCP segment payload length. This represents pure transport control signaling rather than application data transmission.

**Dissecting Individual Packets**

Selecting a packet reveals its encapsulated internal layer structure in the packet details pane, displayed by Wireshark as nested protocol layers.

A standard TCP/IP packet typically exhibits the following hierarchy:

* Frame
* Ethernet II
* Internet Protocol Version 4
* Transmission Control Protocol
* Application Protocol

Each layer encapsulates specific metadata required for protocol stack processing:

* **Frame** — Capture-level metadata: packet index, arrival timestamp, frame length, and interface details.
* **Ethernet II** — Data Link Layer attributes, containing source and destination MAC hardware addresses.
* **Internet Protocol Version 4 (IPv4)** — Network Layer headers, detailing source/destination IP addresses, Time To Live (TTL) values, and fragmentation parameters.
* **Transmission Control Protocol (TCP)** — Transport Layer headers, exposing port pairs, sequence/acknowledgment numbers, and control flags.

When inspecting connectionless UDP traffic, the TCP header block is replaced by a corresponding **User Datagram Protocol** layer.

**Understanding Core TCP Control Flags**

When dissecting TCP streams, recognizing primary control flags is essential for state evaluation:

* **SYN** — Initiates the TCP three-way handshake connection sequence.
* **SYN, ACK** — Server acknowledgment response to a connection request.
* **ACK** — Confirms receipt of transmitted data segments.
* **FIN** — Initiates graceful connection teardown.
* **RST** — Abruptly resets or terminates a TCP connection.
* **PSH** — Instructs the receiving stack to push buffered data immediately to the application layer.

Note that isolated `RST` packets or retransmissions should not automatically be classified as malicious activity. Operating system network stacks routinely encounter transient packet loss, socket timeouts, and normal tear-downs.

**Correlating IP Addresses and Port Pairs**

Analyzing active sockets requires correlating IP destinations with assigned service ports:  
*192.168.1.15:41832 → 9.9.9.9:53* indicates a local process binding ephemeral outbound port `41832` to query remote DNS service on UDP port `53`.  
Similarly: *192.168.1.15:52314 → 142.250.x.x:443* denotes an outbound TCP connection to a remote server over HTTPS port `443`.

A port assignment alone does not strictly dictate protocol compliance; it functions as a default transport convention between communicating endpoints.

**Auditing DNS Traffic**

DNS queries provide an ideal baseline for initial connection analysis. Applying the **dns** display filter isolates packets recognized as Domain Name System traffic. This exposes outbound resolution attempts, such as: *Standard query A example.com*, followed by its response: *Standard query response A 93.184.216.34*. This grants full visibility into domain names requested by local binaries. To isolate specific FQDN lookups, apply targeted filters: **dns.qry.name == "example.com"**. This approach is particularly effective when auditing newly installed software: launch the application, inspect generated DNS requests, and verify them against expected baseline behavior.

**Traffic Filtering Mechanics**

Wireshark leverages display filters to rapidly isolate relevant streams from raw capture data:

* **ip.addr == 9.9.9.9** — Filters all frames involving the specified IP address as source or destination.
* **ip.src == 192.168.1.15** — Restricts output strictly to frames originating from the specified source host.
* **tcp.port == 443** — Isolates TCP traffic bound to or from port `443`.
* **udp.port == 53** — Isolates UDP traffic bound to or from port `53`.

Combine conditions using logical operators to target specific sockets: **ip.addr == 192.168.1.15 && tcp.port == 443**. Utilizing display filters enables progressive narrowing from full packet captures down to specific communication streams.

> [!TIP]
> Do not attempt to memorize complex filter syntax immediately. Mastering a core set of primary filter primitives—`ip.addr`, `ip.src`, `ip.dst`, `tcp.port`, `udp.port`, and `dns.qry.name`—provides sufficient operational capability for standard traffic auditing.

**Inspecting Encrypted HTTPS Traffic**

When analyzing HTTPS sessions, Wireshark exposes connection establishment parameters—including remote endpoint IP addresses, destination ports, and TLS handshake exchanges—while the HTTP application payload remains fully encrypted.

Typical capture sequences display protocol events such as: *TCP*, *TLS Client Hello*, *TLS Server Hello*, and *TLS Application Data*.

The presence of *TLS Application Data* frames does not enable plain-text payload inspection by Wireshark. Without session key export files or explicit decryption credentials, TLS payloads remain cryptographically secured. Keep this operational distinction in mind during analysis: **Wireshark exposes network exchange patterns, but cannot decrypt payload contents by default.**

**Practical Verification Exercise**

To establish basic operational proficiency with the analyzer, execute this standard verification workflow:

**1.** Initiate packet capture on the active network interface.
**2.** Launch the browser.
**3.** Navigate to a known domain.
**4.** Allow traffic to generate for a few seconds, then stop the capture.
**5.** Apply the display filter: **dns**
**6.** Audit the resolved domain names for unexpected external requests.
**7.** Clear the filter and apply: **tcp.port == 443**
**8.** Inspect the resulting HTTPS connection streams established during the browsing session.

Select individual frames and expand protocol headers to observe how high-level user actions traverse the encapsulated network stack layers.

> [!IMPORTANT]
> Wireshark does not classify traffic as benign or malicious automatically. It captures raw network events and provides the analytical framework to dissect them. Determining whether a connection is legitimate, unwanted, or suspicious requires analyst evaluation based on threat modeling and expected software behavior.

This baseline covers the essential scope required for host auditing: operators must be capable of independently capturing network connections, identifying endpoints, evaluating transport protocols and port pairs, and leveraging these primitives to verify hardened host configurations.

**Chapter Assets:** *_assets\images\13_wireshark*

<br>

## Installing and Managing the AppArmor Security System

#### Introduction:

Mandatory Access Control (MAC) over the file system is enforced via the native AppArmor subsystem. It restricts hardware access, file permissions, and network sockets on a per-application basis. Operating as a low-level Linux Security Module (LSM), AppArmor strictly confines running processes to an explicitly defined set of capabilities (a profile).

Consider a practical deployment scenario. A PDF viewer can be completely isolated by revoking all network socket access and denying read privileges to sensitive user directories.

Under this model, the host perimeter remains secure. Even if an adversary triggers a zero-day exploit via a maliciously crafted document, the executed payload remains physically incapable of reading confidential directories or exfiltrating stolen assets to a remote command-and-control server.

#### A New Security Paradigm: Kernel Automation:

Within Ubuntu 24.04 and 26.04 LTS, the AppArmor subsystem has transitioned to deep, automated kernel-level integration. In legacy distributions, system administrators were required to manually deliver profile databases and enforce strict containment on critical utilities via `aa-enforce` invocations.

Modern Ubuntu builds eliminate legacy text-based profile templates (such as `usr.sbin.resolved`, `usr.sbin.NetworkManager`, or `usr.bin.dumpcap`) from the default base image. Host defenses have shifted to lower-level architectural primitives:

* **1. System Daemons (`NetworkManager`, `resolved`):** The Linux kernel isolates these core services out of the box using native `systemd` sandboxing primitives and isolated Linux namespaces.
* **2. Network Utilities (`dumpcap`/Wireshark):** Explicitly selecting **`<Yes>`** during the interactive Wireshark package deployment prompts the Linux kernel to assign granular capabilities (**`CAP_NET_RAW`** and **`CAP_NET_ADMIN`**) directly to the `/usr/bin/dumpcap` binary via the Linux Capabilities framework.

> [!NOTE]
> **Author's Threat Analysis:** The Linux Capabilities mechanism permits the `dumpcap` capture utility to legitimately intercept raw traffic across all system interfaces while running strictly within the unprivileged user context. The process no longer requires elevated `root` privileges, ensuring that a malicious payload embedded in a captured frame remains physically incapable of compromising the underlying operating system. Attempting to manually apply an AppArmor profile to `dumpcap` via `aa-enforce` will return a `Profile not found` error.

Our primary strategic objective is enforcing complete isolation over complex user space software (browsers, media players, document viewers), where threat vectors involving malicious external files are highest. This defensive perimeter is fully addressed in the dedicated sandboxing chapter.

#### Practical Hardening of the AppArmor Subsystem:

To configure audit utilities for deep system analysis, open a terminal session and execute the following steps in order:

**1.** Install the official extended security profiles database alongside administrative utilities:
```bash
sudo apt install apparmor-utils apparmor-profiles -y
```

**2.** Query the active AppArmor state to inspect loaded profiles and confined process lists:
```bash
sudo aa-status
```

**3.** Force-enable automatic initialization of the security service during early kernel boot:
```bash
sudo systemctl enable apparmor
```

**4.** Launch the host security log audit tool (for `fusermount3`: select **[D]eny** 3 times, then **[F]inish**, then **[S]ave**; for `systemd-detect-virt`: select **[A]llow**, then **[F]inish**, then **[S]ave**):
```bash
sudo aa-logprof
```

> [!IMPORTANT]
> On Ubuntu 24.04 distributions, running `aa-logprof` may terminate abruptly with a duplicate profile error:  
> `ERROR: Conflicting profiles for firefox defined in two files...`
> 
> This occurs due to a policy conflict between legacy Canonical text profiles and updated kernel rules. To restore full audit parser functionality, isolate the conflicting duplicate profile into a backup directory using a single command:
> ```bash
> sudo mkdir -p /etc/apparmor.d/backup_conflict/ && sudo mv /etc/apparmor.d/firefox /etc/apparmor.d/backup_conflict/ 2>/dev/null || true
> ```
> 
> Once isolated, re-run `sudo aa-logprof`. The log parser will parse system events cleanly:  
> `Profile: ubuntu_pro_esm_cache_systemd_detect_virt`  
> `Capability: perfmon`
> 
> The interactive utility will then present all blocked calls, allowing operators to grant legitimate capabilities or enforce denials with a single keypress. Full isolation and conflict-free execution of the Firefox browser will be addressed in the subsequent Firejail deployment chapter.

<br>

## Installing and Configuring the Firejail Isolated Sandbox

#### Introduction:

To safely execute untrusted external files and binaries, we deploy the Firejail sandboxing framework. Firejail isolates web browsers, productivity software, and communication clients by constraining their access to the host file system, system calls (seccomp filters), networking stacks, and hardware resources according to predefined security profiles.

Firejail is a lightweight Linux security sandbox that leverages namespaces, cgroups, and Linux Capabilities to run applications inside strictly confined environments.

In this chapter, we will install Firejail, launch previously installed applications (Firefox, KeePassXC, Document Viewer, and Image Viewer) within isolated sandboxes, and proceed to install and confine LibreOffice, GIMP, VSCodium, LM Studio, Telegram, Psi+, and Thunderbird. Furthermore, Psi+ and Thunderbird will be configured to handle OpenPGP (GnuPG) end-to-end encryption. Finally, we will generate custom desktop launchers (`.desktop` entries) to enforce transparent sandbox confinement across all desktop shortcuts.

#### Installing Firejail and Preparing the Sandbox:

**1.** Retrieve the current stable build of Firejail from the project's official repository. First, install the requisite dependency utilities, then automatically resolve the latest available `.deb` release asset and deploy it:
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

**2.** Verify the installed Firejail version. Ensure the output contains the `AppArmor support is enabled` flag, confirming that Firejail integrates with the AppArmor security subsystem:
```bash
/usr/bin/firejail --version
```

> [!IMPORTANT]
> Starting with Ubuntu 24.04 LTS, AppArmor introduces restrictions on unprivileged user namespace creation (`unprivileged_userns`). This is an intentional Linux kernel security feature designed to reduce kernel attack surface, rather than an error or system bug.
> 
> Rather than disabling global system protections or manually altering vendor AppArmor profiles, we query system state first and leverage native Firejail-AppArmor integration mechanisms.
> 
> A fundamental security principle applies: the sandbox container must harden system posture without devolving into an unmaintainable series of manual policy overrides that introduce new threat vectors.

**3.** Query the active unprivileged user namespace restriction status:
```bash
sysctl kernel.apparmor_restrict_unprivileged_userns
```
If the terminal outputs:
```bash
kernel.apparmor_restrict_unprivileged_userns = 1
```

This confirms that enhanced AppArmor kernel restriction remains active. We maintain this baseline configuration enabled.

#### CCore Firejail Filtering Options (Reference):

* **`--apparmor`** — Enforces an AppArmor security profile for secondary kernel-level application containment. Firejail constructs the isolated namespace while AppArmor applies mandatory access control (MAC) policies.
* **`--blacklist`** — Explicitly hides targeted files or directories from the containerized application.
* **`--caps.drop=all`** — Drops all Linux capability flags, eliminating access to privileged kernel operations.
* **`--deterministic-shutdown`** — Guarantees clean sandbox teardown alongside all child processes upon main binary termination.
* **`--dbus-user=none`** — Disables access to the user-session D-Bus bus. Enforces strict isolation for binaries that do not require IPC with the desktop environment.
* **`--dbus-system=none`** — Disables access to the system D-Bus bus.
* **`--net=none`** — Completely unbinds the host networking stack from the container, exposing only the local loopback interface (`127.0.0.1`).
* **`--nonewprivs`** — Sets the `PR_SET_NO_NEW_PRIVS` flag to hardware-prevent process privilege escalation inside the sandbox, neutralizing setuid/setgid execution paths.
* **`--no-sandbox`** — Disables the native Chromium/Electron user-space sandbox engine to avoid nesting conflicts when running under external sandboxing frameworks (such as Firejail).
* **`--private`** — Mounts volatile temporary file systems (`tmpfs` in RAM) over real user home directories, presenting a clean ephemeral state.
* **`--private-dev`** — Constructs a minimal, hardened virtual `/dev` device node directory inside the sandbox.
* **`--private-etc`** — Supplies an isolated, minimal view of the `/etc` configuration directory containing only essential system files.
* **`--private-tmp`** — Completely isolates the temporary system directory `/tmp` from the host environment.
* **`--protocol`** — Restricts process access to specific socket domains and network protocol families inside the sandbox environment.
* **`--seccomp`** — Enables Linux kernel Secure Computing (seccomp) filtering to intercept and block high-risk or non-standard system calls. Any policy violation triggers immediate kernel process termination.
* **`--whitelist`** — Grants explicit read/write access exclusively to targeted files or directories, implicitly denying access to all non-whitelisted paths.

#### Creating a Dedicated Hardened Firefox Profile:

Following the installation of Firejail, proceed to configure a dedicated, hardened Firefox security profile.

By default, Firejail includes a preconfigured Firefox profile. Rather than modifying the system-wide `/etc/firejail/firefox.profile` binary configuration directly, construct a custom user-space profile copy. This strategy maintains default Firejail security baseline rules while allowing custom policy additions that persist across package upgrades.

**1.** Create the local user-space Firejail profile directory and duplicate the stock Firefox profile:
```bash
mkdir -p ~/.config/firejail && cp /etc/firejail/firefox.profile ~/.config/firejail/firefox-hardened.profile
```

**2.** Open the newly created profile for inspection and customization:
```bash
nano ~/.config/firejail/firefox-hardened.profile
```

**3.** Replace the `include firefox.local` directive with the path to our custom local configuration file `firefox-hardened.local`:
```ini
include firefox-hardened.local
```

This retains the internal structure of the upstream Firejail profile. Rewriting the entire profile from scratch is unnecessary, as upstream maintainers have already defined essential containment primitives:

* Seccomp system call filtering;
* Linux Capability drops;
* File system access restrictions;
* D-Bus IPC filtering;
* Essential hardening include files.

Custom policy directives will reside separately within the dedicated local include file.

**4.** Create the local override configuration file for the hardened Firefox profile:
```bash
nano ~/.config/firejail/firefox-hardened.local
```

**5.** Append only essential access permissions required by the hardened Firefox configuration:
```ini
# Custom rules for hardened Firefox

# Permit FIDO2/U2F hardware token access (YubiKey and compatible devices)
ignore nou2f

# Grant exclusive access to the isolated Firefox profile directory
noblacklist ${HOME}/.mozilla-hardened
whitelist ${HOME}/.mozilla-hardened

# Permit file downloads to the standard Downloads directory
whitelist ${HOME}/Downloads

# Enforce clean sandbox teardown upon primary process exit
deterministic-shutdown
```
To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit the editor.

Firejail now references a dedicated user-level Firefox profile that operates independently of system-wide defaults and remains protected against package update overrides.

Avoid interacting directly with the default user profile directory (`~/.mozilla`). Instead, establish an isolated directory structure at `~/.mozilla-hardened` to house the active Firefox environment exclusively. Decoupling browser runtime data from default user home directories yields a clean, auditable profile layout easily managed within sandbox boundaries.

**6.** Create the dedicated hardened directory structure and copy the active Firefox profile:
```bash
mkdir -p ~/.mozilla-hardened && cp -r ~/.config/mozilla/firefox ~/.mozilla-hardened/ 2>/dev/null || true
```

**7.** Inspect the contents of the newly populated profile directory:
```bash
ls -la ~/.mozilla-hardened/firefox/
```
The output must display the active profile directory matching the standard release naming convention: `PROFILE-NAME.default-release`.

**8.** Create a persistent `current` symbolic link pointing directly to the active profile directory:
```bash
cd ~/.mozilla-hardened/firefox/ && rm -f current && ln -s PROFILE-NAME.default-release current && cd ~
```

**9.** Validate that the symbolic link resolves correctly to the target profile directory:
```bash
readlink -f ~/.mozilla-hardened/firefox/current
```

If the invocation outputs the absolute path to the target profile directory, the symbolic link is configured correctly.

**10.** Enforce user ownership across the isolated profile directory tree:
```bash
chown -R $USER:$USER "$HOME/.mozilla-hardened"
```

The Firefox profile is now prepared for execution inside an isolated Firejail container perimeter. Avoid injecting excessive manual overrides that risk compromising core sandbox mechanics. Testing across various launch parameters confirms that runtime edge cases stem from process initialization flags rather than flaws within Firejail or AppArmor primitives.

The verified operational baseline comprises:

* Standard Firejail security profile rules;
* Decoupled Firefox profile configuration;
* Isolated `~/.mozilla-hardened` file system container;
* Reliable sandbox teardown via `--deterministic-shutdown`.

**11.** Launch Firefox inside the hardened Firejail container:
```bash
firejail --profile=firefox-hardened /usr/bin/firefox --no-remote --profile "$HOME/.mozilla-hardened/firefox/current"
```

**12.** Open a secondary terminal window to audit active sandbox container instances:
```bash
firejail --list
```

The output must list the active Firefox container instance: `PID:user::firejail --deterministic-shutdown --profile=firefox-hardened /usr/...`.

Verify container lifecycle behavior: terminate the Firefox browser window normally and wait several seconds.

**13.** Query the active sandbox list to verify process termination:
```bash
firejail --list
```

If configured correctly, the active sandbox list returns empty. This confirms that Firejail successfully trapped the primary process exit signal, terminated child threads cleanly, and completely destroyed the ephemeral execution namespace.

Firefox executes with all predefined user preferences, security extensions, and `user.js` hardening flags active while benefiting from strict OS-level container isolation. Upon browser exit, the sandbox container is destroyed entirely, returning host OS state to its pristine baseline.

> [!NOTE]
> Under certain launch configurations, orphan sandbox processes could previously remain resident in memory after closing the browser interface. This behavior resulted from process tree termination dynamics inside the PID namespace rather than profile corruption or AppArmor policy failures.
> 
> Supplying the `deterministic-shutdown` directive resolves this lifecycle condition: Firejail strictly monitors child process execution trees, guaranteeing immediate sandbox teardown upon main browser interface closure.

Later in this section, we will lock down persistent application launches via customized .desktop shortcut configurations.

#### Airtight PDF Vault: Safely Opening Files in an Isolated Offline Mode:

Because document viewers (such as PDF and DjVu parsers) are routinely targeted by exploits leveraging zero-day parsing vulnerabilities, isolating them from the underlying OS host and networking stack is critical. We will construct a strictly air-gapped container environment for Evince/Papers—an isolated sandbox with all outbound and inbound network capabilities completely severed.

Before launching the command, ensure a sample PDF document is present in the standard user directory. For this exercise, assume a target file named `unsafe.pdf` is located inside the user's `Downloads` directory.

**1.** If no sample PDF is available, generate a dummy placeholder file to perform sandbox verification:
```bash
touch ~/Downloads/unsafe.pdf
```

* **For Ubuntu 24.04 LTS Noble Numbat (Users running Evince):**

**2a.** Launch the default Evince document viewer inside the standard Firejail sandbox:
```bash
firejail evince ~/Downloads/unsafe.pdf
```

**3a.** Without closing the active document viewer window, open a secondary terminal tab and execute the sandbox auditing command to list active isolated containers:
```bash
firejail --list
```

**4a.** Apply hardened containment policies to Evince by creating a dedicated local configuration override `evince.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/evince.local
```

**5a.** Insert the following security directives into the `evince.local` configuration block:
```ini
# Enforce absolute network isolation
net none
protocol unix

# Drop all Linux capabilities and prevent privilege escalation
caps.drop all
nonewprivs

# Isolate temporary files and cache locations
private-cache
private-tmp

# Expose only necessary directories inside a volatile private HOME workspace
private-home Downloads,Documents
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to return to the shell prompt.

**6a.** Perform a verification launch of Evince under the newly hardened profile:
```bash
firejail evince ~/Downloads/unsafe.pdf
```

* **For Ubuntu 26.04 LTS Resolute Raccoon (Users running Papers):**

**2b.** Launch the Papers document viewer inside the standard Firejail sandbox:
```bash
firejail papers ~/Downloads/unsafe.pdf
```

**3b.** Without closing the active document viewer window, open a secondary terminal tab and inspect active isolated container instances:
```bash
firejail --list
```

**4b.** Apply hardened containment policies to Papers by creating a local configuration override `papers.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/papers.local
```

**5b.** Insert the following security directives into the `papers.local` configuration block:
```ini
# Enforce absolute network isolation
net none
protocol unix

# Drop all Linux capabilities and prevent privilege escalation
caps.drop all
nonewprivs

# Isolate temporary files and cache locations
private-cache
private-tmp

# Expose only necessary directories inside a volatile private HOME workspace
private-home Downloads,Documents
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit the editor.

**6b.** Perform a verification launch of Papers under the newly hardened profile:
```bash
firejail papers ~/Downloads/unsafe.pdf
```

* Later in this chapter, permanent sandbox launch directives will be embedded directly into system desktop launchers (`.desktop` files) to ensure transparent, default sandbox enforcement.

#### Sandboxing Image Viewer for Secure Media Inspection:

**1.** If no sample PNG file is available, create a dummy placeholder file to perform sandbox verification:
```bash
touch ~/Pictures/unsafe.png
```

* **For Ubuntu 24.04 LTS Noble Numbat (Users running Eog):**

**2a.** Launch the default Eye of GNOME (Eog) image viewer inside the standard Firejail sandbox:
```bash
firejail eog ~/Pictures/unsafe.png
```

**3a.** Without closing the active image viewer window, open a secondary terminal tab and execute the sandbox auditing command to list active isolated containers:
```bash
firejail --list
```

**4a.** Apply hardened containment policies to Image Viewer by creating a dedicated local configuration override `eog.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/eog.local
```

**5a.** Insert the following security directives into the `eog.local` configuration block:
```ini
# Enforce absolute network isolation and shell restrictions
net none
protocol unix
caps.drop all
nonewprivs
private-cache
private-tmp
```

**6a.** Perform a verification launch of the application under the newly hardened profile:
```bash
firejail eog ~/Pictures/unsafe.png
```

* **For Ubuntu 26.04 LTS Resolute Raccoon (Users running Loupe):**

**2b.** Launch the Loupe image viewer inside the standard Firejail sandbox:
```bash
firejail loupe ~/Pictures/unsafe.png
```

**3b.** Without closing the active image viewer window, open a secondary terminal tab and inspect active isolated container instances:
```bash
firejail --list
```

**4b.** Apply hardened containment policies to Image Viewer by creating a local configuration override `loupe.local`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/loupe.local
```

**5b.** Insert the following security directives into the `loupe.local` configuration block:
```ini
# Enforce absolute network isolation and shell restrictions
net none
protocol unix
caps.drop all
nonewprivs
private-cache
private-tmp
```

**6b.** Perform a verification launch of the application under the newly hardened profile:
```bash
firejail loupe ~/Pictures/unsafe.png
```

* Later in this chapter, permanent sandbox launch directives will be embedded directly into custom user-space `.desktop` launchers to ensure transparent, default sandbox enforcement.

#### KeePassXC Sandboxing Scenario:

Isolating KeePassXC converts it from an ordinary application executing in a shared desktop context into an autonomous vault. It communicates with the host exclusively via Unix domain sockets (to interface with our YubiKey hardware) and maintains access solely to a single, targeted file—our password database. The rest of the host file system is completely masked.

Kernel-level filters embedded within the Firejail profile (`seccomp`, `caps.drop all`, and `ptrace` anti-debugging rules) strictly prohibit external processes from inspecting KeePassXC process memory or reading its memory address space.

**1.** Create the local Firejail configuration directory (if not already present) and open the password manager's profile override file:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/keepassxc.local
```

**2.** Insert the verified override configuration block. This unsets restrictive device blacklists, restores USB token access permissions, enables the `netlink` socket domain for YubiKey Challenge-Response hardware token discovery, and confines the user's home directory—exposing exclusively configuration files and target password databases:
```ini
# Permit FIDO2/U2F hardware token operations (YubiKey and compatible devices)
ignore private-dev
ignore protocol unix
ignore nou2f

# Retain host user group access permissions
ignore groups
ignore nogroups

# Re-enable GTK glycin-loader binary access
noblacklist /usr/libexec
whitelist /usr/libexec/glycin-loaders

# Permit access to KeePassXC application configuration
noblacklist ${HOME}/.config/keepassxc
nowhitelist ${HOME}/.config/keepassxc
whitelist ${HOME}/.config/keepassxc

# CRITICAL: Grant access to target password database and keyfile.
# Specify your actual absolute file paths.
# KeePassXC Database:
# noblacklist ${HOME}/Documents/passwords.kdbx
# whitelist ${HOME}/Documents/passwords.kdbx

# Keyfile located on external encrypted storage:
# noblacklist /media/$USER/DRIVE-NAME/passwords.key
# whitelist /media/$USER/DRIVE-NAME/passwords.key
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to return to the terminal prompt.

**3.** Launch KeePassXC inside the Firejail sandbox container:
```bash
firejail keepassxc
```

> [!IMPORTANT]
> Unconditionally disabling D-Bus IPC may maximize container isolation; however, on modern Linux environments utilizing Wayland, it frequently induces execution failures across graphical desktop applications. Modern GUI software relies on the user D-Bus session bus and XDG Desktop Portals to securely interface with the desktop environment.
>
> If an application fails to launch following complete D-Bus disabling, enforce filtered Inter-Process Communication (IPC) instead:
>
> ```bash
> --dbus-user=filter
> ```
>
> This filtering mode maintains granular IPC control: it blocks unauthorized bus calls while preserving necessary system interfaces required for modern graphical applications to function.

> [!NOTE]
> The `firecfg` helper utility generates symlinks exclusively for legacy binaries installed via native `.deb` packages or compiled from source. As established in the initial chapters of this manual, Canonical's telemetry-heavy Snap infrastructure has been completely purged from our hardened OPSEC environment. Firejail operates at peak mandatory access control efficiency within this pristine configuration: standard system binaries deployed via `apt` and standalone, self-contained AppImage bundles.

* Near the end of this chapter, we will bind these security parameters directly to system desktop files for seamless execution.

#### Installing and Sandboxing the LibreOffice Suite:

Office documents represent one of the most common vectors for organizational data exchange. However, the sheer complexity of modern formats (DOCX, XLSX, ODT) makes office suites full-fledged external data processors. Consequently, running LibreOffice inside an isolated Firejail environment is strongly recommended—especially when handling documents obtained from external sources.

**1.** Install LibreOffice:
```bash
sudo apt install libreoffice -y
```

**2.** Open the `libreoffice.profile` configuration file in the `nano` editor:
```bash
nano ~/.config/firejail/libreoffice.profile
```

**3.** Define explicit mandatory restrictions within the file:
```ini               
# Force GTK3 VCL plugin
env SAL_USE_VCLPLUGIN=gtk3
# File system isolation
private-tmp
private-dev

# Restrict file system access exclusively to these directories
whitelist ${HOME}/Documents
whitelist ${HOME}/Downloads
whitelist ${HOME}/.config/libreoffice

# Enforce absolute network socket restriction
protocol unix
ignore protocol inet
ignore protocol inet6

blacklist /tmp/.X11-unix
blacklist ${HOME}/.Xauthority

# Disable D-Bus and extraneous services
nosound

# Advanced security hardening
caps.drop all
nonewprivs
noroot
seccomp

blacklist ${HOME}/.ssh
blacklist ${HOME}/.gnupg
blacklist ${HOME}/.mozilla

# Removable media storage
blacklist /media
blacklist /mnt
blacklist /run/media
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to return to the terminal prompt.

**4.** Launch the main LibreOffice Start Center inside the sandbox:
```bash
firejail libreoffice
```

**5.** To launch individual writer/calc/impress/draw/math/base applications, execute:
```bash
firejail libreoffice --writer
firejail libreoffice --calc
firejail libreoffice --impress
firejail libreoffice --draw
firejail libreoffice --math
firejail libreoffice --base
```

* Toward the end of this chapter, we will configure permanent sandboxed execution by embedding launch parameters directly into user .desktop entries.

#### Installing and Sandboxing GNU Image Manipulation Program (GIMP):

Image editors represent some of the most complex desktop user space applications. GIMP processes a vast array of graphics formats (including PSD, TIFF, PNG, JPEG, and SVG) while supporting external third-party plugins. Consequently, memory corruption vulnerabilities within file parsers or extension modules could potentially lead to arbitrary code execution.

To mitigate operational risks when opening visual assets from untrusted sources, construct an isolated container perimeter for GIMP. The application will operate with absolute network isolation, stripped Linux capabilities, and file system access strictly bounded to essential target directories.

**1.** Install GIMP via the package manager:
```bash
sudo apt install gimp -y
```

Assume an untrusted visual asset has been downloaded for inspection at `~/Downloads/unsafe.png`.

**2.** Launch the file inside the default Firejail sandbox:
```bash
firejail gimp ~/Downloads/unsafe.png
```

Note that on Ubuntu 26.04 LTS, prior to applying a custom local profile, automatic process termination for GIMP 3.x may fail to trigger cleanly upon main window exit. Enforce the `deterministic-shutdown` directive within local policy overrides to guarantee complete sandbox teardown.

**3.** Harden security constraints for GIMP by creating a local profile override file:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/gimp.local
```

**4.** Append the following container hardening directives:
```ini
# Enforce complete network stack isolation
net none

# Drop all Linux capabilities
caps.drop all

# Preserve dconf and XDG desktop portal IPC for file selection dialogs
ignore nodbus
ignore dbus-user none
ignore dbus-system none

# Mute audio subsystem initialization to eliminate terminal PulseAudio errors
env PULSE_SERVER=disabled

# Override global blacklists and grant access to configuration profiles
noblacklist ${HOME}/.config/GIMP
whitelist ${HOME}/.config/GIMP

# Restrict file system access exclusively to active workspace directories
whitelist ${HOME}/Documents
whitelist ${HOME}/Downloads
whitelist ${HOME}/Pictures

# Enforce immediate container teardown upon main GUI interface closure
deterministic-shutdown
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to return to the terminal prompt.

**5.** Perform a verification launch of the application:
```bash
firejail gimp ~/Downloads/unsafe.psd
```

Unlike static document viewers, full home directory masking via `--private` is omitted for GIMP, as the editor requires persistent access to user brushes, custom plugins, installed system fonts, and application profile configurations.

* Near the end of this chapter, we will bind these security parameters directly to system desktop files for seamless execution.

#### Installing and Sandboxing VS Codium (Development IDE):

VSCodium is a free-software fork of Microsoft’s Visual Studio Code (VS Code) featuring completely purged telemetry, tracking scripts, and proprietary licensing. It provides a clean development environment built with respect for user privacy. However, as with any complex IDE, it requires broad host file system access and spawns numerous child processes; strictly containing it within a hardened sandbox is therefore essential.

**1.** Install requisite system dependencies, navigate to the downloads directory, and fetch the latest stable VSCodium AppImage container from the official repository:
```bash
sudo apt install curl jq -y && cd ~/Downloads && API_HOST="api.github.com" && LATEST_URL=$(curl -s "https://${API_HOST}/repos/VSCodium/vscodium/releases/latest" | jq -r '.assets[].browser_download_url' | grep -E 'x86_64.*\.AppImage$' | head -n 1) && curl -L -o VSCodium.AppImage "$LATEST_URL"
```

**2.** Mark the downloaded binary executable, extract the AppImage payload, deploy the extracted tree to `/opt/vscodium`, and initialize hidden user-space configuration directories:
```bash
chmod +x VSCodium.AppImage && ./VSCodium.AppImage --appimage-extract && sudo mv squashfs-root /opt/vscodium && rm VSCodium.AppImage && mkdir -p ~/.config/VSCodium ~/.vscode-oss/extensions && mkdir -p ~/.vscode-oss-shared
```

**3.** Enforce baseline setuid permissions for the internal Chromium sandbox binary, and recursively restore current user ownership across all hidden configuration paths via the `$USER` variable to eliminate potential *EACCES: permission denied* runtime faults:
```bash
sudo chown root:root /opt/vscodium/usr/share/codium/chrome-sandbox && sudo chmod u+s /opt/vscodium/usr/share/codium/chrome-sandbox && sudo chown -R $USER:$USER ~/.config/VSCodium ~/.vscode-oss ~/.vscode-oss-shared
```

**4.** Create the Firejail configuration directory if not already present, and open the custom profile in `nano`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/vscodium.profile
```

**5.** Define baseline sandbox isolation rules. Explicitly whitelist the `extensions` subfolder (otherwise the extension marketplace defaults to *Read-Only* mode), and include the `runuser` and `var` profile rules to prevent internal Node.js language server initialization crashes:
```ini
# Baseline security
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

# Permit access exclusively to configuration paths, extension modules, and shared memory databases
whitelist ~/.config/VSCodium
whitelist ~/.vscode-oss
whitelist ~/.vscode-oss/extensions
whitelist ~/.vscode-oss-shared

# Permit execution of internal Node.js language servers required by extension engines
include whitelist-runuser-common.inc
include whitelist-var-common.inc
include whitelist-common.inc

# Rapid container teardown upon application exit (retained for potential Electron lifecycle quirks)
#deterministic-shutdown
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit the editor.

**6.** Construct a dedicated workspace directory for active development projects (workspace folder access will be bound via launcher configurations):
```bash
mkdir -p ~/Documents/VSCodium_Projects
```

**7.** Adjust ownership and enforce restrictive permissions on the parent `Documents` directory:
```bash
sudo chown $USER:$USER "$HOME/Documents" && chmod 700 "$HOME/Documents"
```

**8.** Launch the editor in foreground interactive terminal mode. For complex Electron-based IDEs, this launch invocation serves as the baseline execution standard:
```bash
firejail --profile=~/.config/firejail/vscodium.profile /opt/vscodium/AppRun --no-sandbox
```

> [!NOTE]
> Upon closing the primary graphical interface, background Electron services (such as `fileWatcher`) may hold the sandbox container active, leaving the launching host shell blocked. In production setups, this behavior is completely bypassed by utilizing graphical `.desktop` launchers that execute processes asynchronously.

* Further along in this chapter, we will automate sandbox confinement by creating persistent desktop launchers directly in user-space `.desktop` entries.

#### Installing and Sandboxing LM Studio Bionic Local AI:

Cybersecurity professionals cannot transmit sensitive prompts, proprietary source code snippets, or confidential system logs to cloud AI services due to severe data leakage risks.

Security researchers have demonstrated that malicious threat actors can embed execution payloads within chat templates packed inside GGUF format model files.

We will lock down our local AI assistant inside an air-gapped host container perimeter.

Because current LM Studio builds ship as heavy monolithic AppImage containers (~1 GB) and Firejail's native mount mechanisms in Ubuntu 24.04/26.04 trigger file system mounting conflicts (`Invalid argument`), we apply an explicit pre-extraction strategy.

**1.** Navigate to the downloads directory and fetch the latest stable local AI AppImage container directly from the developers' official storage server via a single command, enforcing strict redirect chaining:
```bash
sudo apt install curl -y && cd ~/Downloads && curl -L -o LM-Studio.AppImage "https://lmstudio.ai/download/latest/linux/x64?format=AppImage"
```

> [!TIP]
> **Author's Tip:** The asset payload measures ~1 GB; wait for the terminal transfer progress indicator to reach 100%. Utilizing this static URL string ensures the command always retrieves the latest neural network build.

**2.** Grant standard execution permissions to the downloaded file and unpack its internal file system structure into a temporary user directory:
```bash
chmod +x LM-Studio.AppImage && ./LM-Studio.AppImage --appimage-extract
```

**3.** Move the extracted graphical interface directory tree from the temporary workspace into a hidden, isolated user profile folder:
```bash
mv squashfs-root ~/.lmstudio_gui
```

**4.** Create the Firejail configuration directory if not already present, and open the custom profile in `nano`:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/lmstudio.profile
```

**5.** Define baseline container isolation rules:
```ini
# Do not isolate /dev — preserve access to host GPU and graphics devices
ignore private-dev

# Permit access to LM Studio model stores and internal configuration data
noblacklist ${HOME}/.lmstudio

# Enforce rapid container teardown upon application exit
deterministic-shutdown
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit the editor.

**6.** At this initial stage, the global network Kill-Switch is held inactive, as the application requires outbound internet access to download model weights. To prevent large language models (LLMs) from defaulting to slow CPU execution fallback, wrap application launch in a universal one-line terminal invocation. The script dynamically checks for active host NVIDIA drivers: if an NVIDIA GPU is detected, access to `/dev/nvidia*` device nodes is preserved; otherwise, execution defaults to host Intel/AMD graphics stacks:
```bash
firejail --profile=lmstudio ~/.lmstudio_gui/lm-studio --no-sandbox
```

> [!NOTE]
> Once required model files are fully downloaded to disk via the built-in Hugging Face browser, close the application interface. Outbound network access for this utility will only be necessary when pulling new LLM weights in the future. All downloaded model weights remain securely stored inside the user home directory path `~/.lmstudio/`. Proceed to final container sealing.

Detailed setup for automated split-profile launching (*Secure Sandbox* without network vs. *Online Downloader* with network) for LM Studio, including deployment of custom high-resolution 512px and 256px icons, is covered **later in this text within the `firecfg` section**. The automated helper script provided there generates integrated shortcuts inside the GNOME Applications menu ("Apps").

**7.** To force-launch the full LM Studio graphical interface inside an air-gapped Linux kernel container (bypassing desktop launchers), execute the following command with the `--net=none` flag, which automatically handles GPU passthrough for NVIDIA or integrated Intel/AMD devices:
```bash
firejail --net=none --profile=lmstudio ~/.lmstudio_gui/lm-studio --no-sandbox
```

**8.** To bypass the heavy graphical interface and execute only the lightweight local AI engine as a background service (Daemon) for CLI or API operations while air-gapping network access, use the corresponding universal invocation string. This ensures the `lms` CLI engine binds directly to NVIDIA tensor cores for rapid inference while maintaining stability across Intel/AMD host configurations:
```bash
firejail --net=none --profile=lmstudio $HOME/.lmstudio/bin/lms daemon up
```

**9.** Remove the downloaded installation image from the `Downloads` directory:
```bash
rm ~/Downloads/LM-Studio.AppImage
```

> [!NOTE]
> **OPSEC Security Analysis:** The local AI assistant is now operational within an isolated sandbox across both graphical (GUI) and daemon (CLI/Daemon) execution modes. The `--net=none` directive completely unbinds Linux kernel network namespaces for the running container. Dynamic device mapping guarantees that CUDA engines interface directly with GPU hardware without degrading host file system isolation controls. Sensitive prompts, internal logs, and proprietary source code fragments are processed strictly inside host RAM and GPU tensor cores, remaining physically air-gapped from external network infrastructure.

* Toward the end of this chapter, we will configure permanent sandboxed execution by embedding these launch parameters directly into custom `.desktop` shortcuts.

#### Securing Communications: Mandatory Isolation of Messengers and Crypto Infrastructure (Author's OPSEC Setup):

For everyday tasks, mainstream users typically opt for **Telegram**. However, across the professional cybersecurity community, the **XMPP (Jabber)** protocol and encrypted email paired with end-to-end **OpenPGP (GnuPG)** encryption remain the gold standards for privacy, decentralization, and absolute digital sovereignty.

> [!NOTE]
> When using secure email services like ProtonMail, remember that end-to-end OpenPGP encryption is built directly into the web interface by default for "Proton-to-Proton" internal communications. However, to achieve complete operational sovereignty (a security model designed to mitigate host-side or provider-level compromise), apply a **cascading encryption strategy**: encrypt the message body using a local offline Curve25519 key pair directly on the host, then transmit the resulting ciphertext via Proton. Under this model, intercepting communications becomes mathematically impossible—even if a third party gains full access to Swiss data centers.

Any communication client continuously processes massive volumes of untrusted external data: HTML email layouts, XML chat streams, asynchronous link previews, avatars, and media files. This creates a critical attack surface for file-parsing exploits (including kernel-level or application buffer overflow vulnerabilities). We will neutralize the risk of 0-day exploit execution and host data exfiltration by isolating every communication tool at the Linux kernel level using the Firejail sandbox.

#### Installing and Sandboxing Telegram Desktop:

The primary security flaw of the default Telegram client on Linux is its unrestricted access to the host home directory, alongside storing cached media, downloaded assets, and session keys in plaintext. Should a malicious stealer script execute on the system, it can effortlessly hijack active messenger sessions.

Let's strictly isolate Telegram: prohibit it from viewing any host files outside its own configuration directory and a single designated download folder, while preserving full traffic visibility for Portmaster's eBPF network filtering lenses.

> [!IMPORTANT]
> Because the Snap package framework has been completely removed from our paranoid OPSEC configuration, and Flatpak builds suffer from subtle D-Bus passthrough issues, we strictly utilize the official, clean static messenger binary. This grants the Firejail sandbox maximum mandatory access control over running processes.

**1.** Navigate to the downloads directory, fetch the official stable messenger archive directly via the official `telegram.org` redirect gateway in a single command, unpack its structure, relocate the clean executable binary to the canonical `/usr/bin/` path, and automatically sweep away temporary archive debris:
```bash
sudo apt install curl -y && cd ~/Downloads && curl -L -o telegram.tar.xz "https://telegram.org/dl/desktop/linux" && tar -xvf telegram.tar.xz && sudo mv Telegram/Telegram /usr/bin/telegram-desktop && rm -rf Telegram/ telegram.tar.xz
```

The `curl -L` directive follows the HTTP redirects of the official download portal, fetches the latest upstream tarball, extracts it, and deploys the static binary to `/usr/bin/telegram-desktop`. This canonical execution path ensures seamless execution under the Linux kernel and desktop environments.

**2.** Create a dedicated, isolated inbound file landing zone inside the user directory to prevent chat downloads from cluttering the host file system:
```bash
mkdir -p ~/Downloads/Telegram_Downloads
```

**3.** Enforce binary integrity via POSIX ownership attributes:
```bash
sudo chown root:root /usr/bin/telegram-desktop
```

**4.** Apply strict execution permissions following the Principle of Least Privilege:
```bash
sudo chmod 755 /usr/bin/telegram-desktop
```

**5.** Create the configuration directory if absent, and open the profile file in the `nano` editor:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/telegram.profile
```

**6.** Insert baseline container isolation rules into the opened configuration file:
```ini
# Telegram Desktop
seccomp

# Exclusively permit access to essential target directories
whitelist ${HOME}/.local/share/TelegramDesktop
whitelist ${HOME}/Downloads/Telegram_Downloads
```
To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit the editor.

**7.** On Ubuntu 24.04/26.04 distributions, default system messenger profiles are overloaded with redundant AppArmor profiles, causing Qt applications to drop network sockets and blind Portmaster's eBPF driver. To completely bypass this bottleneck, launch Telegram using a direct command string: the `--profile=telegram` flag applies our custom profile restrictions, while `--seccomp` enforces kernel-level system call filtering to neutralize local privilege escalation (LPE) exploits:
```bash
firejail --profile=telegram /usr/bin/telegram-desktop
```

The messenger immediately gains outbound host network access, while Portmaster's eBPF lenses capture and render the `telegram-desktop` process within the network monitor UI. Meanwhile, the client's internal file picker remains strictly blind to the rest of the host home directory—seeing only existing session state and the isolated `Telegram_Downloads` folder. Even if a threat actor transmits a malicious payload and it executes within the messenger context, the exploit remains trapped inside a virtual memory vacuum, unable to access SSH keys, cryptocurrency wallets, or sensitive host configurations!

* Near the end of this chapter, we will bind these security parameters directly to system desktop files for seamless execution.

#### Host Cryptographic Foundation: Generating and OPSEC-Protecting GnuPG Keys:

Before passing cryptographic cores into isolated sandboxes of instant messengers and email clients, we must deploy a flawless, mathematically unassailable **OpenPGP (GnuPG)** asymmetric encryption infrastructure on the host. Generation errors or lax file access permissions for keyrings completely neutralize protection, allowing local malware to hijack your digital identity.

> [!NOTE]
> The GnuPG toolkit comes pre-installed by default as a baseline component in Ubuntu Desktop. The `apt` package manager continuously leverages GPG cryptographic algorithms at a deep system level to verify digital signatures of Canonical repositories during system updates, rendering the utility fully operational out of the box.

**1.** Abandon outdated, legacy RSA algorithms in favor of modern, ultra-fast, and highly resistant **Elliptic Curve Cryptography (ECC)**. Launch the interactive GnuPG generator:
```bash
gpg --full-generate-key
```
**Select the following strict security parameters in the interactive wizard:**
> 1. **Key Type:** Select option `(9) ECC and ECC (Sign and Encrypt)`—this provisions separate elliptic curve keys for signing and encryption.
> 2. **Elliptic Curve Type:** Select `(1) Curve 25519` (the renowned Edwards curve `Ed25519`/`Cv25519`)—an established global EdDSA standard immune to hidden state-sponsored backdoors.
> 3. **Expiration Date:** Select `0` (key does not expire) OR define a strict rotation policy (e.g., `1y`—one year).
> 4. **User ID (UID):** Enter your name/handle and target e-mail address.
> 5. **Passphrase:** The system will prompt for a master password to protect the private key in RAM. Supply a generated passphrase at least **20–24 characters** long (comprising random mixed-case alphanumeric characters and special symbols).

> [!IMPORTANT]
> When building a fully anonymous communications perimeter, use a fictional pseudonym paired with a non-existent email account under a privacy-conscious jurisdiction (e.g., `dark_agent@proton.me`).

**2.** By default, the `~/.gnupg` directory is created with overly permissive access attributes. If an unprivileged spy script executes on the system, it could read key metadata. Block this vector by applying strict POSIX permission masks across the hidden directory and key files at the Linux kernel level:
```bash
chmod 700 ~/.gnupg && find ~/.gnupg -type f -exec chmod 600 {} + && find ~/.gnupg -type d -exec chmod 700 {} +
```

> **Security Mechanics:** The permissions mask now forms an impenetrable `drwx------` access barrier. Any process executing outside our current user context attempting to inspect the keyring folder triggers an immediate OS kernel hardware denial: `Permission denied`.

> **(OPSEC Recommendations for Storing Public and Private Key Pairs):** Asymmetric cryptography separates data assets into two distinct entities governed by fundamentally different storage policies:

> [!IMPORTANT]
> When executing key export commands, replace the demonstration address `YOUR-EMAIL@DOMAIN.COM` strictly with the specific e-mail assigned during Step 1 key generation. Otherwise, the GnuPG core returns a `WARNING: nothing exported` error.

**3.** Public Key: Our digital calling card. Interlocutors use it to encrypt outbound messages for us and verify our digital signatures. Its security does not rely on secrecy. You may publish it to GitHub, transmit it across public channels, or attach it to an XMPP profile description. Export the public key block to an ASCII text file:
```bash
gpg --armor --export YOUR-EMAIL@DOMAIN.COM > ~/Downloads/my_public_key.asc
```

**4.** Export the secret key block into the downloads folder:
```bash
gpg --armor --export-secret-keys YOUR-EMAIL@DOMAIN.COM > ~/Downloads/my_PRIVATE_key.asc
```

**MANUAL ACTION:** Copy the `my_PRIVATE_key.asc` asset onto an external encrypted storage medium!

**5.** Destroy the temporary private key stored in Downloads using the `shred` secure deletion tool:
```bash
shred -u -v -n 3 ~/Downloads/my_PRIVATE_key.asc
```

> [!WARNING]
> **Private Key:** Our digital lifeblood and the foundational DNA of our operational sovereignty. We use it to decrypt incoming communications and sign outgoing payload assets. Storing secret keys in cloud environments, mailboxes, or networked storage drives is **STRICTLY PROHIBITED**. Master private keys should reside exclusively in Cold Storage—on an encrypted external physical device (or inside an isolated crypto-container). Only lightweight, easily replaceable daily working subkeys should be imported into the local LUKS host's `~/.gnupg` directory for routine mail encryption, eliminating master key compromise during physical device loss or system intrusion.

> [!NOTE]
> Residual data destruction via `shred`/`wipe`, metadata cleansing via `mat2`, and **VeraCrypt** crypto-container deployment were covered thoroughly in preceding chapters. At this operational stage, an encrypted offline storage volume must already be provisioned to receive private key backups prior to physically purging original files from the local downloads directory.

#### Installing and Sandboxing the Psi+ Jabber Client:

For daily workspace communications, mainstream users typically opt for Telegram. However, across the professional cybersecurity community, the **XMPP (Jabber)** protocol paired with end-to-end encryption remains the benchmark for privacy, decentralization, and absolute digital sovereignty.

We will adopt **Psi+** as our reference client. Unlike the heavy Gajim client (written in Python with an extensive stack of third-party dependencies), Psi+ is a native Qt/C++ application boasting a minimalist architecture and built-in XMPP diagnostic tools, including an integrated XML console.

However, any XMPP client continuously parses massive volumes of untrusted external XML streams, asynchronous links, avatars, and media assets. In theory, this exposes a dangerous attack surface for file-parsing exploits (including critical buffer overflow vulnerabilities within the application core). We significantly constrain the impact of potential Psi+ exploit execution by isolating the client using Firejail.

We establish three valid message encryption vectors depending on our threat model:

* **OMEMO (Modern Standard):** Based on the Signal Double Ratchet cryptographic protocol, featuring Forward Secrecy and encrypted file transfer support. Ideal for daily security collaboration.
* **OpenPGP/GnuPG (Classic Baseline):** Asymmetric encryption backed by robust key pairs. The Psi+ OpenPGP plugin interfaces directly with the host GnuPG infrastructure to handle OpenPGP key operations.
* **OTR (Off-the-Record Messaging):** Absolute symmetric mathematical resistance immune to quantum cryptanalysis (each key is generated manually and used strictly once per message).

Our objective is to build a universal, fault-tolerant sandbox profile that isolates the file system while seamlessly permitting traffic across any selected cryptographic layer.

Because strict UFW firewall policies are enforced on the host, we must append specific egress rules:

**1.** Open the standard XMPP port (5222) for outbound TCP traffic across all servers to allow baseline Psi+ connections:
```bash
sudo ufw allow out to any port 5222 proto tcp
```

**2.** Optionally, open the secure XMPP TLS port (5223) for outbound TCP traffic to support servers enforcing direct TLS connections:
```bash
sudo ufw allow out to any port 5223 proto tcp
```

* **For Ubuntu 24.04 LTS (Noble Numbat) Users:**

**3a.** The default native package inside Ubuntu 24.04 repositories suffers from critical Qt library linkage errors under the Wayland display server (resulting in *Segmentation fault* crashes). To bypass this system bug, add the official Psi+ developer PPA, fetch the adapted stable Psi+ v1.5.2068 build, the plugin suite (including OMEMO), and the baseline GnuPG framework in a single command:
```bash
sudo add-apt-repository ppa:psi-plus/ppa -y && sudo apt update && sudo apt install psi-plus psi-plus-plugins gnupg -y
```

* **For Ubuntu 26.04 LTS (Resolute Raccoon) Users:**

In Ubuntu 26.04, the upstream repository supplies Psi+ branch 1.4.1456. The required 1.5.2068 version could not simply be ported from Noble because pre-compiled Noble plugins were linked against outdated ABIs. Consequently, Psi+ 1.5.2068 was recompiled directly on Ubuntu 26.04 Resolute from the official 1.5.2068 source archive. The client and plugin suite were then consolidated into a single package: `psi-plus-resolute-client-and-plugins_1.5.2068-1~resolute1_amd64.deb`. As a result, OMEMO, OTR, and OpenPGP utilize libraries native to Resolute without backporting legacy Noble dependencies.

Two deployment paths are available. The first option installs the older yet functional Psi+ v1.4.1456 build from official system repositories. The second option installs the version recompiled for this book's repository based on the `noble` release source.

**Option 1:**

**3b1.** Install Psi+ version 1.4.1456 directly from standard system repositories:
```bash
sudo apt update && sudo apt install psi-plus psi-plus-plugins -y
```

**Option 2:**

**3.b2-1.** Download the custom `.deb` package from the author's repository (`github.com/eugexo`):
```bash
wget https://raw.githubusercontent.com/EugeXo/security-baseline-ubuntu/main/_assets/psi-plus/psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
```

> [!IMPORTANT]
> Do not implicitly trust downloaded `.deb` binaries prior to installation. Verify the file's checksum and inspect its structural contents first. While this does not prove the absence of malicious code, it confirms payload integrity and reveals exactly what assets will be deployed to the host. **This verification procedure must be applied across all untrusted or third-party sources.**
> 
> Verify the SHA-256 checksum of the package:
> ```bash
> sha256sum psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
> ```
> 
> Inspect `.deb` metadata headers prior to installation:
> ```bash
> dpkg-deb -I psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
> ```
> 
> Inspect the internal archive manifest:
> ```bash
> dpkg-deb -c psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb
> ```
> A matching SHA-256 hash confirms the received asset matches the verified upstream reference, but hash validation alone does not guarantee software trustworthiness. Treat hash verification as one defensive layer among many, rather than absolute proof of safety.

**3.b2-2.** Following hash validation, execute the Psi+ package installation. Ubuntu's package manager will automatically resolve and install necessary system dependencies:
```bash
sudo apt install ./psi-plus-client-and-plugins-1.5.2068-resolute1-amd64.deb -y
```

**4.** Launch Psi+ using its canonical system command. Firejail automatically parses baseline security directives, applies the default profile, and renders the graphical interface:
```bash
firejail psi-plus
```

Psi+ allows messaging encryption via OMEMO, OTR, or OpenPGP. Meanwhile, Firejail's mandatory access controls restrict file system access and significantly contain the impact of potential application-level vulnerabilities.

Optional WebKit/WebEngine binaries and unnecessary dependencies were intentionally omitted from this build. The result is a streamlined Psi+ 1.5.2068 deployment featuring full native plugin support (including OMEMO, OTR, and OpenPGP) without extraneous web engines or unnecessary functionality outside our core OPSEC perimeter.

> [!IMPORTANT]
> Additional outbound network rules for file transfers depend on your specific XMPP server configuration and its associated HTTP Upload/proxy services.

* Toward the end of this chapter, we will configure permanent sandboxed execution by embedding these parameters directly into custom `.desktop` shortcuts.

#### Installing and Sandboxing Thunderbird (Encrypted Email Workflow):

Email represents a critically vulnerable host zone. Modern phishing campaigns and targeted attacks rely on malicious attachments and embedded JavaScript payloads packed inside incoming messages. Running an uncontained email client poses a direct threat of host compromise. We will deploy the reference **Thunderbird** client, seal its local message database within an isolated sandbox perimeter, and fully integrate it with our host OpenPGP cryptographic core.

**1.** The default `thunderbird` package in Ubuntu repositories is a transitional stub requiring the presence of the `snapd` framework—which has been completely removed from our system setup. To bypass this deadlock and force the package manager to fetch native binaries directly from the official Mozilla Team PPA, create a strict pin priority file:
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

**2.** Protect our future native package from accidental deletion, rollback, or forced replacement by Snap dummy stubs during background operating system updates:

* **For Ubuntu 24.04 LTS (Noble Numbat) Users:**
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:noble";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-mozilla
```
* **For Ubuntu 26.04 LTS (Resolute Raccoon) Users:**
```bash
echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:resolute";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-mozilla
```

**3.** Update the local package cache and install native Thunderbird:
```bash
sudo apt update && sudo apt install thunderbird -y
```

**4.** Create a Firejail isolation profile for Thunderbird:
```bash
mkdir -p ~/.config/firejail && nano ~/.config/firejail/thunderbird.profile
```

**5.** Append baseline container isolation rules into the opened configuration file:
```ini
caps.drop all
nonewprivs

whitelist ~/.thunderbird
whitelist ~/Downloads/Mail_Attachments

# Rapid container teardown upon application exit
deterministic-shutdown
```

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit the editor.

> [!WARNING]
> It is **strictly prohibited** to launch Thunderbird while the system remains connected to the internet. Upon its very first launch, the application will immediately transmit initial telemetry payloads outbound across the network.

**6.** Disable all network interfaces to prevent the mail client from "calling home" during initialization, then launch Thunderbird to establish its baseline internal profile architecture:
```bash
nmcli networking off
```
**Following execution of this command, launch Thunderbird manually from the applications menu.** Wait 2–3 seconds for directory structure generation to complete, then close the application entirely.

**7.** Navigate to the generated UUID profile directory and initialize a clean configuration file:
```bash
cd ~/.thunderbird/*default-release && touch user.js
```

**8.** Open the newly created `user.js` file in the `nano` terminal editor:
```bash
nano user.js
```

**9.** Copy our ultimate OPSEC security directive array—completely blinding Gecko core telemetry modules—and paste it into the editor buffer:
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

To commit modifications in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to exit back to the console shell.

**10.** Lock file access permissions by applying a strict read-only POSIX mask for the file owner (`0400`), preventing any background host process from silently modifying our hardened security profile:
```bash
chmod 0400 user.js
```

**11.** To prevent mail attachments from scattering across the system and silently modifying host configuration paths, initialize a dedicated landing zone directory:
```bash
mkdir -p ~/Downloads/Mail_Attachments
```

**12.** Restore host internet connectivity (replacing `enp0s1` with your specific interface identifier):
```bash
nmcli networking on && nmcli connection up netplan-enp0s1
```

**13.** Execute the isolated Thunderbird instance using our custom profile. To ensure heavy email rendering on NVIDIA hardware under Wayland does not trigger interface crashes, wrap application execution in a universal wrapper that dynamically detects active proprietary drivers and unblinds necessary device nodes while preserving strict file system whitelisting for Intel/AMD setups:
```bash
firejail --profile=thunderbird /usr/bin/thunderbird
```

> [!IMPORTANT]
> **Air-Gapped Encrypted Mail Processing Protocol:** Storing private cryptographic keys permanently on the host system or inside application sandboxes introduces a critical security vulnerability. We mitigate this risk by applying a temporary, offline key import workflow:
> 
> **1.** Launch Thunderbird within the Firejail sandbox container to fetch and synchronize inbound encrypted messages from remote servers.
> **2.** Disable all host network interfaces, bringing the entire operating system and Thunderbird into a completely isolated offline state:
> ```bash
> nmcli networking off
> ```
> **3.** Connect an encrypted external USB storage medium and transfer required key files exclusively into our designated file landing zone: `~/Downloads/Mail_Attachments`.
> **4.** Inside the Thunderbird interface, click the top-right **burger menu**, navigate to **Tools** ➔ **OpenPGP Key Manager** ➔ **File**, and select **Import Public Key(s) From File** and **Import Secret Key(s) From File** respectively.
> **5.** Import the target key blocks, then decrypt and review confidential messages offline.
> **6.** Once reading is complete, purge the private key pair directly from Thunderbird's key store interface.
> **7.** Permanently destroy residual key files located in the landing zone by running a 3-pass secure overwrite routine from the host terminal:
> ```bash
> shred -u -n 3 ~/Downloads/Mail_Attachments/PRIVATE_key.asc
> ```
> **8.** Re-enable host network connectivity only after verifying complete erasure of cryptographic material. On Ubuntu 24.04/26.04 builds, network state re-initialization can stall after interface teardown. Force network link recovery using the following explicit command string (replacing `netplan-enp0s1` with your physical interface name):
> ```bash
> nmcli networking on && nmcli connection up netplan-enp0s1
> ```
> 
> Mail traffic remains fully visible to Portmaster's eBPF filtering driver, while the host file system is completely shielded: even if an incoming encrypted message packs a zero-day exploit payload, execution remains contained inside the isolated sandbox, lacking outbound network channels for data exfiltration and blocked by strict kernel-level read-only boundaries!

* Toward the end of this chapter, we will bind these security parameters directly to system desktop files for seamless execution.

#### Automating the Defensive Perimeter (Firecfg Utility) and Customizing System Icons:

Repeatedly entering long commands manually into the terminal quickly becomes exhausting. To automate this process, we leverage the built-in `firecfg` tool. It scans the operating system and automatically wraps standard applications (browsers, torrent clients, email clients) inside isolated sandbox containers.

> [!IMPORTANT]
> Modern Firejail releases omit local unprivileged automation modes. Executing `firecfg` requires elevated root privileges because the utility constructs global symbolic links within the `/usr/local/bin` system directory.
>
> While `sudo firecfg` provides convenient bulk sandbox enrollment, running it blindly without auditing targeted applications is discouraged. Controlled, targeted isolation via explicit profile definitions and dedicated user `.desktop` files remains the preferred security approach.

**1.** Enable the global application launcher sandbox integration:
```bash
sudo firecfg
```

**2.** To prevent path collisions, stale symlink layering, and cascade failures when operating alongside AppArmor, execute an atomic reset sequence using the `&&` operator. This completely purges legacy symlinks before deploying fresh sandbox wrappers from scratch:
```bash
sudo firecfg --clean && sudo firecfg
```

This command first flushes obsolete, potentially conflicting symlinks, then deploys a clean sandbox execution framework in a single pass. Clicking application icons (e.g., Firefox or Evince) within the GNOME application launcher will now transparently spawn those binaries inside isolated container environments.

To eliminate human error, visually distinguish hardened sandbox containers from unprotected host processes, and replace default generic GNOME icons, deploy isolated user-level launchers featuring custom visual assets for our web browser and local AI stack.

**3.** Create the user icon directory hierarchy and copy downloaded 256px (`256x256`) and 512px (`256x256@2x`) PNG assets into their respective destination paths:
```bash
mkdir -p ~/.local/share/icons/{256x256,256x256@2x} && cp "$HOME/PATH-TO-FILES/icons/256x256/"*.png ~/.local/share/icons/256x256/ && cp "$HOME/PATH-TO-FILES/icons/256x256@2x/"*.png ~/.local/share/icons/256x256@2x/
```

> [!WARNING]
> After modifying `Exec=` directives for applications such as LibreOffice, Image Viewer, or Document Viewer, log out of your desktop session ("Log Out...") or reboot the host system to force desktop environment menu caching routines to register updated entry points.

* Generate the primary hardened launcher for **Mozilla Firefox running inside Firejail**, strictly bound to our hardened security profile and explicit icon path:
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

* Modify the uncontained **Mozilla Firefox launcher** (reserved for downloading large files directly to the host), assigning it a distinct visual icon:

```bash
sudo sed -i -e 's/^Name=.*/Name=Firefox (Unsecured Host)/' -e "s|^Icon=.*|Icon=/home/$USER/.local/share/icons/256x256@2x/firefox-unsecure.png|" /usr/share/applications/firefox.desktop
```

* **For Ubuntu 24.04 LTS (Noble Numbat) Users (Document and Image Viewers):**

Configure Firejail sandbox wrapping for the **Evince Document Viewer** launcher:
```bash
sudo sed -i 's|^Exec=evince.*$|Exec=firejail evince|' /usr/share/applications/org.gnome.Evince.desktop
```

Verify configuration changes:
```bash
grep 'Exec=' /usr/share/applications/org.gnome.Evince.desktop
```

Configure Firejail sandbox wrapping for the **Eye of GNOME (Eog) Image Viewer** launcher:
```bash
sudo sed -i 's|^Exec=eog.*$|Exec=firejail eog|' /usr/share/applications/org.gnome.eog.desktop
```

Verify configuration changes:
```bash
grep 'Exec=' /usr/share/applications/org.gnome.eog.desktop
```

* **For Ubuntu 26.04 LTS (Resolute Raccoon) Users (Document and Image Viewers):**

Configure Firejail sandbox wrapping for the **Papers Document Viewer** launcher:
```bash
sudo sed -i 's|^Exec=papers.*$|Exec=firejail papers|' /usr/share/applications/org.gnome.Papers.desktop
```

Verify configuration changes:
```bash
grep 'Exec=' /usr/share/applications/org.gnome.Papers.desktop
```

Configure Firejail sandbox wrapping for the **Loupe Image Viewer** launcher, disabling D-Bus activation to force binary interception:
```bash
sudo sed -i 's|^Exec=loupe.*$|Exec=firejail loupe %U|; s|^DBusActivatable=true$|DBusActivatable=false|' /usr/share/applications/org.gnome.Loupe.desktop
```

Verify configuration changes:
```bash
grep -E '^(Exec|DBusActivatable)=' /usr/share/applications/org.gnome.Loupe.desktop
```

* Harden the **KeePassXC** application launcher, isolating its execution context and network access (optionally backing up the original desktop entry):
```bash
sudo cp /usr/share/applications/org.keepassxc.KeePassXC.desktop /usr/share/applications/org.keepassxc.KeePassXC.desktop.bak
```

```bash
sudo sed -i -e 's/^Name=.*/Name=KeePassXC (Secure Sandbox)/' -e 's|^Exec=.*|Exec=firejail --net=none keepassxc %f|' -e "s|^Icon=.*|Icon=$HOME/.local/share/icons/256x256@2x/keepassxc-secure.png|" /usr/share/applications/org.keepassxc.KeePassXC.desktop
```

* Apply Firejail sandbox execution across the entire **LibreOffice** productivity suite:

This process updates binary invocation targets across desktop entries to launch under Firejail isolation by modifying primary and secondary `Exec` entries:

```bash
sudo sed -i 's|^Exec=libreoffice|Exec=firejail libreoffice|' /usr/share/applications/libreoffice-startcenter.desktop
sudo sed -i 's|^Exec=libreoffice --writer|Exec=firejail libreoffice --writer|' /usr/share/applications/libreoffice-writer.desktop
sudo sed -i 's|^Exec=libreoffice --calc|Exec=firejail libreoffice --calc|' /usr/share/applications/libreoffice-calc.desktop
sudo sed -i 's|^Exec=libreoffice --impress|Exec=firejail libreoffice --impress|' /usr/share/applications/libreoffice-impress.desktop
sudo sed -i 's|^Exec=libreoffice --draw|Exec=firejail libreoffice --draw|' /usr/share/applications/libreoffice-draw.desktop
sudo sed -i 's|^Exec=libreoffice --math|Exec=firejail libreoffice --math|' /usr/share/applications/libreoffice-math.desktop
sudo sed -i 's|^Exec=libreoffice --base|Exec=firejail libreoffice --base|' /usr/share/applications/libreoffice-base.desktop
```
All office suite binaries will now execute within the boundary constraints specified inside `libreoffice.profile`.

Verify each updated desktop launcher:
```bash
grep 'Exec=' /usr/share/applications/libreoffice-writer.desktop
grep 'Exec=' /usr/share/applications/libreoffice-calc.desktop
grep 'Exec=' /usr/share/applications/libreoffice-impress.desktop
grep 'Exec=' /usr/share/applications/libreoffice-draw.desktop
grep 'Exec=' /usr/share/applications/libreoffice-math.desktop
grep 'Exec=' /usr/share/applications/libreoffice-base.desktop
```

* Enforce sandbox isolation for **GIMP**:
Locate the system target desktop entry:
```bash
find /usr/share/applications -iname '*gimp*'
```

Modify the execution path (adjusting target filename if package variations exist):
```bash
sudo sed -i 's|^Exec=|Exec=firejail |' /usr/share/applications/gimp.desktop
```

Verify launcher modifications:
```bash
grep 'Exec=' /usr/share/applications/gimp.desktop
```

* Generate an isolated desktop entry for **VS Codium without network access (Offline Mode)**:
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

* Generate an isolated desktop entry for **VS Codium with network access (Online Mode for extension management)**:
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

* Create an online launcher for **LM Studio** with network access (for downloading model weights from Hugging Face), dynamically adapting to hardware configurations (NVIDIA GPU or CPU fallback):
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

* Construct an air-gapped launcher for **LM Studio (Offline AI Mode)**. The underlying wrapper dynamically detects NVIDIA hardware, passes through CUDA inference interfaces, isolates execution behind network kill switches, and applies HiDPI visual assets:
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
> Background processes such as LM Studio's `node-Main` remain active in the system tray after closing the graphical UI. Failing to fully terminate running instances causes secondary launchers to hook into existing background sessions. Fully quit tray processes before switching between online and offline profiles.

* Generate a hardened launcher for **Telegram**, configuring sandbox constraints and `seccomp` kernel filtering:
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

* Generate an isolated entry for the **Psi+** XMPP client. This entry registers the application within GNOME menus, restricts access to the general home directory structure (including default downloads), whitelists strict state paths required for OMEMO keys and chat history, and routes cryptographic operations directly to the host GnuPG engine:
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
> The `psi-plus` background process minimizes to the system tray upon closing the window. Completely terminate active tray instances before launching alternate profile modes to avoid process session hijacking.

* Generate a hardened **Thunderbird** desktop entry delivering path whitelisting, LPE attack mitigation, and NVIDIA driver passthrough for Wayland environments:
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

* Update the **Terminal** application icon on **Ubuntu 24.04 LTS**:
```bash
sudo sed -i "s|^Icon=org.gnome.Terminal|Icon=/home/$USER/.local/share/icons/256x256@2x/terminal.png|" /usr/share/applications/org.gnome.Terminal.desktop
```

* Update the **Ptyxis Terminal** application icon on **Ubuntu 26.04 LTS**:
```bash
sudo sed -i "s|^Icon=org.gnome.Ptyxis|Icon=/home/$USER/.local/share/icons/256x256@2x/terminal.png|" /usr/share/applications/org.gnome.Ptyxis.desktop
```

* (Optional) Customize system **Trash** icon resources (replacing `PATH-TO-FILES` with your relative icon path, e.g., `.local/share/`):
```bash
for s in 16x16 16x16@2x 24x24 24x24@2x 32x32 32x32@2x 48x48 48x48@2x 256x256 256x256@2x; do sudo cp "$HOME/PATH-TO-FILES/icons/Trash/$s/"user-trash{,-full}.png /usr/share/icons/Yaru/$s/status/; done && for s in 16x16 16x16@2x 24x24 24x24@2x 32x32 32x32@2x 48x48 48x48@2x 256x256 256x256@2x; do sudo cp "$HOME/PATH-TO-FILES/icons/Trash/$s/"user-trash{,-full}.png /usr/share/icons/Yaru/$s/places/; done
```

Restore standard POSIX read permissions across updated icon assets:
```bash
sudo find /usr/share/icons/Yaru -type f -name 'user-trash*.png' -exec chmod 644 {} \;
```

**4.** Force GNOME Shell to reindex the application database, instantly reflecting updated launcher entry points without requiring a full system reboot:
```bash
update-desktop-database ~/.local/share/applications/
```

**5.** Refresh the system icon cache index:
```bash
gtk-update-icon-cache -f ~/.local/share/icons/
```

>[!NOTE]
> For applications handling diverse file types, query active MIME type bindings directly via terminal using `grep`. Format support varies across package revisions; auditing file associations ensures proper file handler bindings across desktop environments.
>
> Example query to extract active MIME type bindings for GIMP:
> ```bash
> grep '^MimeType=' /usr/share/applications/gimp.desktop
> ```

* Upon completing profile and launcher modifications, reboot the operating system:
```bash
sudo reboot
```

>[!IMPORTANT]
> Let's analyze user-level application launcher override configurations via `.desktop` files.
>
> Direct modification of system-wide launchers located in `/usr/share/applications/` is discouraged because upstream package updates overwrite custom edits.
>
> The recommended method involves creating user-level overrides inside:
> ```bash
> ~/.local/share/applications/
> ```
>
> Entries in this directory take operational precedence over global system definitions stored in:
> ```bash
> /usr/share/applications/
> ```
>
> Locate target system `.desktop` files using `find`:
> ```bash
> find /usr/share/applications/ ~/.local/share/applications/ -name "APP-NAME.desktop" 2>/dev/null
> ```
>
> Alternatively, query installed package manifests via `dpkg`:
> ```bash
> dpkg -L APP_NAME | grep "\.desktop$"
> ```
>
> **Example:** Locating GIMP launcher files:
> ```bash
> dpkg -L gimp | grep "\.desktop$"
> ```
>
> Create a local user-space copy:
> ```bash
> cp /usr/share/applications/gimp.desktop ~/.local/share/applications/gimp.desktop
> ```
>
> Open the localized desktop file:
> ```bash
> nano ~/.local/share/applications/gimp.desktop
> ```
> 
> Replace the existing `Exec=gimp %U` directive with `Exec=firejail --quiet gimp %U`.
> 
> Optionally update display parameters, e.g., `Name=GIMP (Sandbox)`.
> 
> Rebuild the local desktop database to apply modifications:
> ```bash
> update-desktop-database ~/.local/share/applications/
> ```
>
> Launching the target application through desktop menus will now execute inside Firejail.
>
> To hide duplicate or redundant system application entries from desktop menus entirely, deploy a localized override file:
> ```ini
> cat <<EOF> ~/.local/share/applications/APP-NAME.desktop
> [Desktop Entry]
> Type=Application
> Name=Hidden System Link
> NoDisplay=true
> EOF
> ```
>
> This entry suppresses redundant menu listings while preserving underlying system functionality.

> [!TIP]
> Use native GNOME Shell configuration keys to toggle desktop icon displays without removing underlying file assets.
> 
> Desktop Trash Icon:
> ```bash
> gsettings set org.gnome.shell.extensions.ding show-trash false  # Hide
> gsettings set org.gnome.shell.extensions.ding show-trash true   # Display
> ```
> 
> Desktop Home Folder:
> ```bash
> gsettings set org.gnome.shell.extensions.ding show-home false   # Hide
> gsettings set org.gnome.shell.extensions.ding show-home true    # Display
> ```

> [!IMPORTANT]
> GNOME 46+ running on Wayland maintains strict internal application launcher caching. Modifying existing `.desktop` files with altered launch flags, parameters, or binary targets can cause GNOME Shell to reject menu clicks, treating modified profiles as untrusted—even when direct invocation via `gtk-launch` works as expected.
> 
> The most reliable fix to clear stale desktop launcher metadata is renaming the target desktop file identifier, bypassing cached desktop entries.
> 
> If newly deployed desktop launchers fail to respond to click events within application menus, purge the GNOME launcher cache by renaming the entry files (illustrated using LM Studio):
> 
> * For offline LM Studio Firejail sessions:
> ```bash
> mv ~/.local/share/applications/lm-studio.desktop ~/.local/share/applications/lm-offline.desktop 2>/dev/null || true
> ```
> * For online LM Studio Firejail sessions:
> ```bash
> mv ~/.local/share/applications/lm-studio-unsecure.desktop ~/.local/share/applications/lm-online.desktop 2>/dev/null || true
> ```
> * Rebuild the global application menu index:
> ```bash
> update-desktop-database ~/.local/share/applications/
> ```
> * Refresh local icon caches:
> ```bash
> gtk-update-icon-cache -f ~/.local/share/icons/
> ```
> 
> Opening the application grid ("Show Apps") forces GNOME to discover **LM Studio (Offline AI)** and **LM Studio (Online Downloader)** as distinct entities, re-validate execution permissions, and enable reliable UI execution.

#### Advanced Paranoia Mode: Sandboxing with Session Persistence via Overlay:

Using the `--private` flag is ideal for ephemeral, single-use sessions. But what should you do when you need to rigorously audit a questionable utility's behavior, retain its configuration files or plugins, while guaranteeing absolute protection for the underlying operating system against infection?

For this, we tap into a hidden killer feature of Firejail—**Overlay Mode**. This mechanism constructs a temporary virtual layer over your actual file system. The application perceives your files as fully accessible, yet remains physically incapable of modifying a single byte on the physical disk: every write attempt, configuration creation, or stealthy malware persistence routine is transparently redirected into an isolated sandbox overlay directory.

**1.** Execute an application while redirecting state changes to a dedicated overlay layer:
```bash
firejail --overlay-dir=~/.sandbox_overlay --seccomp --nonewprivs telegram-desktop
```
*(The `--overlay-dir=` parameter defines the target directory path where all file system modifications generated during the session will be intercepted and stored).*

**2.** After terminating the application, inspect the isolated overlay directory structure to audit runtime modifications:
```bash
ls -la ~/.sandbox_overlay
```
This grants full visibility into any hidden files or configuration changes the utility attempted to write across `/etc`, `/var`, or your user home directory!

**3.** If the audit confirms benign application behavior, retain the overlay directory for subsequent launches. Conversely, if malicious or suspicious activity is detected, completely purge all runtime traces from the host operating system with a single command:
```bash
rm -rf ~/.sandbox_overlay
```

<br>

## Installing Rkhunter and Hunting Rootkits

Next, we will focus on internal host operating system security—fortifying the system against potential compromise and auditing it for hidden malware and rootkits. Rootkits represent a dangerous class of malicious software that deeply embeds into the OS kernel and conceals its presence by modifying or replacing core system binaries.

To perform rootkit scanning and system file integrity verification, we will deploy `Rkhunter`. To scan for viruses and general threats, we will implement `ClamAV`—a battle-tested, open-source antivirus engine that does not exfiltrate private user data to third-party corporate servers. For operational security, both utilities will be run strictly via the command line interface without graphical wrappers.

**1.** Install the rootkit scanner utility:
```bash
sudo apt install rkhunter -y
```

**2.** In the interactive `debconf` pseudo-graphical prompt that appears, explicitly select **"No configuration"** and press **"Enter"**. This completely blocks the installation of background mail-routing daemons for automated reporting, eliminating unintended network exposure.

**3.** Open the primary application configuration file:
```bash
sudo nano /etc/rkhunter.conf
```

Locate and modify the following configuration keys to ensure signature updates are fetched exclusively through secure mirror nodes:
```ini
UPDATE_MIRRORS=1
MIRRORS_MODE=0
AUTO_X_DETECT=0
WEB_CMD=""
```

To prevent the scanner from throwing false positive warnings on purged system components (`snapd`) and our custom security directives (such as the YubiKey Kill Switch), append strict security exceptions to the bottom of the file:
```ini
# Whitelist purged Snap directories so the scanner does not flag missing paths
EXISTWHITELIST="/var/lib/snapd/*"
EXISTWHITELIST="/snap"

# Authorize our custom session kill switch udev rule
FILEWHITELIST="/etc/udev/rules.d/80-yubikey-kill.rules"

# Suppress false positives on specific Ubuntu shell script wrappers
SCRIPTWHITELIST="/usr/bin/egrep"
SCRIPTWHITELIST="/usr/bin/fgrep"
```

Save your changes in `nano` by pressing **"Ctrl + O"** ➔ **"Enter"**, followed by **"Ctrl + X"** to return to the shell.

**4.** Verify that `rkhunter` is running the latest engine release:
```bash
sudo rkhunter --versioncheck
```

**5.** Download and install updated detection signatures and test rules:
```bash
sudo rkhunter --update
```

**6.** Generate an initial baseline snapshot of known-good system binary properties:
```bash
sudo rkhunter --propupd
```
This step creates an authoritative reference database of file cryptographic hashes across the current system.

**7.** Launch an interactive system audit:
```bash
sudo rkhunter --check --sk
```
The `--sk` (*skip-keypress*) flag automatically bypasses prompts to press **"Enter"** between test sections, running the entire audit in a single pass.

To prevent unnecessary system overhead and eliminate unprompted background execution, disable automated scheduled scans.

**8.** Open the daily task configuration file:
```bash
sudo nano /etc/default/rkhunter
```

**9.** Locate the `CRON_DAILY_RUN` key and set its value to `false`:
```ini
CRON_DAILY_RUN="false"
```

Save the configuration in `nano` by pressing **"Ctrl + O"** ➔ **"Enter"**, then **"Ctrl + X"** to exit.

> [!IMPORTANT]
> Note that `Rkhunter` relies on heuristic analysis and produces a baseline level of false positives. If the tool reports a *Possible rootkit* alert on a fresh, pristine system setup, it is almost certainly a false alarm.
> 
> The aggressive AppArmor hardening, telemetry removal, and Snapd purging performed in previous steps significantly altered system configurations under `/etc`. The initial scan will flag these modifications and trigger a few *Warnings*—this is expected system behavior.
> 
> Document the baseline output of this initial "clean" scan. If subsequent routine audits reveal unexpected cryptographic hash discrepancies, perform a targeted manual investigation. Remember that `Rkhunter` functions strictly as an auditing engine—it does not remove infected files. In the event of an actual compromise, remediating rogue kernel modules requires manual intervention following security incident response procedures.
> 
> Pay special attention to the `sudo rkhunter --propupd` command. This directive generates the reference hash database stored at `/var/lib/rkhunter/db/rkhunter.dat`. Always observe this core rule: re-run `sudo rkhunter --propupd` immediately after every legitimate package upgrade via `sudo apt upgrade`.
> 
> Skipping this step causes subsequent `Rkhunter` scans to emit critical false warnings across basic system binaries (such as `ls`, `ps`, or `top`), as their file hashes naturally change during official package updates. The correct administrative workflow is: upgrade system packages ➔ verify overall system stability ➔ execute `sudo rkhunter --propupd` to refresh the reference snapshot in the database.

<br>

## Installing and Configuring the ClamAV Antivirus Scanner

#### Introduction:

ClamAV is a fully featured, open-source antivirus engine. Within Linux operating systems, it is primarily deployed to inspect incoming mail attachments, scan external encrypted USB drives, or audit web downloads for embedded malware targeting Windows environments, ensuring malicious payloads are not inadvertently transferred to other workstations across the network.

#### Installing ClamAV:

**1.** Install the ClamAV antivirus engine and its background system daemon:
```bash
sudo apt install clamav clamav-daemon -y
```

**2.** Verify the installation and check the active scanner version:
```bash
clamscan --version
```

**3.** Install the official Graphical User Interface (GUI)—an optional step for users who prefer visual management:
```bash
sudo apt install clamtk -y
```

**4.** Launch the antivirus GUI frontend:
```bash
clamtk
```

#### Updating Signature Databases and Bypassing Network Blocks:

The background automatic update service for the antivirus engine may encounter network delivery failures or regional endpoint restrictions (manifesting as HTTP *403 Forbidden* errors). To guarantee secure and reliable database retrieval, disable the automated updater daemon and perform manual synchronization:

**1.** Temporarily stop the background automatic update daemon prior to performing manual database operations:
```bash
sudo systemctl stop clamav-freshclam
```

**2.** Initiate the standard CLI signature update sequence:
```bash
sudo freshclam
```

> [!NOTE]
> **Author's Note:** If the updater emits access restriction errors, upstream Cisco Talos servers are actively blocking incoming connection requests. Under this scenario, current signature database files (`main.cvd`, `daily.cvd`, `bytecode.cvd`) must be downloaded manually over a secure proxy tunnel from the official mirror at `database.clamav.net` or retrieved from trusted community security mirrors. The official Microsoft technology repository serves as a fast, reliable, fully open alternative mirror: `https://packages.microsoft.com/clamav/`.

Once the download finishes, open a terminal in the `~/Downloads` folder and transfer the files directly into the system antivirus database directory using the following commands:

**3.** Copy all three downloaded signature database files using a single command:
```bash
sudo cp main.cvd daily.cvd bytecode.cvd /var/lib/clamav/
```

**4.** Explicitly grant file ownership to the system `clamav` service account, as the antivirus engine cannot read the signature set without proper permissions:
```bash
sudo chown clamav:clamav /var/lib/clamav/*
```

**5.** Re-enable and start the background update daemon:
```bash
sudo systemctl enable clamav-freshclam --now
```

#### Structuring System Scans:

**1.** Launch a full root partition scan with elevated superuser privileges:
```bash
sudo clamscan -r -i --max-filesize=100M --max-scansize=100M --exclude-dir="^/sys" --exclude-dir="^/proc" --exclude-dir="^/dev" --exclude-dir="^/snap" --exclude-dir="^/run" /
```

Break down the filtering parameters of this heavy scan command:
* **`-r`** (*recursive*) — Perform deep inspection across nested subdirectories.
* **`--bell`** — Sound an audible terminal bell alert upon detecting any threat.
* **`-i`** (*infected*) — Output strictly infected file entries to screen stdout, keeping the console free of millions of clean file logs.
* **`--exclude-dir`** — Explicitly bypass virtual kernel filesystems (`/sys`, `/proc`, `/dev`) and container mounts (`/snap`, if not purged in previous chapters) to prevent execution loops across pseudo-filesystem interfaces.

**2.** Perform a rapid audit of the current user's home directory (personal documents and data files):
```bash
clamscan -r /home/$USER
```

**3.** Display a concise CLI reference for available tool options:
```bash
clamscan --help
```

**4.** Open the official system manual detailing all advanced scanner flags and fine-tuning options:
```bash
man clamscan
```

If the antivirus component is no longer required, execute a complete purge to remove the package along with all leftover configuration files in a single step:

**5.** Completely purge ClamAV and its graphical GUI frontend:
```bash
sudo apt purge clamav clamav-base clamav-daemon clamav-freshclam clamtk -y && sudo apt autoremove --purge -y
```

#### Multithreaded Scanning (Hardening):

By default, the standard `clamscan` command operates strictly single-threaded, causing full system disk audits to take anywhere from 5 to 8 hours while pegging a single CPU core at 100%. To dramatically boost execution efficiency, leverage the multi-threaded `clamdscan` engine powered by the running `clamav-daemon` service. It parallelizes the workload across all available CPU cores, accelerating scan speeds by 4x to 6x!

**1.** Execute a multi-threaded system-wide filesystem audit:
```bash
sudo clamdscan -m --fdpass --stream --config-file=/etc/clamav/clamd.conf /
```
The `-m` (*multiscan*) flag enables parallel processing.

> [!WARNING]
> Exercise extreme caution when using the aggressive `--remove` flag for instantaneous destruction of detected threats. In the event of a false positive, the engine could permanently delete a critical system binary, immediately compromising operating system stability.

To safely isolate potential threats into a secure quarantine zone rather than destroying them immediately, create a dedicated directory and assign ownership permissions to the antivirus daemon:

**2.** Create the quarantine directory:
```bash
sudo mkdir -p /var/lib/clamav/quarantine
```

**3.** Assign directory ownership to the antivirus service account:
```bash
sudo chown clamav:clamav /var/lib/clamav/quarantine
```

Only after establishing the target isolation directory, execute high-speed multi-threaded scanning with automatic threat quarantine movement:

**4.** Launch multi-threaded disk scanning with threat quarantine redirection:
```bash
sudo clamdscan -m --fdpass --move=/var/lib/clamav/quarantine --stream /
```

> [!NOTE]
> Including the `--fdpass` (*file descriptor passing*) flag in multi-threaded scan invocations is strictly required. It forces the terminal to pass target file descriptors directly to the background daemon, allowing seamless auditing of protected filesystem paths that the unprivileged `clamav` system user cannot access directly.

<br>

## Installing and Configuring the VirtualBox Virtualization Environment

The ideal tool for creating isolated virtual machines and safely testing third-party operating systems (such as Kali Linux, Parrot OS, Windows, and others) is VirtualBox. To ensure maximum stability, deploy the official release directly from Oracle's repositories.

**1.** Prevent critical package manager deadlocks. Previous chapters implemented strict PAM stack hardening and disabled biometric authentication; consequently, scheduled updates for fingerprint reader libraries will cause an indefinite runtime hang at 78%. Explicitly unhold, completely purge, and erase leftover configuration traces for the biometric daemon and background auto-updaters:
```bash
sudo apt-get purge fprintd libfprint-2-2 libfprint-2-tod1 libpam-fprintd unattended-upgrades --allow-change-held-packages -y
```

**2.** Perform a clean update of package indices and core OS modules without triggering interactive terminal stalls:
```bash
sudo apt update && sudo apt upgrade -y
```

**3.** Install base compilers (`gcc`, `make`) and the `dkms` framework, required to build VirtualBox kernel modules automatically during scheduled Linux kernel updates:
```bash
sudo apt install wget dkms build-essential -y
```

**4.** Integrate the official Oracle repository into `apt` sources. To eliminate reliance on vendor-side cryptographic discrepancies (such as short 32-bit PGP key collisions) and bypass stuck signature checks under strict 4x4 host isolation, force the `[trusted=yes]` override flag. Packages will be securely pulled over an encrypted TLS HTTPS channel directly from Oracle's official domain.

For **Ubuntu 24.04 LTS (Noble Numbat)**, declare the `noble` branch:
```bash
echo "deb [arch=amd64 trusted=yes] https://download.virtualbox.org/virtualbox/debian noble contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
```

For **Ubuntu 26.04 LTS (Resolute Racoon)**, explicitly lock the sources to the stable parent LTS base (`noble`), as Oracle servers do not maintain a distinct directory for the 2026 release cycle:
```bash
echo "deb [arch=amd64 trusted=yes] https://download.virtualbox.org/virtualbox/debian resolute contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
```

**5.** Update the system package repository lists. The `[trusted=yes]` directive forces the system to bypass vendor key validation and seamlessly ingest repository metadata into runtime:
```bash
sudo apt update
```

> [!NOTE]
> Having intentionally bypassed importing legacy Oracle signing keys, the `apt` package manager will emit index warnings such as `W: GPG error...` or `Signed file isn't valid, got 'NODATA'`. **Ignore these completely.** The mandatory `[trusted=yes]` flag instructs the system to ignore these warnings, keep the execution pipeline active, and ingest `contrib` branch package lists for subsequent installation.

**6.** Install the current stable release of VirtualBox, fully optimized for modern Linux kernels (the system pulls the authentic package over a secure TLS HTTPS channel):
```bash
sudo apt install virtualbox-7.2 -y
```

**7.** Add the current user account to the system virtualization management group to enable direct, pass-through access for guest operating systems to host USB ports (the `$USER` variable expands your username automatically):
```bash
sudo usermod -aG vboxusers $USER
```

> [!NOTE]
> During initial VirtualBox deployment on bare metal running active Secure Boot, the internal builder compiles modules in uncompressed `.ko` format, placing them under `/lib/modules/$(uname -r)/misc/`. 
> 
> Due to timing delays in updating the kernel dependency map, running `modinfo -n vboxdrv` may return a false-positive `ERROR: Module vboxdrv not found`. This is not an issue—the utility simply has not reindexed the new paths yet. 
> 
> The sole definitive indicator that Secure Boot successfully accepted the MOK key and loaded modules into kernel Ring 0 is inspecting active kernel memory:
> ```bash
> lsmod | grep vbox
> ``` 
> If the output lists `vboxdrv`, `vboxnetflt`, and `vboxnetadp`, the hypervisor is fully autonomous, hardware-isolated, and ready to host guest operating systems safely.

During system reboot, the blue-and-gray **Perform MOK management** screen will appear. Quickly press any key and complete the enrollment process step-by-step: **Enroll MOK** ➔ **Continue** ➔ **Yes** ➔ enter the password (configured previously via `mokutil`) ➔ **Reboot**.

**8.** Reboot the system and complete **Enroll MOK**:
```bash
systemctl reboot -i
```

**9.** Compile and initialize low-level virtualization drivers inside the Linux kernel:
```bash
sudo /sbin/vboxconfig
```

**10.** Prevent the virtual machine autostart service and the web API management daemon from launching at boot:
```bash
sudo systemctl disable --now vboxautostart-service && sudo systemctl disable --now vboxweb-service
```

> [!WARNING]
> Never configure a virtual machine network adapter to **Bridged Adapter** mode unless explicitly requiring un-VPNed network access within the guest OS. In Bridged mode, the guest OS (whether a suspicious Windows build or a testing Kali Linux instance) acquires a direct, unmanaged IP address on the host's physical local network. This exposes host home routers, network printers, and internal devices directly, introducing a severe local security breach.
> 
> Always verify settings to ensure virtual machine network adapters are bound to **NAT** or **Host-only** modes. **NAT** mode safely isolates guest OS traffic inside the host environment, routing all outbound connections through the UFW firewall's strict Kill Switch and the secure `tun0` VPN tunnel configured in earlier chapters.
>
> The **sole exception** to this operational rule is deploying the specialized anonymous OS *Whonix*. Its architecture relies on two isolated virtual machines with custom network bindings:
> 
> * **On Whonix-Gateway:** The primary network adapter accesses external networks via **NAT** (automatically wrapped in host-level VPN and UFW firewall rules), while the secondary adapter is assigned to an **Internal Network** labeled `whonix`.
> * **On Whonix-Workstation:** The single network adapter is similarly bound to the **Internal Network** on the same isolated `whonix` segment.
> 
> This architecture ensures the workstation lacks direct physical access to the local router or host system, forcing all outbound traffic through the Tor anonymous network via the isolated gateway.

<br>

## Shrinking and Optimizing VDI Virtual Disks

#### Introduction:

During active operation, virtual machine disk files naturally expand over time. Installing software or downloading data inside a guest OS causes the dynamically allocated `*.vdi` virtual disk file to grow on the physical host storage. However, deleting those files within the guest operating system does not automatically reduce the size of the `*.vdi` container on the physical drive.

This overhead occurs because the guest filesystem merely marks deleted sectors as "free" without physically clearing their contents. From the perspective of the VirtualBox hypervisor, those storage blocks still contain residual data. Reclaiming unused storage back to the physical host SSD requires manual disk zeroing and compaction.

#### Sanitizing a Windows Guest Virtual Machine:

**1.** Launch the target Windows virtual machine.
**2.** Download the official `SDelete` CLI utility directly from Microsoft `https://learn.microsoft.com/en-us/sysinternals/downloads/sdelete`.
**3.** Extract the `sdelete64.exe` binary (for 64-bit operating systems) and move it directly into the root directory of the `C:\` drive.
**4.** Open Command Prompt (`cmd.exe`) with elevated administrative privileges and execute the following command:
```cmd
C:\sdelete64.exe -z C:
```

**5.** Wait for the operation to complete (the utility forcibly writes binary zeroes across all unallocated disk space), then perform a complete shutdown of the Windows virtual machine.

> [!IMPORTANT]
> The `-z` flag in `SDelete` fills free storage exclusively with binary zeroes, which is a mandatory requirement for subsequent VirtualBox container compression. However, if the operational goal is forensic data destruction rather than disk space optimization, use the `-c` flag instead of `-z`.
> 
> The `-c` flag overwrites free space with random bit patterns adhering to the US Department of Defense *DoD 5220.22-M* sanitization standard. Note that applying the `-c` flag prevents VirtualBox compression routines from shrinking the `*.vdi` image, as random bit arrays are processed as valid payload data. Use `-z` exclusively for space optimization.

#### Sanitizing a Linux Guest Virtual Machine (Ubuntu/Kali Linux):

Instead of using the slow and aggressive method of filling the disk with zeroes via `dd` (which wears down the physical host SSD by writing hundreds of gigabytes of empty data), Linux virtual machines benefit far more from using the specialized `zerofree` utility. It targetedly identifies only modified blocks where files were deleted and zeroes them in seconds without unnecessary write endurance strain on the SSD.

To execute the utility, the guest filesystem must be unmounted or remounted in **Read-Only** mode. The easiest way to achieve this is via **Recovery Mode**. Configure the GRUB bootloader menu directly from the running guest system:

**1.** Inside the guest Linux environment, open the bootloader configuration file:
```bash
sudo nano /etc/default/grub
```

**2.** Locate the line `GRUB_TIMEOUT=0` and change its value to `5` (providing a 5-second window at boot to access the menu). Additionally, if `GRUB_TIMEOUT_STYLE=hidden` is active, comment it out by adding a `#` character at the beginning of the line. Save the file in `nano` with **"Ctrl + O"** ➔ **"Enter"**, then exit via **"Ctrl + X"**.

**3.** Update the bootloader configuration in the OS:
```bash
sudo update-grub
```

**4.** Reboot the virtual machine. Upon boot, the text-based GRUB menu will appear. Use the arrow keys to select the second entry: **"Advanced options for Ubuntu"**, press **"Enter"**, and from the subsequent list select the option appended with **"(recovery mode)"**.

**5.** The system will boot into a graphical recovery menu. Select **"drop to root shell prompt"** using the arrow keys and press **"Enter"**.

**6.** A root console will open at the bottom of the screen. Remount the root partition in read-only mode:
```bash
mount -o remount,ro /
```

**7.** Launch instantaneous zeroing of free filesystem blocks:
```bash
zerofree -v /dev/sda1
```

> [!TIP]
> **Author's Note:** Determine the precise name of the target root partition (for example, `/dev/sda1` or `/dev/nvme0n1p2`) beforehand from the running system using `df -h`. Once the zeroing process completes, perform a full shutdown of the virtual machine.

#### Final Virtual Disk Compaction on the Host Machine:

Now that the free space within the virtual disks has been zeroed out, open a terminal on the host Ubuntu system. Navigate to the directory containing the virtual machine files (for example, `~/VirtualBox VMs/`), and initiate the final compaction process.

> [!IMPORTANT]
> **Attention:** Linux terminal commands are case-sensitive. The VirtualBox management utility binary must be typed precisely as `VBoxManage`.

**1.** Display a detailed list of all registered virtual hard disks along with their unique UUIDs:
```bash
VBoxManage list hdds
```

**2a.** Compact the virtual disk using its UUID. If the drive's UUID is `21e5b710-6ed1-412f-6313-ac7e6251b3f3`, execute:
```bash
VBoxManage modifymedium --compact 21e5b710-6ed1-412f-6313-ac7e6251b3f3
```

**2b.** Compact the virtual disk directly using its file path:
```bash
VBoxManage modifymedium --compact "VM_NAME.vdi"
```

Once compaction completes, the virtual disk image files will immediately shrink by several gigabytes up to tens of gigabytes (depending on the volume of previously unallocated or deleted data), reclaiming physical storage on the main SSD.

<br>

## Installing and Configuring the Docker Containerization Platform

#### Introduction:

The VirtualBox virtualization environment detailed and configured in the previous chapter works exceptionally well for running heavy guest operating systems. However, modern offensive and defensive security workflows rely far more frequently on Docker containerization to deploy isolated utilities, vulnerable lab environments (like DVWA or WebGoat), and OSINT scripts.

Understand the core architectural impact: out-of-the-box Docker introduces a massive security blind spot on a hardened paranoid desktop. Running it in a secured environment without aggressive security tuning is outright fatal.

> [!NOTE]
> I still personally lean toward full-OS virtualization via traditional virtual machines, so Docker testing on Ubuntu 26.04 was performed only at a surface level. Container deployment was validated exclusively on Ubuntu 24.04.4.

#### What Is the Hidden Danger of Default Docker?

* **The Omnipotent Root Daemon:** By default, the Docker background service (`dockerd`) executes with unrestricted `root` privileges. Containers launch under superuser context. Should a critical vulnerability emerge within containerized software, an attacker can execute a sandbox escape (Container Escape) and instantly capture full control over the host Linux kernel.
* **Network Hijacking Bypassing UFW:** This represents the most dangerous architectural risk. Upon initialization, Docker creates its own network bridge and injects routing rules directly into the Linux kernel's `iptables/nftables` tables at the highest priority level, completely bypassing UFW rules. Exposing a service port via Docker (e.g., `-p 80:80`) causes Docker to open that port directly to the public internet, completely ignoring the Kill Switch and UFW rules. Traffic routes into the container directly via the physical interface, bypassing the active `tun0` VPN tunnel entirely. This is a classic, textbook OPSEC failure in practice.

To mitigate these threats, deploy a two-stage defensive strategy: transition Docker into secure Rootless Mode and strictly forbid it from autonomously modifying the host network stack.

To maintain absolute system hygiene, rely exclusively on the standard APT package manager while locking down official, verified Canonical update mirrors. This prevents the system from pulling untrusted third-party binaries from external PPA repositories. Pay strict attention to release codenames: **Ubuntu 24.04 LTS is Noble Numbat** (`noble`), while **Ubuntu 26.04 LTS is Resolute Raccoon** (`resolute`).

#### Deploying Docker in Rootless Mode:

Rootless Mode forces the Docker daemon and all child containers to execute entirely within an isolated User Namespace (`userns`). The daemon runs strictly under an unprivileged user context. Even if an attacker compromises a container and achieves "root" within the sandbox, the host operating system still treats the process as an unprivileged local user, denying any access to raw system files.

**1.** To enforce verified official mirrors on modern Ubuntu releases, open the DEB822-formatted repository configuration file using a text editor with elevated privileges:
```bash
sudo nano /etc/apt/sources.list.d/ubuntu.sources
```

**2.** Verify that the `URIs` field strictly points to official mirror endpoints (`http://archive.ubuntu.com/ubuntu/` and `http://security.ubuntu.com/ubuntu/`) matching your operating system release codename (`noble` for 24.04 or `resolute` for 26.04), mitigating untrusted third-party attack vectors.

**3.** Refresh local APT package indices and install the upstream Docker engine along with user-space networking components, network encapsulation utilities, and `curl` from Canonical's trusted mirror:
```bash
sudo apt update && sudo apt install docker.io docker-buildx docker-compose-v2 docker-doc uidmap dbus-user-session slirp4netns fuse-overlayfs curl -y
```

**4.** Disable and stop the host-level root Docker service to prevent background daemon execution at boot:
```bash
sudo systemctl disable --now docker.service docker.socket
```

**5.** Mask the system root service and its listening socket, symlinking them directly to `/dev/null` so external system triggers cannot activate the privileged daemon:
```bash
sudo systemctl mask docker.service docker.socket
```

**6.** Bypass the restrictive default policy in Ubuntu 24.04/26.04 LTS by disabling the global kernel restriction on unprivileged user namespaces, locking the rule into the host's `sysctl` configuration to persist across system reboots:
```bash
sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0 && echo 'kernel.apparmor_restrict_unprivileged_userns=0' | sudo tee /etc/sysctl.d/99-rootless-docker.conf
```

**7.** Execute the official, independent rootless environment setup script directly from its upstream source (run strictly under your unprivileged user account without `sudo`):
```bash
curl -fsSL https://get.docker.com/rootless | sh
```

**8.** Append paths for isolated rootless binaries and the user-space Docker socket to your shell configuration file—dynamically resolving your user ID via `$UID`—then reload the current environment:
```bash
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc && echo 'export DOCKER_HOST=unix:///run/user/$UID/docker.sock' >> ~/.bashrc && source ~/.bashrc
```

**9.** Grant system authorization to preserve long-running user processes in the background after terminating the active terminal session:
```bash
loginctl enable-linger $USER
```

**10.** Reload the user-space `systemd` daemon configuration and enable the isolated rootless Docker service on boot:
```bash
systemctl --user daemon-reload && systemctl --user enable --now docker.service
```

**11.** Perform a final audit on the containerization engine to confirm that Docker explicitly reports active rootless status:
```bash
docker info | grep -i rootless
```

#### Securing Docker Networking: Preventing UFW Firewall Bypass:

Now for the critical security enforcement: revoke Docker's ability to manipulate kernel routing tables completely and force its network traffic to obey host UFW firewall rules. At this stage, re-enable the network interface in NetworkManager.

**1.** Create a hidden configuration directory and open the Docker daemon configuration file under the local user profile:
```bash
mkdir -p ~/.config/docker/ && nano ~/.config/docker/daemon.json
```

**2.** Insert the JSON payload to strip Docker of `iptables/nftables` modification privileges while enforcing privacy-focused, non-logging Quad9 DNS servers. Save via **"Ctrl + O"** ➔ **"Enter"** and exit with **"Ctrl + X"**:
```json
{
  "iptables": false,
  "dns": ["9.9.9.9", "149.112.112.112"]
}
```

**3.** Restart the user-space Docker daemon to apply network restrictions:
```bash
systemctl --user restart docker.service
```

**4.** Selectively allow UFW packet forwarding (`FORWARD`) exclusively for the isolated Docker subnet based on active network architecture:

* **If operating WITH an active VPN via `tun0`:**
```bash
sudo ufw route allow in on lo out on tun0 from 172.17.0.0/16
```
* **If operating DIRECTLY via physical NIC (replace `enp0s1` with target interface name):**
```bash
sudo ufw route allow in on lo out on enp0s1 from 172.17.0.0/16
```

**5.** Open UFW's low-level post-routing and filtering rules configuration file:
```bash
sudo nano /etc/ufw/before.rules
```

**6.** Scroll to the bottom, append a single blank line right after the final default `COMMIT` statement (which closes the main filter table), and append an isolated NAT rule block to masquerade the Docker subnet and force traffic through the designated interface. Save and close:

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
# Route and masquerade Rootless Docker traffic DIRECTLY through physical NIC (replace enp0s1 with target interface name)
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 172.17.0.0/16 -o enp0s1 -j MASQUERADE
COMMIT
```

**7.** Reload UFW to apply low-level NAT modifications, isolate the subnet, and update routing tables:
```bash
sudo ufw reload
```

**8.** Force NetworkManager to re-read physical network interface configurations to restore hypervisor gateway connectivity post-firewall activation (replace `enp0s1` with target interface name):
```bash
sudo nmcli device reapply enp0s1
```

**9.** Verify outbound WAN connectivity by executing an application-layer TCP request through the firewall and Portmaster eBPF filters (raw ICMP/ping is intentionally bypassed as hardened network profiles drop raw sockets for CLI binaries):
```bash
curl -I https://google.com
```

**10.** Restart Portmaster to re-bind eBPF socket-interception hooks and enforce kernel-level control over unprivileged daemon activity:
```bash
sudo systemctl restart portmaster
```

**11.** Manually launch the Portmaster GUI from the application desktop menu (**"Show Apps"**); otherwise, the kernel eBPF driver remains in a strict lock state, dropping outbound system traffic until the GUI user-session initializes.

Acknowledge the prompt by clicking "Allow" on Portmaster's pop-up alert. Absolute perimeter control is now established: UFW masquerades and routes Docker traffic strictly through the chosen network interface (bound mandatorily to the VPN tunnel in operational environments), Portmaster intercepts telemetry in real time, and Docker is physically contained within host firewall parameters—incapable of autonomously exposing external host ports.

#### Hardened Container Deployment in Practice:

Stripping root privileges and restricting network routing provide essential baseline protection. However, when deploying specific containers, implement additional hardening flags to constrain process permissions within the sandbox.

**1.** Deploy a reference Nginx web server container under strict isolation constraints. Note that prefixing the port binding with `127.0.0.1:` serves as the primary network boundary, locking the exposed socket strictly to the local loopback interface (`localhost`). Additionally, enforce a read-only root filesystem (`--read-only`), explicitly block process privilege escalation, and mount isolated temporary RAM filesystems for essential runtimes:
```bash
docker run -d --name secure_web -p 127.0.0.1:8080:80 --read-only --security-opt=no-new-privileges --tmpfs /tmp --tmpfs /var/cache/nginx --tmpfs /run nginx
```

**2.** Inspect active listening sockets on the host machine to confirm that the socket is bound exclusively to `localhost` and owned solely by the `rootlesskit` process:
```bash
ss -tulpn | grep 8080
```

#### Experimental Proof of Security (Verifying Non-Root Execution):

To definitively confirm that the container is fully isolated and lacks superuser privileges on the host system, conduct a practical security experiment. Simulate an attacker attempting to compromise the underlying system by creating files under the context of an "internal" root user.

**1.** Create a clean local directory on the host machine to log experiment results:
```bash
mkdir -p ~/host_share
```

**2.** Launch an isolated Alpine Linux container, mount the created directory inside the sandbox via the volume flag `-v`, and generate a payload file from within the containerized "root" context:
```bash
docker run --rm -v ~/host_share:/tmp/container_share alpine touch /tmp/container_share/evil_payload.txt
```

**3.** Inspect real file ownership attributes directly on the host filesystem:
```bash
ls -l ~/host_share/evil_payload.txt
```
*This demonstrates the fundamental security mechanics of User Namespaces in practice. The output reveals file ownership as `user user`. The Linux kernel dynamically remapped process identifiers: the containerized "pseudo-root" is recognized by the underlying OS as a completely unprivileged user process, incapable of writing root-owned binaries to host storage. Container escapes under this architecture are rendered technically impossible.*

**4.** Completely purge all testing artifacts from the disk:
```bash
rm -rf ~/host_share
```

> [!NOTE]
> **Important Orchestration Note:** Unlike an isolated Nginx web server, the Portainer management interface requires continuous database writes and logging to persistent storage, rendering the `--read-only` flag inapplicable. Instead, Portainer security is built on strict loopback interface binding (`localhost`), process privilege escalation restriction, and execution via the unprivileged user-space rootless socket.

**5.** Deploy the Portainer web management interface in a hardened configuration: strictly bind listening ports to `localhost` (`127.0.0.1:`), block process privilege escalation, and dynamically mount the unprivileged user-space socket using the system `$UID` variable:
```bash
docker run -d --name portainer --restart always -p 127.0.0.1:9443:9443 --security-opt=no-new-privileges -v /run/user/$UID/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

**6.** Re-inspect host listening sockets to verify that Portainer's administrative web interface (port 9443) is bound exclusively to 127.0.0.1 and completely shielded from external network scanning:
```bash
ss -tulpn | grep 9443
```

> [!WARNING]
> Transporting this configuration from an isolated virtual machine directly onto a bare-metal host fundamentally alters the threat model. To avoid compromising host OS integrity, strictly enforce three mandatory rules:
> 
> 1. **Avoid global sysctl overrides on the host:** Never execute `sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0` globally on a bare-metal host environment. Disabling this restriction opens security surface area to any malware. On bare-metal hosts, Rootless environments must execute *strictly* via targeted AppArmor profiles tailored for the `rootlesskit` binary.
> 2. **Enforce directory mount hygiene (the `-v` flag):** Never mount the host root partition (`/`) or home directory root (`~`) inside containers. In the event of a container escape, an adversary—even while restricted by Rootless Mode boundaries—gains immediate read, write, and deletion access to local documents, SSH keys, and stored credentials on the physical machine.
> 3. **Implement account isolation:** The optimal host security posture requires provisioning a dedicated unprivileged service user (e.g., `isolated-docker`) without `sudo` privileges, running Rootless Docker strictly within that isolated user context. This enforces total segregation between container runtimes and the primary workstation account.

<br>

## Installing and Configuring the AIDE File Integrity Monitoring System

#### Introduction:

A powerful tool for host internal security monitoring is AIDE (*Advanced Intrusion Detection Environment*)—an advanced host-based intrusion detection system (HIDS). It performs continuous filesystem monitoring across Linux to detect stealthy malware, rootkits, and unauthorized adversary activity in real time.

The architecture of AIDE relies on generating a digital baseline snapshot (a cryptographic hash database) of a clean operating system state, against which current filesystem attributes are routinely compared. This instantaneously pinpoints exactly which binaries or configuration files were modified, deleted, or introduced. To calculate these baselines, the system leverages strong hashing algorithms, including SHA-256 and SHA-512.

> [!IMPORTANT]
> Deploying and initializing the primary AIDE database must be executed at the absolute end of host deployment—strictly after installing and fully hardening all necessary tooling (VPN, Portmaster, VeraCrypt, Firejail). This guarantees that legitimate binaries and configs are indexed into the reference "clean" system snapshot, completely preventing a flood of false positives during routine integrity checks.

#### Installing and Configuring AIDE:

Open the terminal under an unprivileged user account and proceed with the installation.

**1.** Install the file integrity monitoring system:
```bash
sudo apt update && sudo apt install aide -y
```

**2.** Create a custom configuration snippet to exclude noisy runtime directories from overall system integrity auditing:
```bash
sudo nano /etc/aide/aide.conf.d/99_custom
```

**3.** Insert custom security exclusion rules into the empty file. Explicitly restrict AIDE from scanning rapidly changing temporary directories, caches, system logs, and Portmaster eBPF firewall databases to completely prevent false positive alerts:
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

To save the configuration in `nano`, press **"Ctrl + O"** ➔ **"Enter"**, then **"Ctrl + X"** to exit back to the terminal.

Native AIDE exclusion rules (negation rules) must be formatted without spaces! Do not insert a space between the exclamation mark `!` and the initial path slash `/`; otherwise, the parser will fail with a syntax error.

**4.** Rebuild the global system configuration file from the modular snippets and generate the primary baseline cryptographic snapshot (computing SHA-512 hashes across large storage volumes may take considerable time):
```bash
sudo aideinit
```

**5.** Copy the newly generated database into position as the primary active baseline (the `-p` flag preserves original file permissions):
```bash
sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
```

On Ubuntu systems, AIDE database files must remain compressed using gzip and retain the `.gz` file extension.

**6.** Run an initial integrity audit against the host filesystem:
```bash
sudo aide -c /etc/aide/aide.conf --check
```

Normally, the audit output would confirm zero integrity violations—indicating that the active database perfectly matches the current filesystem state. However, due to complex runtime dependencies, minor diffs will appear. Tracked modifications will report under `/home/$USER/` and its nested subdirectories, including `/.config/dconf/*`, `/.config/tiling-assistant/*`, `/.local/share/`, `.bash_history`, and others.

#### Executing a Penetration Test (Validating Defense Mechanisms):

Verify that the host intrusion detection system functions as expected. Simulate a covert payload drop inside a restricted superuser system directory:

**1.** Plant a simulated backdoor file inside the protected `/root` directory:
```bash
sudo touch /root/test_virus.txt
```

**2.** Execute a manual filesystem integrity check:
```bash
sudo aide -c /etc/aide/aide.conf --check
```

AIDE instantaneously detects unauthorized alterations within the directory structure, flags the hidden file, highlights the alert, and logs the precise timestamp of creation.

When system changes occur legitimately (e.g., intentionally upgrading or installing a binary via the package manager), refresh the cryptographic baseline database:

**3.** Recalculate file hashes and generate an updated baseline database:
```bash
sudo aideinit
```

**4.** Promote the newly generated database to serve as the active reference snapshot:
```bash
sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
```

**5.** Lock the database file (prohibiting modifications or deletion, even by the `root` account):
```bash
sudo chattr +i /var/lib/aide/aide.db
```

**6.** Unlock the database file (required prior to updating the baseline after running `apt upgrade`):
```bash
sudo chattr -i /var/lib/aide/aide.db
```

> [!WARNING]
> Keep in mind a fundamental logical limitation inherent to all local host-based integrity control systems. Should an adversary successfully breach every defensive boundary (UFW, AppArmor, Firejail) and achieve full root privileges on the operating system, they can neutralize AIDE's protections. An attacker can simply execute `sudo aide --update` immediately after dropping a malicious payload, effectively legitimizing the changes within the local database.
> 
> To enforce strict, uncompromised integrity for the database file, immediately following Step 4, copy the active `/var/lib/aide/aide.db.gz` file onto an air-gapped physical USB drive equipped with a hardware **Write-Protect** switch.

During routine audits, mount this write-protected USB drive in read-only mode and execute the scan using the path to the protected external database file:

**7.** Run an integrity check referencing an externally secured baseline database:
```bash
sudo aide --config=/media/user/secure_flash/aide.conf --check
```

Replace `/media/user/secure_flash/` with the actual mount path of the write-protected USB drive on your system. This strategy renders any adversary attempt to tamper with or re-legitimize disk modifications completely futile.

> [!NOTE]
> By default, Ubuntu's native AIDE detection rules enforce strict auditing (utilizing `Hbrps` and `High` macros). The engine verifies not only changes in file size, but also `inode` numbers, hard link counts, extended access attributes (`Mtime`/`Ctime`), and, most importantly, SHA-256/SHA-512 cryptographic hashes. This completely neutralizes Trojan horse attacks, where critical system binaries (such as `/usr/bin/sudo` or `/bin/ls`) are replaced with malicious variants crafted to match the original file size.
  
<br>

## Automated System Security Auditing with Lynis

To finalize the deep hardening of the base operating system, conduct a comprehensive independent security audit of the current deployment. For this task, leverage Lynis—a professional automated scanner. Installing the `lynis` package via standard `apt` repositories is strongly discouraged: distribution repositories lag behind, triggering false positives and missing novel attack vectors. Instead, deploy the scanner directly from the developers' official Git repository to ensure maximum signature freshness and preserve absolute OS package hygiene.

Because the scanner deploys temporary binary modules inside the runtime directory during execution, immediately remove the utility upon completion and securely erase all local report files using `shred`.

**1.** Create a hidden directory under the user home path and populate it with a custom exclusion profile heavily optimized for desktop threat models. This isolates the runtime from irrelevant server-level checks, false GRUB warnings, and password rotation policies, focusing scan runtime strictly on actionable local vulnerabilities:
```bash
mkdir -p ~/.config/lynis && nano ~/.config/lynis/custom.prf
```

**2.** Insert custom exception rules to suppress server-oriented audit modules:
```ini
# --- Exceptions for Desktop setups with YubiKey and Encryption ---

# Disable password expiration policy checks (90-day password rotation is unnecessary on a desktop)
skip-test=AUTH-9222
skip-test=AUTH-9226
skip-test=AUTH-9282
skip-test=AUTH-9286

# Disable account lockout policy requirements during brute-force attempts (faillock/tally)
skip-test=AUTH-9230

# Suppress false positive GRUB warnings (configured independently via custom.cfg)
skip-test=BOOT-5122

# Suppress server-oriented ban, restriction, and PAM utilities (redundant with hardware tokens)
skip-test=DEB-0880
skip-test=AUTH-9229
skip-test=KRNL-5820

# Partition layout warnings (irrelevant under full LUKS disk encryption)
skip-test=FILE-6310

# Disable USB port restriction checks (essential for workstation peripheral usage)
skip-test=USB-1000

# Suppress uncommon network protocol auditing
skip-test=NETW-3200

# Suppress legal console login banners (unnecessary for personal workstations)
skip-test=BANN-7126
skip-test=BANN-7130

# Suppress remote log aggregation checks (SIEM integration)
skip-test=LOGG-2154

# Disable continuous process auditing systems (prevents heavy CPU and battery drain on laptops)
skip-test=ACCT-9622
skip-test=ACCT-9626
skip-test=ACCT-9628

# Suppress domain DNS audit checks
skip-test=NAME-4028

# Suppress configuration management framework checks (Ansible/Puppet—redundant on a standalone PC)
skip-test=TOOL-5002

# Suppress compiler restrictions (which would prevent user-level software builds)
skip-test=HRDN-7222

# Suppress pre-installation APT bug notification alerts
skip-test=DEB-0810
skip-test=TIME-3104
skip-test=PKGS-7394
skip-test=PKGS-7396

# Suppress strict kernel module loading prohibitions (avoids breaking Ledger/YubiKey hardware drivers)
skip-test=KRNL-5788
skip-test=KRNL-5622

# Suppress IPTables auditing (network controls are already configured independently)
skip-test=FIRE-4513

# Suppress desktop file/folder permission auditing (permissions were assigned during manual setup)
skip-test=FILE-7524

# Suppress AIDE hash algorithm warnings (default 'H' macro enforces maximum checksum coverage)
skip-test=FINT-4402

# Suppress deep systemd service configuration auditing (unnecessary overhead for desktop environments)
skip-test=SRV-2300

# Suppress server-level update and service restart prompts
skip-test=PKGS-7394
skip-test=PKGS-7396

# Suppress recommendations for scheduled debsums cron execution
skip-test=PKGS-7370
```

> [!NOTE]
> This custom Lynis exclusion profile is specifically tailored for a hardened desktop environment protected by YubiKey hardware tokens and LUKS full-disk encryption. Suppressing server-centric constraints (password expiration, USB lockdowns) and system audit daemons allows the scanner to focus strictly on realistic local workstation attack vectors.

**3.** Clone the latest upstream Lynis release directly from the official repository into an isolated temporary directory (`/tmp/`) on the host:
```bash
sudo apt update && sudo apt install git && git clone https://github.com/CISOfy/lynis.git /tmp/lynis
```

**4.** Executing a thorough audit of the kernel and system logs requires elevated privileges. Switch to an interactive `root` session:
```bash
sudo -i
```

**5.** **Critical Security Step:** Because the repository was cloned under an unprivileged user context, Lynis's paranoid strict-security engine will abort execution with a fatal permission error when run as `root`. Reassign ownership of the temporary directory to the superuser:
```bash
chown -R root:root /tmp/lynis
```

**6.** Navigate to the utility directory and execute a full system security audit in standard interactive mode, explicitly passing the custom desktop profile:
```bash
sh -c "cd /tmp/lynis && ./lynis audit system --profile /home/$SUDO_USER/.config/lynis/custom.prf"
```

*(The `$SUDO_USER` environment variable dynamically resolves your primary username to locate the custom configuration profile).*

During execution, the scanner streams audit results to the stdout console. Interpret the color-coded markers as follows:
* **Green Markers** (*OK/Success*)—Parameters are properly hardened; no vulnerabilities detected.
* **Yellow Markers** (*Warnings/Suggestions*)—Non-critical warnings or debatable configurations requiring review.
* **Red Markers** (*Critical/Danger*)—Critical security risks that demand immediate remediation.

At the conclusion of the audit run, Lynis outputs an overall numerical percentage score (**Hardening Index**) alongside an itemized list of specific recommendations (**Suggestions**), each tagged with a unique alphanumeric identifier. Querying these codes on the official project portal (`https://cisofy.com`) provides actionable remediation steps for each reported finding.

Once the audit review is complete, purge the scanner and all generated log files from the host filesystem to eliminate any residual forensic trace of the security assessment.

> [!WARNING]
> Storing unencrypted scan logs and audit reports on disk is strictly forbidden. Should an account compromise occur, an adversary could leverage these detailed logs as a read-made roadmap targeting residual system weaknesses and configuration quirks.

**7.** Terminate the `root` interactive session and return to your unprivileged user account:
```bash
exit
```

**8.** Overwrite and erase local report files, logs, and the scanner repository directory using a 3-pass `shred` pattern before purging the host temporary directory:
```bash
find /tmp/lynis/ -type f -exec shred -v -u -z -n 3 {} \; && rm -rf /tmp/lynis
```

> [!IMPORTANT]
> Expect Lynis to report several yellow or red findings (*Suggestions*) even after applying extensive kernel, access control, and network hardening measures. This behavior is expected and legitimate: the Lynis assessment platform is engineered primarily around high-availability corporate Linux servers.
> 
> Consequently, on a hardened desktop setup, the scanner naturally triggers warnings for absent server infrastructure—such as local MTA daemons (*Postfix/Sendmail*) or dedicated log aggregation daemons (*Syslog-ng*). On a personal security workstation, these background services introduce unnecessary risk by opening additional network sockets and expanding attack surface area. They were omitted deliberately.
> 
> The primary metric is achieving a desktop **Hardening Index** above **75%**, which represents an exceptionally strong security posture for a standalone personal workstation.

This completes the overall security configuration and host-level hardening of the base Ubuntu Desktop operating system. The following chapter covers isolated environment deployment, guest OS provisioning inside VirtualBox, and safe hardware cryptocurrency wallet passthrough using Ledger devices.

<br>

## Configuring Ubuntu/Xubuntu/Lubuntu Guest Systems in VirtualBox

#### Installing Guest Additions:

Following a successful deployment and initial boot of a guest Ubuntu operating system (or lightweight derivatives like Xubuntu/Lubuntu) within a virtual machine, the immediate priority is installing the official *VirtualBox Guest Additions* package. This enables hardware video acceleration, smooth UI performance, bidirectional clipboard sharing, and dynamic display auto-resizing when adjusting the window parameters.

In the top menu bar of the VirtualBox window, navigate to **"Devices"** ➔ **"Insert Guest Additions CD image..."**. Then, open the terminal inside the guest OS and execute the following steps in sequence:

**1.** Update local repository indices and install baseline compilation toolchains along with the `bzip2` archiver (forcing an update of its underlying dependencies):
```bash
sudo apt update && sudo apt install -y gcc make perl dkms tar build-essential libbz2-1.0 bzip2
```

**2.** Dynamically pull the exact kernel headers corresponding to the currently active Linux kernel (leveraging environmental variable expansion to guarantee copy-paste compatibility):
```bash
sudo apt install -y linux-headers-$(env uname -r)
```

> [!WARNING]
> Modern Linux distributions enforce security hardening policies that mount optical drives and home partitions with the strict `noexec` flag (prohibiting binary execution), or restrict direct script invocation under superuser contexts. Launching the installer directly off the mounted media causes the Linux kernel to throw a deceptive *«failed to open/No such file or directory»* error—even when the file is visibly present. To bypass this restriction, copy the setup binary into the RAM-backed temporary directory (`/tmp`) and explicitly execute it via the `sh` shell interpreter:

**3.** Identify the block device designation assigned to the mounted Guest Additions optical media (typically `sr0`):
```bash
lsblk
```

**4.** Unmount any existing stale mount points, force-mount the optical device to `/mnt`, copy the setup installer into the system temporary directory using `sudo`, change directory into `/tmp`, and execute driver compilation:
```bash
sudo umount /mnt 2>/dev/null; sudo mount /dev/sr0 /mnt && sudo cp /mnt/VBoxLinuxAdditions.run /tmp/ && cd /tmp/ && sudo sh ./VBoxLinuxAdditions.run
```
*(Note: Explicitly using `sudo` during the file copy step is required to read contents from the mounted optical media owned by `root`, while executing out of `/tmp` successfully bypasses `noexec` mount restrictions).*

**5.** Reboot the virtual machine to complete kernel module initialization and load the newly compiled VirtualBox drivers:
```bash
sudo reboot now
```

#### Installing Mozilla Firefox:

In certain minimal Linux desktop flavors (such as Lubuntu), a pre-installed web browser may be completely absent by default. Deploy the official classic build of the Mozilla Firefox browser, bypassing default Snap packages and third-party PPA repositories via direct standalone extraction:

**6.** Download the latest binary archive of the stable Firefox release directly into the root of the home directory:
```bash
wget -O ~/FirefoxSetup.tar.bz2 "https://download.mozilla.org/?product=firefox-latest-ssl&os=linux64&lang=en-US"
```

**7.** Extract the downloaded archive directly into the current user's home directory (strictly without `sudo` privileges), preserving native file permissions and filesystem security constraints:
```bash
tar xjf ~/FirefoxSetup.tar.bz2 -C ~/
```

This creates a clean `firefox` directory inside your personal home path, containing the self-contained `firefox` executable binary. The browser is fully prepared for its initial standalone launch and subsequent deep, uncompromising privacy tuning via the `about:config` engineering menu, as detailed in the previous chapters of this book.

#### Configuring Shared Folders in VirtualBox:

Shared Folders serve as the primary mechanism for securely exchanging configuration files, scripts, and audit logs between the isolated guest environment and the host system. By default, Ubuntu's access control policies restrict unprivileged access to hypervisor-mounted directories.

To grant read and write permissions **inside the guest virtual machine**, execute the following steps in the terminal:

**1.** Add the current active user to the trusted VirtualBox system group using a dynamic variable:
```bash
sudo usermod -aG vboxsf $USER
```
*(Note: On a Windows host, directory permissions are handled automatically by the hypervisor installer; access control enforcement must be configured strictly inside the guest Linux OS).*

**2.** Refresh the current user session to re-evaluate group memberships without requiring a full system reboot:
```bash
su - $USER
```

> [!NOTE]
> When adding a shared directory in the VirtualBox GUI settings, always enable both the **"Auto-mount"** and **"Make Permanent"** options. This ensures the shared folder automatically mounts on system boot under the `/media/sf_FOLDER_NAME/` directory path.

<br>

#### Installing Ledger Live in VirtualBox with Ubuntu/Xubuntu/Lubuntu:

To establish secure control over cryptocurrency assets, deploy the official Ledger Live application suite. Open the browser and download the latest stable Linux package directly from the official developer servers: `https://download.live.ledger.com/latest/linux`.

Once the download completes, open a system terminal inside the guest OS and execute the following steps in sequence:

**1.** Provision a dedicated directory within the user home path to isolate cryptographic software:
```bash
mkdir ~/ledger_live
```

**2.** Change directory into the system downloads location where the executable payload was stored:
```bash
cd ~/Downloads
```

**3.** Relocate the downloaded package into the target directory (the wildcard character `*` dynamically resolves any version string):
```bash
mv ledger-live-desktop-*-linux-x86_64.AppImage ~/ledger_live/
```

**4.** Change directory into the workspace path and explicitly grant executable permissions to the binary payload:
```bash
cd ~/ledger_live && chmod +x ledger-live-desktop-*-linux-x86_64.AppImage
```

**5.** Fetch and apply the official hardware `udev` rules to the Linux kernel for Ledger devices:
```bash
wget -q -O - https://raw.githubusercontent.com/LedgerHQ/udev-rules/master/add_udev_rules.sh | sudo bash
```

> [!IMPORTANT]
> Omitting this step prevents the guest operating system and the VirtualBox hypervisor from identifying or interfacing with the hardware wallet over the USB bus.

**6.** Install the user-space filesystem mounting library required by modern Ubuntu releases (mandatory for Ubuntu 24.04/26.04 LTS environments):
```bash
sudo apt install libfuse2t64 && sudo apt install fuse3 -y
```

> [!NOTE]
> Without this runtime dependency, self-contained `AppImage` binary packages fail to initialize and execute.

**7.** Launch Ledger Live within the isolated guest environment:
```bash
./ledger-live-desktop-*-linux-x86_64.AppImage
```

> [!WARNING]
> Configuring `udev` rules alone is insufficient for the Ledger Live instance inside the guest VM to establish a connection with the physical device. Connect the Ledger wallet via USB cable to the host machine, enter your PIN code directly on the hardware unit, and navigate into the target application interface (e.g., *Bitcoin* or *Ethereum*). 
> 
> Once unlocked, right-click the USB icon in the bottom-right corner of the active VirtualBox window and select the Ledger device entry from the pop-up menu. The hypervisor detaches the device from the physical host OS and passes the raw USB bus connection directly into the isolated virtual machine.

<br>

#### Running Ledger Live on the Main Host System (Ubuntu)

If you need to run Ledger Live directly on the primary host operating system rather than within a virtual machine, download the Linux binary via your browser from `https://download.live.ledger.com/latest/linux` into the home `Downloads` directory.

**1.** Install the required Fuse runtime libraries:
```bash
sudo apt install libfuse2t64
```

**2.** Launch the Ledger Live AppImage container:
```bash
./ledger-live-desktop-*-linux-x86_64.AppImage --no-sandbox
```

And on this cryptographic note, we conclude the construction of our secure, hardened digital architecture.

**Stay tuned and Hack the Planet!** 🚀

<br>
<br>
<br>

## About the Author & Legal Information

**Author:** EugeXo  
**Specialization:** Information Security, Linux Hardening, OPSEC.

#### Contact Information & Community Resources:

* **GitHub:** `https://github.com/EugeXo/`
* **Telegram:** `@EugeXoSecurity`
* **Jabber:** `eugexo@paranoici.org`
* **Email:** `eugexo@proton.me`

> [!NOTE]
> This guide is a completely independent, non-commercial open-source initiative. It was authored not for financial gain, but to consolidate practical field experience and provide the security community with a verified, reliable blueprint for building a trusted digital environment.
> 
> All materials are distributed freely and openly. If this guide saved you time, spared you sleepless nights, or protected your personal data, its purpose has been fulfilled!