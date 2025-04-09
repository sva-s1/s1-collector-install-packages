# s1-collector-install-packages

[![Latest Release](https://img.shields.io/github/v/release/sva-s1/s1-collector-install-packages)](https://github.com/sva-s1/s1-collector-install-packages/releases)
[![Issues](https://img.shields.io/github/issues/sva-s1/s1-collector-install-packages)](https://github.com/sva-s1/s1-collector-install-packages/issues)
[![License](https://img.shields.io/github/license/sva-s1/s1-collector-install-packages)](https://github.com/sva-s1/s1-collector-install-packages/blob/main/LICENSE)

---

## Overview

This repository provides alternative methods to acquire and install the **SentinelOne Collector (formerly Scalyr Agent)** RPM packages in scenarios where you cannot use the official shell script or a direct YUM/DNF repository—especially helpful for **air-gapped** or network-restricted environments.

> **Note:** These instructions focus on **RHEL-like** environments. We plan to expand to other operating systems soon!

---

## Problem Statement

Many organizations need a straightforward way to install the SentinelOne Collector in secure, offline (air-gapped) environments. The official repository and installer scripts often assume direct internet connectivity or a fully functional package manager configured to reach public endpoints. When this isn’t possible, you need a reliable, alternative approach to obtain the RPM files, verify their integrity, and install them locally.

---

## The Solution

### 1. Determine the Latest Version

- You can look up the **current version** in the [SentinelOne Collector GitHub repo](https://github.com/scalyr/scalyr-agent-2) or check the official [SentinelOne Collector documentation](https://community.sentinelone.com/s/topic/0TO69000000as2qGAA/sentinelone-collector).
- For example, as of this writing, a recent RPM file is:
  ```
  scalyr-agent-2-2.2.18-1.noarch.rpm
  ```

Below is an updated **Solution** section for your README, breaking out the installation methods into clear sub-steps (2.1 and 2.2). Adjust the numbering as desired.

### 2. Acquire the RPM File

#### 2.1 Download via cURL (Mac/Linux)

If you already know the **exact filename**, you can simply use `curl`:

```bash
curl -O https://app.scalyr.com/scalyr-repo/stable/latest/scalyr-agent-2-2.2.18-1.noarch.rpm
```

This downloads the **RPM** from the SentinelOne Collector (Scalyr) repo directly.  
Use this method if you want a quick download from a machine that **does** have internet access but isn’t necessarily a RHEL system.

#### 2.2 Download from GitHub Releases

Alternatively, you can download the **RPM** attached to this repository’s [Releases](https://github.com/sva-s1/s1-collector-install-packages/releases) page. Just:

1. Click on the **Releases** tab to the right (or at the top).
2. Locate the **latest release** containing the `.rpm` asset.
3. Download the RPM file from the “Assets” section.

> **Tip**: This repository hosts the RPM file for convenience when you want to move it into air-gapped environments.

### 3. Transfer to Air-Gapped Systems

Once you have the `.rpm` file, copy it into your air-gapped environment via USB, SSH, or whichever secure method you prefer.

### 4. Install the RPM Locally

Inside your air-gapped Linux system, install the RPM:

```bash
sudo rpm -ivh scalyr-agent-2-2.2.18-1.noarch.rpm
```

If you want to verify GPG signatures, you can also import the GPG key before installing:

```bash
sudo rpm --import https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x84AC559B5FB5463885CE0841F70CEEDB4AD7B6C6
sudo rpm --checksig scalyr-agent-2-2.2.18-1.noarch.rpm
sudo rpm -ivh scalyr-agent-2-2.2.18-1.noarch.rpm
```

> For **legacy RHEL** or special distributions that need alternate dependencies, consult official SentinelOne docs to confirm library requirements and package compatibility.

---

## References

1. **Official SentinelOne Collector Docs**  
   [https://community.sentinelone.com/s/topic/0TO69000000as2qGAA/sentinelone-collector](https://community.sentinelone.com/s/topic/0TO69000000as2qGAA/sentinelone-collector)

2. **GitHub – Scalyr Agent 2 Source**  
   [https://github.com/scalyr/scalyr-agent-2](https://github.com/scalyr/scalyr-agent-2)

3. **Installing Without the Shell Script**  
   [https://community.sentinelone.com/s/article/000006802](https://community.sentinelone.com/s/article/000006802)

4. **GPG Key**  
   [https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x84AC559B5FB5463885CE0841F70CEEDB4AD7B6C6](https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x84AC559B5FB5463885CE0841F70CEEDB4AD7B6C6)

---

## Coming Soon

- **Additional OS Versions**: We will add `.deb` packages (for Debian/Ubuntu) and instructions for other OSes.

---

## Contributing

We appreciate feedback and PRs! Please open an [issue](https://github.com/sva-s1/s1-collector-install-packages/issues) or submit a pull request if you’d like to improve these instructions.

---

## Disclaimer

This README is provided by SentinelOne solution engineering as a convenience. Always refer to official SentinelOne documentation for the most up-to-date and authoritative guidance. Use at your own discretion, and consult your SentinelOne sales engineer or support representative for in-depth assistance.
