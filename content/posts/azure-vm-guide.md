---
title: 'How to Launch Your First Azure Virtual Machine: A Simple Guide'
date: 2026-05-23
draft: false
tags: ['Cloud', 'Azure', 'Tutorial']
categories: ['Cloud Computing']
---

Running your own virtual server (a Virtual Machine, or VM) in the cloud is a great way to host personal projects, test code, or run private software. You don’t need to be a systems architect to do it; you just need to follow these steps.

### Important Requirements Before You Start
* **Azure Account:** You need an active subscription. If you are just starting, use the "Free Tier" options so you don't accidentally get charged for high-end hardware you don't need.
* **Region Selection:** Pick a region close to your physical location (e.g., "South Africa North" if you are in Nigeria) to keep your server fast.
* **Keep Your Keys Safe:** If you set up a Linux server, you will download a "Key" file. **Do not lose this.** If you lose it, you cannot log into your server, and you will have to delete and recreate the whole thing.

### Step 1: Create the Virtual Machine
1. Log into your <a href="https://portal.azure.com/" target="_blank" rel="noopener noreferrer">Azure Portal</a>.
2. In the top search bar, type "Virtual Machines" and select it.
3. Click **Create** > **Azure virtual machine**.
4. **Subscription & Resource Group:** A Resource Group is just a digital "folder." If you don’t have one, click **Create New** and give it a simple name (like "MyFirstProject").
5. **Name your VM:** Give your server a name you will recognize later.

### Step 2: Pick Your Hardware
* **Image:** Choose the operating system you want (e.g., Ubuntu Server for web projects, or Windows Server if you need a familiar desktop interface).
* **Size:** Look for the "B-series" (like B1s or B2s). These are "burstable" servers designed for personal projects. They are very inexpensive compared to the professional-grade options.

### Step 3: Storage and Disks
You don't need a massive hard drive for most basic projects. Under the **Disks** tab:
* **OS Disk Type:** "Standard HDD" is the cheapest and fine for basic tasks. "Premium SSD" is very fast but significantly more expensive. Pick "Standard SSD" if you want a good balance between speed and price.
* **Disk Encryption:** For most personal projects, leaving this as "Platform-managed key" is the easiest and most reliable setting.

### Step 4: Networking and Access
If you don't configure this, your server will be totally isolated from the internet. Under the **Networking** tab:
* **Inbound Ports:** You must allow specific traffic. 
    * Allow **SSH (Port 22)** if you are using Linux.
    * Allow **RDP (Port 3389)** if you are using Windows.
* **Public IP:** Ensure this is set to "Enabled" so your computer can reach the server over the internet.

### Step 5: Management and Auto-Shutdown
This is the most important tab for protecting your budget. Under the **Management** tab:
* **Auto-Shutdown:** **Turn this ON.** Pick a time (like 8:00 PM). This tells Azure to automatically turn off your server every night so you don't pay for it while you are sleeping or not using it.
* **Shutdown Notification:** Set this to "Yes" and enter your email address. Azure will send you a friendly heads-up before it turns the server off.
* **Backup:** For your first server, you can leave this "Off," but consider turning it on later if your project starts storing important data.

### Step 6: Final Launch
1. Click **Review + Create**.
2. Azure will run a quick check. If everything is green, click **Create**.
3. It takes a few minutes to "spin up." Once the screen says "Deployment Succeeded," click **Go to resource**. You will see your **Public IP Address**—that is the "phone number" of your new server!
---