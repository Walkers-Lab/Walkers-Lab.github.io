---
title: "Adding a Domain into Microsoft 365"
date: 2024-09-01 21:25:00 +0100
categories:
  - Microsoft 365
tags:
  - Microsoft 365
  - DNS
  - Cloudflare
  - Exchange Online
  - M365 Admin
  - Custom Domain
excerpt: "Step-by-step guide to adding a custom domain to Microsoft 365, covering domain verification and automatic DNS configuration via Cloudflare."
header:
  teaser: /assets/images/adding-a-domain-into-microsoft-365/teaser.png
---

Adding a custom domain to Microsoft 365 lets you use branded email addresses (e.g. `user@yourcompany.com` instead of `user@yourcompany.onmicrosoft.com`), and ties your organisation's identity into Teams, SharePoint, and other Microsoft services.

This guide walks through the process using Cloudflare as the domain registrar. Microsoft 365 can connect directly to Cloudflare to verify ownership and add DNS records automatically. If your domain is registered with a different provider, the verification steps will differ — you'll need to add a TXT record manually instead.

## Prerequisites

- A Microsoft 365 account with Global Administrator rights
- A domain registered with a DNS provider (this guide uses Cloudflare)
- Access to your Cloudflare account

## Step 1 — Open the Domains page

Sign in to the [Microsoft 365 Admin Centre](https://admin.microsoft.com/), expand **Settings** in the left-hand menu, and click **Domains**.

This page lists all domains currently associated with your tenant, including the default `.onmicrosoft.com` domain. Click **Add domain** to begin.

## Step 2 — Enter your domain name

Type the domain you want to add (e.g. `yourcompany.co.uk`) then click **Use this domain**.

## Step 3 — Verify domain ownership

Microsoft 365 will attempt to detect your domain registrar automatically.

<div class="notice--info" markdown="1">
**Not using Cloudflare?** Microsoft will provide a TXT record (e.g. `MS=ms12345678`) to add manually in your DNS provider's dashboard. Once added, return here and click **Verify**.
</div>

For Cloudflare users:

1. Click **Verify** when Microsoft detects Cloudflare
2. Sign in to your Cloudflare account in the popup window
3. Click **Authorise** — Cloudflare automatically adds the verification TXT record to your domain's DNS
4. The Cloudflare window closes and you are returned to the Admin Centre
5. Click **Continue**

## Step 4 — Add DNS records

Microsoft 365 will now offer to add the DNS records required for Exchange Online and Exchange Online Protection — the MX record, an Autodiscover CNAME, and an SPF TXT record needed for email to flow correctly.

Leave everything as default and click **Add DNS records**.

For Cloudflare users, another authorisation popup will appear. Click **Authorise** and Cloudflare will add all the required records automatically.

## Step 5 — Finish

Click **Done**. Your domain is now verified and configured in Microsoft 365.

You can now assign the custom domain to user accounts and mailboxes. Navigate to **Users > Active users**, open a user, and edit their email address to use the new domain.

<div class="notice--warning" markdown="1">
**DNS propagation:** DNS changes can take up to 72 hours to propagate globally, though Cloudflare changes typically take effect within a few minutes.
</div>
