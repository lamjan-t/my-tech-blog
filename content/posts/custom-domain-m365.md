---
title: 'The Ultimate Guide to M365 Custom Domains: Automatic, Manual, and NS Paths'
date: 2026-05-22
draft: false
tags: ['Microsoft 365', 'DNS', 'Cloud-Administration', 'SysAdmin']
---

Nobody wants to use that long company.onmicrosoft.com address for official business emails. It looks temporary and unprofessional. Mapping your actual custom domain to Microsoft 365 is the very first thing you should do, but if your DNS is not correct, your emails will just be bouncing.

Depending on where your domain is hosted, Microsoft offers three different setup paths. Let us break them down directly so you can deploy cleanly without any issues.

### Path 1: The Automatic Path with Domain Connect

If you bought your domain from major providers like GoDaddy, Azure DNS, or Namecheap, you do not need to waste time manually typing out mail records and security hashes. Microsoft supports an industry standard called Domain Connect.

First, go to the M365 Admin Center, navigate to Settings, then Domains, and select Add Domain. Type in your domain name and click Use this domain. 

Microsoft will scan your domain, detect the registrar automatically, and show a button asking you to sign in to your registrar. Click it, log into your registrar account in the secure pop-up window, and click Authorize.

Microsoft will talk directly to your provider API, verify your ownership instantly, and add all the required mail and security records in the background. You do not need to copy or paste anything manually.

### Path 2: The Manual DNS Path

If your domain provider does not support Domain Connect, you have to configure the records manually. This path is also best if you want complete control over your DNS table.

First you have to prove ownership. Microsoft will give you a unique verification string. Log into your DNS host and add a new TXT record with these details:
Host name should be @ or left blank.
The value must be the exact MS=msXXXXXXXX token from the portal.
Set the TTL to 3600 or 1 hour.
Go back to the Microsoft portal and click Verify.

Once verification passes, you need to route your actual email traffic. You must add these three core records to your DNS host:

1. The MX Record for mail delivery:
Type is MX.
Host is @.
Points to: yourdomain-com.mail.protection.outlook.com
Priority is 0. This ensures Exchange Online handles all incoming mail.

2. The CNAME Record for autodiscover:
Type is CNAME.
Host is autodiscover.
Points to: autodiscover.outlook.com. This handles the configuration so users can easily set up their email profiles on Outlook apps.

3. The TXT Record for SPF security:
Type is TXT.
Host is @.
Value is v=spf1 include:spf.protection.outlook.com -all. Do not skip this, or your outbound emails will go straight to the spam folders of your users.

### Path 3: The Name Server Path

If you want Microsoft 365 to handle the entire DNS management for you so you do not have to keep logging into your registrar, you can delegate your Name Servers.

In the domain setup wizard, select the option that says Set up my online services for me. Microsoft will give you a list of 4 custom name servers. 

Log into your domain registrar, open the DNS management page, delete your current name servers, and paste the 4 name servers from Microsoft. Save your changes, return to the M365 portal, and click Verify.

Once this is done, your domain moves into Microsoft infrastructure. Any time you activate a new feature in your tenant, Microsoft will automatically handle the records for you.

### How to deal with DNS propagation traps

Even if your setup is correct, you might still hit a timeout or a record not found error when you click verify in the portal.

This usually happens because of a caching issue. If you click verify before the record has fully saved at your host, the portal will cache that old failure state.

Before you keep clicking the verify button over and over, open your terminal and run this quick query to see what is active on the public internet:

Resolve-DnsName -Name yourdomain.com -Type TXT

If your token string does not appear in the terminal output, the records are not live yet globally. Just give it 10 to 15 minutes for global nameservers to sync, then run the terminal command again. Once the terminal pulls the correct value, click verify in the portal and it will clear instantly.