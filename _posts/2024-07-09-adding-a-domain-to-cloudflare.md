---
title: "Adding a Domain to Cloudflare"
date: 2024-07-09 20:49:00 +0100
categories:
  - Cloudflare
tags:
  - Cloudflare
  - DNS
  - Nameservers
  - CDN
  - Domain Setup
excerpt: "Step-by-step guide to adding a domain to Cloudflare by updating your registrar's nameservers, covering the full process from registrar to Cloudflare activation."
header:
  teaser: /assets/images/adding-a-domain-to-cloudflare/teaser.png
---

Adding your domain to Cloudflare puts your DNS under Cloudflare's control, unlocking their CDN, DDoS protection, WAF, and free SSL. The process takes about five minutes — most of the wait is DNS propagation.

This guide uses Fasthosts as the domain registrar. The steps at your registrar will look slightly different, but the Cloudflare side is identical regardless of where your domain is registered.

## Prerequisites

- A domain registered with any registrar
- A Cloudflare account (free tier is sufficient)

## Step 1 — Add the site in Cloudflare

Sign in to [Cloudflare](https://dash.cloudflare.com/) and click **Add a site**. Enter your domain name and click **Continue**.

Cloudflare will scan your existing DNS records and import them automatically. Review the imported records before proceeding to make sure nothing is missing.

## Step 2 — Note the Cloudflare nameservers

On the nameservers page, Cloudflare will give you two nameservers — something like:

```
aria.ns.cloudflare.com
ben.ns.cloudflare.com
```

Copy both of these. You will need them in the next step.

## Step 3 — Update nameservers at your registrar

Log in to your domain registrar and find the nameserver settings for your domain. The exact location varies by registrar:

| Registrar | Where to find it |
|---|---|
| Fasthosts | Domain Names → select domain → Manage nameservers → Specify name servers |
| GoDaddy | My Products → DNS → Nameservers |
| Namecheap | Domain List → Manage → Nameservers |

Replace the existing nameservers with the two Cloudflare nameservers you copied, then save.

## Step 4 — Verify in Cloudflare

Return to Cloudflare and click **Check nameservers now**.

<div class="notice--info" markdown="1">
**Propagation time:** Nameserver changes typically take 5–30 minutes with most registrars, but can take up to 24 hours. Cloudflare will email you once the domain is active.
</div>

Click **Continue**, then **Finish later** on the Quick Start Guide — you can configure those settings at any time.

## What you get

Once Cloudflare is active, your domain benefits from:

- **CDN** — static assets served from Cloudflare's global edge network
- **DDoS protection** — volumetric attack mitigation at the network layer
- **Free SSL/TLS** — automatic HTTPS with a Cloudflare-issued certificate
- **DNS management** — fast, reliable DNS with an easy dashboard
- **Analytics** — traffic insights without cookies or tracking scripts
