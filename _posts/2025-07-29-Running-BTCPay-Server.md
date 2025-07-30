---
title: Running BTCPay Server
date: 2025-07-29 11:00:21 -0400
categories: [Bitcoin Payments, Lunanode Hosting]
tags: [BTCPayserver Setup]
description: BTCPayg Guide By BTC Sessions.
---

{% include embed/youtube.html id='v=-GJr4XjRCPo' %}


- The tutorial details setting up a self-hosted, open-source Bitcoin payment processor (BTCPay Server) using Luna Node, a cloud hosting service. This involves creating a Luna Node account (payable in Bitcoin or credit card), generating API credentials, and launching the BTCPay Server instance.
- Prior experience with Bitcoin wallets is recommended. The tutorial uses Sparrow Wallet as an example, but others can be used. Understanding basic networking is helpful but not strictly required for the Luna Node method.
- The tutorial shows how to connect an external Bitcoin wallet (like Sparrow) to BTCPay Server using its extended public key. This allows BTCPay Server to receive payments without compromising the user's private keys.
- The tutorial explains setting up a Lightning node using BTCPay Server's internal node or a custom node. It demonstrates purchasing a Lightning channel from a service provider (like LnBig or Olympus) to receive Lightning payments. Alternatively, plugins for services like Strike or Blink offer simpler Lightning integration without managing a node directly.
- BTCPay Server offers customizable POS options, including product list-based systems with shopping carts and simple keypad-only terminals for in-person transactions. These can be configured to request customer data (email, shipping address) as needed.
Crowdfunding/Donations: The tutorial demonstrates setting up crowdfunding campaigns with BTCPay Server, allowing users to specify goals, deadlines, and reward tiers for contributors.
- The tutorial highlights the use of plugins (Strike and Blink) as alternatives to managing a self-hosted Lightning node. These plugins integrate directly with the user's existing Lightning wallets, simplifying payment processing. The tutorial uses Strike as a primary example, given its availability in many countries.
Managing Funds: The tutorial shows how to access and manage both on-chain and Lightning balances through the BTCPay Server interface and integrated wallets (Sparrow, Strike, Blink). It explains closing Lightning channels using Ride the Lightning.
- The tutorial emphasizes the importance of using hardware wallets (like Coldcard) for secure storage of significant Bitcoin holdings, particularly when receiving payments through BTCPay Server.
- The tutorial covers updating BTCPay Server to the latest version (2.0 and beyond), including using SSH to access the server and execute update commands. This step is optional if only using basic features without plugins.

## **Running BTCPay Server: A Complete Deployment Guide (From Scratch)**

BTCPay Server is one of the most powerful open-source Bitcoin payment processors available today. It lets you become your own payment gateway with full self-custody—no middlemen, no compromises. And the best part? The setup process is now easier than ever.

If you’re ready to launch your own BTCPay instance, here’s a **clean step-by-step guide** to get you running smoothly.

---

### **1. Launch the BTCPay Deployment Tool**

Go to the official LunaNode BTCPay Server launcher:
➡️ [https://launchbtcpay.lunanode.com](https://launchbtcpay.lunanode.com)

This web-based deployment wizard will handle most of the heavy lifting for you.

---

### **2. Connect Your LunaNode Account**

* Log in to your LunaNode account and create an API key + API ID (found under your LunaNode account settings).
* Paste both the **API ID** and **API key** into the BTCPay launcher.
* Click **Continue**.

---

### **3. Choose Your Domain**

At this step, you have two options:

* **Use a LunaNode-generated domain** (fastest way to get online).
* **Use your own custom domain** if you want a professional look. *(Tip: If using your own domain, set up DNS records first—see BTCPay’s [domain configuration guide](https://docs.btcpayserver.org/Domain/))*.

Click **Continue** once you’re ready.

---

### **4. Customize Your BTCPay Setup**

Here you can fine-tune your deployment:

* **SSH key:** Add it if you want secure terminal access.
* **SSL e-mail:** Used for automatic HTTPS certificates.
* **Altcoins:** (Optional) Enable support for additional cryptocurrencies.
* **Lightning Network:** Choose your implementation (e.g., LND, Core Lightning).

💡 **Pro tip:** If you plan on enabling more than two altcoins or expect higher transaction volume, upgrade to a stronger hosting plan.

---

### **5. Launch Your Server**

Click **Launch BTCPay** and wait. Deployment typically takes **about 5 minutes**. Be patient—the server is provisioning and setting up your environment behind the scenes.

---

### **6. First Login & Blockchain Sync**

Once the setup is done:

* Navigate to your chosen domain.
* Log in with the credentials you set during deployment.

**Syncing:**

* If you selected Bitcoin Core + Lightning (on the \$8.80/month *M2* plan), expect a **2–4 day sync time**.
* Want faster synchronization? Choose a higher-tier hosting plan with more CPU and storage.

---

### **7. That’s It—You’re Live!**

You now have a fully self-hosted BTCPay Server up and running. From here, you can:

* Create stores and payment buttons.
* Integrate BTCPay with your website or POS.
* Manage invoices, payouts, and Lightning channels—all from your dashboard.

---

Making BTCPay easy to install is the key to mainstream adoption. The simpler the process, the more merchants and users we’ll see embracing Bitcoin payments. But it doesn’t stop here:

* We need more **tutorials** like this one.
* We need more **translations** for global reach.
* We need more **UX/UI improvements**.

The BTCPay roadmap is packed with features—stay tuned for upcoming articles where we’ll dive into the newest tools and integrations.


---

⚡ **Your node. Your keys. Your payments.**


