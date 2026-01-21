---
title: Silent Payments (BIP352)
date: 2026-01-20 10:06:51 -0400
categories: [Free Speech, Bitcoin]
tags: [financial privacy, Bitcoin, first amendment]
description: **Silent Payments (BIP352)**, the following explainer breaks down this innovative Bitcoin protocol.
---

### **What are Silent Payments?**

Silent Payments provide **privacy-preserving static addresses** for Bitcoin. Traditionally, if you post a single Bitcoin address (e.g., for donations), everyone can see every transaction sent to that address, compromising both your privacy and that of your donors.

Silent Payments solve this by allowing a receiver to share one **static address** while ensuring that every sender generates a **unique, one-time address** on the blockchain that only the receiver can identify and spend.

---

### **Key Technical Concepts**

1. **Static Address (The "Payment Code"):** Instead of the standard `bc1...` address, a Silent Payment address starts with `sp1...`. This address is longer because it encodes two public keys:
* **Scan Key:** Used by the receiver to "watch" the blockchain for incoming funds.
* **Spend Key:** Used to actually sign and move the funds.


2. **ECDH (Elliptic-Curve Diffie-Hellman):**
This is the "magic" math behind the protocol. It allows the sender and receiver to create a **shared secret** using only their public information.
* **The Sender** uses their own transaction inputs (UTXOs) and the receiver's Silent Payment address to calculate a "tweak."
* **The Receiver** uses their private scan key to find that same tweak on the blockchain.


3. **Indistinguishability:**
On-chain, a Silent Payment looks exactly like a standard **Taproot (P2TR)** transaction. An outside observer cannot tell if a transaction was a normal payment or a Silent Payment, nor can they link it back to the `sp1...` address.

---

### **How It Operates (The Process)**

#### **Step 1: The Setup (Receiver)**

The receiver generates a Silent Payment address (`sp1...`) in a compatible wallet and shares it (e.g., on a website or social media).

#### **Step 2: Sending (The Tweak)**

When Alice sends Bitcoin to Bob's `sp1...` address:

* Alice’s wallet selects the coins (UTXOs) she wants to spend.
* The wallet mathematically combines the **private keys** of Alice’s inputs with **Bob’s public scan key**.
* This creates a **unique one-time Taproot address**. Alice sends the funds to this new address.

#### **Step 3: Receiving (The Scan)**

Bob’s wallet is constantly "scanning" new blocks. For every transaction on the network, his wallet:

* Looks at the inputs used in that transaction.
* Performs a calculation using his **private scan key**.
* If the result matches one of the outputs in that transaction, the wallet "sees" the payment and adds it to Bob's balance.

---

### **Practical Step-by-Step Instructions**

#### **To Receive Funds:**

1. **Get a Compatible Wallet:** Use a wallet that supports BIP352 (e.g., **Cake Wallet**, **BitBox02**, or **Silentium**).
2. **Generate your `sp1` Address:** Locate the "Silent Payments" section in your wallet and copy your static address.
3. **Share the Address:** You can safely post this address anywhere. Unlike traditional addresses, reuse here is impossible—every donor will automatically generate a fresh address for you.
4. **Sync/Scan:** Because your wallet has to "calculate" your balance by looking at every transaction, you may need to let it scan for a few minutes to find new payments.

#### **To Send Funds:**

1. **Paste the `sp1` Address:** Enter the recipient's Silent Payment address in your wallet's "Send" field.
2. **Choose Inputs:** Your wallet will automatically select your Taproot or SegWit inputs to use for the math.
3. **Send:** Confirm the transaction. You don't need to ask the receiver for a "new" address; the protocol handles the privacy for you.

---

### **Real-World Use Cases**

* **Political Dissidents & Human Rights:** An activist can post a single donation address on a public website. Even if the government knows the static address, they cannot see how many people have donated or what the total balance is because every donation appears as a random, disconnected address on the blockchain.
* **Social Media Tips:** You can put your `sp1` address in your "X" (Twitter) or Nostr profile. Friends can send you tips repeatedly without you ever having to generate and send them a fresh address for every tip.
* **Business Invoicing:** A company can print one QR code on an invoice. Every customer who scans it will pay into a unique address, preventing competitors from analyzing the company's total revenue through a block explorer.

[Bitcoin Privacy Revolution](https://www.youtube.com/watch?v=KhahmfrkTeA)
{% include embed/youtube.html id="KhahmfrkTeA" %}
This video provides a practical demonstration of how to use Silent Payments in daily transactions to enhance your financial privacy.