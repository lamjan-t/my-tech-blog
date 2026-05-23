---
title: 'How to Migrate GoDaddy Email to Microsoft 365 Step by Step'
date: 2026-05-23
draft: false
tags: ['Microsoft 365', 'GoDaddy', 'Cloud Migration', 'SysAdmin']
---

If you are currently stuck dealing with a restricted GoDaddy-managed email setup and want to break free, you need a clean path to move your data. This guide provides a how to migrate GoDaddy email to Microsoft 365 step by step fix that lets you gain full control over your tenant environment. Instead of paying extra for GoDaddy's marked-up plans, you can defederate GoDaddy Microsoft 365 account setups to unlock enterprise-grade security features like conditional access and direct billing. Let's look at exactly how to handle this transition cleanly without losing data or running into a major GoDaddy to Microsoft 365 mailbox migration error along the way.

The Reality of GoDaddy Federation

When you purchase Microsoft 365 through GoDaddy, they don't give you a normal tenant. They federate your domain, meaning GoDaddy controls the identity management and authentication layers. You cannot access half of the security configurations in the Entra ID portal, and you are forced to use their simplified dashboard. Defederating means we are cutting that umbilical cord. We are changing the domain from federated to managed so that Microsoft becomes your direct provider while keeping all your existing mailboxes, emails, and SharePoint files completely intact.

Prerequisites Before You Begin

Do not rush into this process without checking your access levels. You need full control of your domain's DNS panel because we will need to verify records if things slip up. You also need an administrative account that uses the default onmicrosoft domain. GoDaddy always creates a hidden admin account when they set up the tenant, usually ending in netorg or a similar string. You must locate this account before running any commands.

Locating the Real Global Admin Account

Open a private browsing window and navigate to the Azure portal. Log in using your current GoDaddy admin credentials. Once inside, go to Microsoft Entra ID and click on Users. Look through the list for an account that looks like admin@netorg12345.onmicrosoft.com or something similar. This is your target. Select this account and reset its password. This gives you a pure cloud administrator account that does not rely on GoDaddy's single sign-on page for authentication.

### Use PowerShell to Convert Domain from Federated to Managed

Now we need to drop into the command line to break the lock. Open your PowerShell terminal as an administrator on your computer. You will need the Microsoft Graph modules installed to talk directly to the identity infrastructure. Run these commands line by line to connect and flip the switch.

Install-Module Microsoft.Graph -Scope CurrentUser
Import-Module Microsoft.Graph.Identity.DirectoryManagement
Connect-MgGraph -Scopes "Domain.ReadWrite.All","Directory.AccessAsUser.All"

The connection prompt will pop up. Sign in using that netorg cloud admin account whose password you just reset. Once you are authenticated, check the status of your domain by running the next command line.

Get-MgDomain | Select Id,AuthenticationType

If the status says Federated, GoDaddy is still in control. To break the link and move the domain to native Microsoft management, execute the update command.

Update-MgDomain -DomainId yourdomain.com -Authentication Managed

Replace yourdomain.com with your actual custom domain name. Run the verification command again to confirm the authentication type has changed to Managed.

Buying Your New Licenses

The moment you flip the domain to managed, GoDaddy's billing systems lose their hooks into your users, but the mailboxes are still there. However, your users will show up as unlicensed or their existing licenses will stop working soon. Go straight to the Microsoft 365 Admin Center using your cloud admin account. Navigate to Billing and then Purchase Services. Buy the exact number of Business Basic, Standard, or Premium licenses you need. Go to Active Users, select your people, and assign the new direct licenses immediately so email flow doesn't drop.

Resetting User Passwords

Because GoDaddy was handling the passwords through single sign-on, your users do not have native Microsoft passwords yet. You must reset the passwords for all active users inside the Microsoft 365 Admin Center. You can do this one by one or do a bulk reset. Give them temporary passwords and inform them that they will need to log back into Outlook and Teams using these new credentials.

### Fix Common GoDaddy to Microsoft 365 Mailbox Migration Error

A common headache during this shift is when users try to log in and get stuck in a continuous loop redirecting them back to the GoDaddy sign-in page. This happens because the browser cache or the local office credentials still think the account is federated. Tell your users to completely clear their browser data or use an Incognito window for the first sign-in. For desktop Outlook apps, you might need to go to the Windows Credential Manager and clear all stored identities related to Microsoft Office before re-authenticating.

Removing the Remaining GoDaddy Access Keys

Even after changing the domain type, GoDaddy still has delegated administrator access and enterprise applications running inside your tenant. You need to clear them out to secure your environment completely. Go to the Microsoft 365 Admin Center, click on Settings, and open Partner Relationships. Find GoDaddy in the list and remove their roles. Next, open the Entra ID portal, go to Enterprise Applications, search for the Partner Center Web App, and delete it. Now the tenant is fully yours.
