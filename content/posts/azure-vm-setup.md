---
title: 'How to Launch Your First Azure Virtual Machine: A Simple Guide'
date: 2026-05-23
draft: false
tags: ['Cloud', 'Azure', 'Tutorial']
categories: ['Cloud Computing']
---

Running your own virtual server (a Virtual Machine, or VM) in the cloud is a great way to host personal projects or test software. You don’t need to be a systems architect to do it; you just need to follow the setup steps in order.

### Before You Start

* **Azure Account:** You will need an active subscription. If you are just testing things out, look for the "Free Tier" options so you don't get charged by accident.
* **Region Selection:** Pick a region close to where you live to keep things fast (e.g., if you are in Nigeria, "South Africa North" is usually your best bet for speed).
* **Save Your SSH Key:** If you are setting up a Linux server, **do not lose the key file** you download at the end of the setup. If you lose it, you lose access to your server.

### Step 1: Create the Virtual Machine

1. Log into your <a href="https://portal.azure.com/" target="_blank" rel="noopener noreferrer">Azure Portal</a>.
2. In the top search bar, type "Virtual Machines" and select it.
3. Click **Create** > **Azure virtual machine**.
4. **Subscription & Resource Group:** If you don’t have a Resource Group, click **Create New** and give it a simple name. This is just a folder to keep your server files together.
5. **Name your VM:** Give your server a name you can recognize.

### Step 2: Pick Your Hardware

This is where you decide how powerful your server should be.

* **Image:** Choose the OS you want (e.g., Ubuntu Server or Windows Server).
* **Size:** Don't pick the most expensive one! Look for the "B-series" sizes (like B1s or B2s). These are meant for personal use and are much cheaper.



### Step 3: Networking and Access

This is the most important part to avoid "Access Denied" errors later.

1. **Inbound Ports:** Under the "Networking" tab, make sure you allow **SSH (Port 22)** if you are using Linux, or **RDP (Port 3389)** if you are using Windows.
2. If you don't open these ports during setup, your computer won't be able to "talk" to your new cloud server.

### Step 4: Final Launch

1. Click **Review + Create**.
2. Azure will run a quick check to make sure your settings are valid.
3. Once the validation passes, click **Create**. It usually takes 2 to 5 minutes to finish spinning up.

### How to know it's working

Once the screen says "Deployment Succeeded," click **Go to resource**. You will see your VM's "Public IP Address." This is the address you will use to log into your new server from your laptop.

---