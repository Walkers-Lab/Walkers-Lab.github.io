---
title: "Download ISO Files to an ESXi Datastore via SSH"
date: 2023-08-04 22:36:00 +0100
categories:
  - VMware
tags:
  - ESXi
  - SSH
  - VMware
  - vSphere
  - Datastore
  - wget
excerpt: "Use wget over SSH to download ISO files directly to a VMware ESXi datastore, avoiding the need to download locally and re-upload."
header:
  teaser: /assets/images/esxi-download-iso-files-via-ssh/teaser.png
---

When building virtual machines on ESXi you normally have to download an ISO to your local machine, then upload it to the datastore — which doubles the transfer time and ties up your workstation. Using `wget` over SSH, you can download ISOs directly to the datastore in a single step.

## Prerequisites

- SSH enabled on your ESXi host (Host > Actions > Services > Enable Secure Shell)
- Network access from the ESXi host to the internet

## Step 1 — Connect via SSH

```bash
ssh root@your-esxi-host
```

## Step 2 — Navigate to your datastore

```bash
cd /vmfs/volumes/datastore1/
```

Replace `datastore1` with the name of your datastore. You can list available datastores with:

```bash
ls /vmfs/volumes/
```

## Step 3 — Allow outbound HTTP traffic

By default ESXi blocks outbound HTTP connections. Enable the `httpClient` firewall rule:

```bash
esxcli network firewall ruleset set -e true -r httpClient
```

## Step 4 — Download the ISO

```bash
wget --no-check-certificate --user-agent="Mozilla" "https://example.com/path/to/file.iso"
```

To save the file with a custom name, use the `-O` flag:

```bash
wget --no-check-certificate --user-agent="Mozilla" "https://example.com/path/to/file.iso" -O "Windows-11.iso"
```

The `--no-check-certificate` flag bypasses SSL certificate validation (some Microsoft download URLs require this). The `--user-agent="Mozilla"` flag is needed because some servers reject non-browser user agents.

## Step 5 — Disable the firewall rule

Once the download is complete, re-enable the default firewall stance:

```bash
esxcli network firewall ruleset set -e false -r httpClient
```

The ISO will now appear in your datastore and can be attached to any virtual machine on that host.
