---
title: 'How to Migrate GoDaddy Email to Microsoft 365: The Complete Step by Step Fix'
date: 2026-05-23
draft: false
tags: ['Microsoft 365', 'Cloud Migration', 'GoDaddy', 'Tutorial']
categories: ["Cloud Computing"]
---

It is incredibly common to get these terms mixed up, but confusing a basic domain pointer with an actual mailbox migration will cause a massive data loss. If you only move the email address by flipping your DNS settings, you are essentially just forwarding your mail to a brand new empty building. Your old folders, calendar invites, and historical contacts will be left behind in the old GoDaddy servers.

To make sure you do not lose a single file, let us break down exactly what a mailbox is and map out the bulletproof step by step fix to migrate your entire history based on the exact GoDaddy system you are using.

### Email Address vs. Mailbox: The Core Difference

Think of your email configuration like physical mail:
* Email Address (you@yourdomain.com): This is just the routing identity or the mailbox address painted on your curb. Moving this tells the world where to send new letters.
* Mailbox Container: This is the entire filing cabinet. It holds your full email history, custom folder structures, calendar appointments, contacts list, tasks, and notes.

### How to Migrate the Entire Mailbox Safely

GoDaddy has deployed two completely different email backends over the years. Look at where you log in right now to choose your exact path:

* Scenario A: You log in at Outlook.office.com. Your email is already powered by Microsoft 365, but GoDaddy owns the billing tenancy. For this, you do not migrate data files at all. You use the Defederation workflow to change the locks on the front door and hand the direct admin keys over to yourself. Everything stays completely untouched.
* Scenario B: You log in at Email.godaddy.com. This is the legacy GoDaddy Workspace system (POP/IMAP). Your data lives on old GoDaddy hardware. To move this to Microsoft 365 without errors, you must execute a clean IMAP data migration.

Here is the exact production roadmap to execute the Scenario B migration successfully.

### Critical Pre-Migration Technical Settings

Before running any migration tools, you must configure your environment to prevent a connection block or dropped emails.

1. Adjust DNS TTL: Log into your GoDaddy DNS dashboard 24 hours before starting. Lower the Time-To-Live (TTL) of your MX record down to 300 seconds (5 minutes). This ensures that when you flip the switch later, the change propagates across the internet instantly.
2. Bypass the Basic Auth Block: Microsoft has globally disabled Basic Authentication, and GoDaddy heavily enforces Multi-Factor Authentication (MFA). If you feed raw passwords into the migration engine, you will hit a quick ProvisioningFailedException error. You must log into each user security panel on GoDaddy and generate a unique App Password specifically for the migration tool.

### Step 1: Export Calendars and Contacts

The standard IMAP protocol only reads email messages and folder syncs. It cannot see calendar events or address books. You must pull these out manually.

Log into GoDaddy Workspace webmail, open your Contacts tab, click Export, and save the asset as a .CSV file. Next, open your Calendar tab, click Export, and save it as an .ICS file. Keep these safe on your local drive.

### Step 2: Verify the Custom Domain and Create Empty Users

Log into your new, direct Microsoft 365 Admin Center interface. You cannot create production mailboxes until Microsoft verifies your domain identity.

1. Navigate to Settings > Domains > Add Domain.
2. Type in your custom domain name.
3. Copy the generated TXT record value from Microsoft and paste it into your GoDaddy DNS zone manager. Click verify. Note: Do not change your MX records yet.
4. Once verified, go to Users > Active Users > Add a User. 
5. Create the exact matching usernames (e.g., sales@yourdomain.com) and assign a valid Microsoft 365 exchange license. This creates a fresh, empty mailbox container waiting for incoming data.

### Step 3: Configure the IMAP Migration Endpoint

Now we tell the Microsoft 365 backend to reach back into GoDaddy and mirror the historical data folders.

1. Inside the Microsoft 365 Admin Center, navigate to Setup > Migrations > Email.
2. Select Other email provider (IMAP).
3. Configure the migration endpoint configuration with these exact technical specs:
   IMAP Server: imap.secureserver.net
   Port: 993
   Authentication: Basic
   Encryption: SSL
4. Upload a migration CSV file listing your new destination email addresses, your old GoDaddy usernames, and the unique App Passwords you generated during the prep phase.
5. Start the synchronization batch. Microsoft will log into GoDaddy in the background and copy every single historical email and subfolder. Your users can keep working inside GoDaddy normally while this sync runs.

### Step 4: Cut Over the DNS MX Pointer

Once the migration panel status reads Synced, the copy job is complete. It is time to update the routing address on the curb.

Log back into your GoDaddy DNS management console. Delete the old GoDaddy MX records and replace them with the new destination MX pointer provided in your Microsoft 365 setup card (usually formatted as yourdomain-com.mail.protection.outlook.com). 

From this exact second, all brand new emails will bypass GoDaddy completely and land straight inside the new Microsoft 365 cloud environment.

### Step 5: Import Calendars and Contacts to Complete the Fix

Have your users launch their desktop Outlook profiles and connect to their brand new Microsoft 365 accounts. 

To restore their schedules and address books, navigate to File > Open & Export > Import/Export. Choose to import from another program or file, select your saved .CSV file for contacts, and repeat the loop for the .ICS calendar file.

The setup is fully optimized. Your users now have their exact same email identities, every single piece of historical data, and a fully functional infrastructure running directly on corporate cloud architecture without GoDaddy restrictions.
---