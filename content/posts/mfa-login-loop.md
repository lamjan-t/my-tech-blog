---
title: 'How I Fixed the Azure MFA Login Loop'
date: 2026-05-22
draft: false
tags: ['Azure', 'EntraID', 'Troubleshooting']
categories: ["Cloud Computing"]
---

### The Issue
Today a user got stuck in a continuous authentication loop when trying to access the Azure portal. They would input their password, approve the Microsoft Authenticator prompt, and then get kicked back to the login screen.

### How I Resolved It
1. Opened **Microsoft Entra ID** and checked the user's **Sign-in logs**.
2. Found a Conditional Access policy causing a conflict because it required a compliant device, but the user was on an unmanaged home laptop.
3. Created a temporary exclusion group for emergency remote access.