---
title: 'The Full Guide to Launching Your Azure Virtual Machine'
date: 2026-05-23
draft: false
tags: ['Cloud', 'Azure', 'Tutorial']
categories: ['Cloud Computing']
---

Launching a server in the cloud is more than just clicking "Create." To avoid security holes and hidden costs, you need to configure the full stack correctly. Here is the full breakdown of every tab you will encounter.

### Step 1: Basics & Hardware
* **Resource Group:** Think of this as your project folder. Everything you create here (Disk, Network, VM) stays in this group.
* **Size:** Don't just click "Next." Look for **B-Series** (burstable) machines. They are perfect for testing and personal web hosting because they save you money when the server is idle.

### Step 2: Disks (The Hard Drive)
Don't waste money on the fastest drive if you don't need it. 
* **Standard HDD:** Best for backups or files you rarely open.
* **Standard SSD:** Perfect for most web servers and personal software.
* **Premium SSD:** Only choose this if you are running a heavy database that needs lightning-fast read/write speeds.
* **Encryption:** Always leave this as "Platform-managed key." It keeps your data secure without you having to manage complex encryption keys yourself.

### Step 3: Networking
If you don't configure this, the server is "dark" to the internet.
* **Public IP:** Ensure this is enabled. 
* **Inbound Ports:** You must pick these now or you won't be able to log in. 
    * **SSH (22):** For Linux servers.
    * **RDP (3389):** For Windows servers.

### Step 4: Management (The Budget Saver)
This is the most critical tab in the entire portal. 
* **Auto-Shutdown:** **Always turn this ON.** Set it to shut down at a specific time (like 8:00 PM) every single day. This prevents your server from running all night while you aren't using it.
* **Shutdown Notification:** Set this to "Yes" and add your email. You will get a warning 30 minutes before it turns off, allowing you to hit "Delay" if you are still working.
* **Backup:** For your first server, you can leave this "Off," but consider turning it on later if your project starts storing important data.

### Step 5: Advanced (The "Under the Hood" Stuff)
Most beginners skip this, but you shouldn't:
* **Custom Data:** If you have a script you want to run the very first time the server starts (like installing Docker or Nginx automatically), paste that script here. It saves you 20 minutes of manual setup every time you launch a new machine.
* **Tags:** Add tags like `Environment: Testing` or `Project: MyWebSite`. When you have 10+ servers later, tags are the only way to quickly search and manage your assets.

### Step 6: Review & Launch
Before you hit Create, look at the **"Price per hour"** displayed on the review page. If that number looks too high, go back to the **Size** tab and choose a smaller B-Series machine. Once it looks good, click **Create** and wait for the "Deployment Succeeded" message.
---