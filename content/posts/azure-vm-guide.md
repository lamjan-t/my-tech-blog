---
title: 'The Pro Guide: How to Launch Your First Azure Virtual Machine'
date: 2026-05-23
draft: false
tags: ['Cloud', 'Azure', 'Tutorial']
categories: ['Cloud Computing']
---

Launching a virtual server in the cloud is a core skill, but it’s easy to get lost in the menu options. This guide breaks down every tab so you can launch a server that is secure, affordable, and easy to manage.

### 1. The Setup Checklist
* **Azure Subscription:** Ensure you are on a free tier or have a budget set.
* **Region:** Always pick a region closest to your users to keep latency low.
* **Key Pair:** If you choose Linux, you *must* download the SSH key file. If you lose it, you lose access to the server.

### 2. The Configuration Breakdown
As you go through the portal, here is what you need to know about the key tabs:

* **Basics:** Create a new **Resource Group**. Think of this as a digital container. When you want to delete the VM later, you can just delete the Resource Group to wipe everything at once.
* **Disks:** For most personal projects, **Standard SSD** is the perfect middle-ground. It’s faster than an HDD, but much cheaper than Premium SSD. 
* **Networking:** You are building a secure "door" to your server.
    * You **must** open **Port 22 (SSH)** for Linux or **Port 3389 (RDP)** for Windows.
    * If you skip this, the server will be online, but you will be locked out.
* **Management (The Most Important Tab):**
    * **Auto-Shutdown:** Turn this **ON**. Schedule it to shut down automatically every night to save money.
    * **Shutdown Notification:** Set this to "Yes" to get an email warning before the server turns off.
    * **Backup:** Turn this on if you are storing personal files or important configurations.
* **Advanced:** * **Tags:** Use these to label your VMs (e.g., `Owner: Me`, `Project: Testing`). It makes managing your account much easier as you grow.

### 3. Launching and Testing
Once you click **Create**, wait a few minutes for the "Deployment Succeeded" message. Click **Go to resource** to find your **Public IP Address**. 

* **To test:** Open your web browser and try to reach the IP. If you installed a web server, you should see a welcome page.
* **To cleanup:** If you are done testing, go to your **Resource Group** and click **Delete**. This ensures you don't get charged for a server you aren't using.
---