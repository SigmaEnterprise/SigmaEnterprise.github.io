Explore the Mostro Messaging Protocol: Unveiling a Seamless Trading Experience! 🌐

Discover the intricacies of the Mostro messaging protocol through a series of simple yet powerful steps! From creating new orders to facilitating lightning-fast transactions with lightning addresses, Mostro ensures a streamlined and secure trading environment. Learn how to initiate and navigate disputes, empowering users to address issues effectively.

📜 Overview of Mostro Specifications:
Unveil the secrets of Mostro daemon messages, all crafted as Parameterized Replaceable Events. Dive into the communication channels between users and Mostro, where Nostr event kind 4 takes the spotlight. Explore the art of encryption and serialization in the world of Mostro messaging.

🔑 Keys and Ephemeral Keys:
Master the art of secure communication with Mostro by understanding the significance of pubkeys and ephemeral keys. Witness how fresh keys play a crucial role in safeguarding user privacy during interactions.

💼 Creating and Taking Orders:
Embark on a journey of creating buy orders with lightning addresses, speeding up the trading process. Delve into the intricacies of the Nostr event kind 4, unveiling the magic behind base64-encoded, aes-256-cbc encrypted JSON-serialized strings. Follow the confirmation messages and order publication steps, ensuring a smooth trading experience.

💰 Payment Requests and Responses:
Witness the efficiency of using lightning addresses for receiving funds, minimizing the need for constant invoice creation. Explore the exchange of Nostr event kind 4 messages, facilitating secure and rapid transactions. Keep an eye on Mostro responses, providing essential updates on order statuses.

⚖️ Handling Disputes:
Navigate the delicate process of initiating and responding to disputes within orders. Understand the nuances of dispute-related messages, both initiated by users and Mostro. Explore the role of Mostro admin in resolving disputes and the subsequent updates in the event timeline.

📚 For a Comprehensive Understanding:
While this guide provides a glimpse into the Mostro messaging protocol, the full spectrum of details awaits you in the official documentation. 📖 Visit Mostro Messages Overview for an in-depth exploration, ensuring you are well-equipped for a seamless and secure trading journey on Mostro. Happy trading! 🌟

# Mostro Network: Pioneering Censorship-Resistant Bitcoin Exchange


Mostro Network, an avant-garde project initiated on November 6, 2023, unfolds a revolutionary approach to facilitate Bitcoin transactions through the Lightning Network. The project addresses the growing demand for conducting Bitcoin transactions without compromising personal data, introducing a groundbreaking solution for peer-to-peer exchanges.

## Project Genesis: @lnp2pBot on Telegram

The inception of Mostro Network traces back to the initiation of @lnp2pBot on Telegram, a testament to enabling users worldwide to buy and sell Bitcoin via the Lightning Network. The bot operates organically, gaining traction globally, with a significant impact observed in Latin America, where the adoption of Bitcoin transcends the limitations of local currencies, especially in regions facing dictatorial regimes such as Cuba and Venezuela.

While @lnp2pBot thrived on Telegram, concerns arose about potential censorship by powerful entities. To mitigate this risk, the quest for a platform impervious to censorship led to the discovery of Nostr.

## Enter Nostr: A Sanctuary for Decentralized Communication

Nostr emerges as the ideal platform for hosting the Mostro Network, providing a haven where the bot can thrive without the looming threat of censorship. The exploration of Nostr began a month ago, with a focus on creating a new bot version—a censorship-resistant iteration, aptly named the "Monster" version.

The initial steps involve crafting a Nostr bot in Rust, a language known for its reliability and performance. This nascent implementation marks the beginning of a journey toward creating an unstoppable and censorship-resistant peer-to-peer exchange on the Lightning Network.

## Mostro Architecture and Operation

### Escrow Mechanism for Enhanced Security

Mostro acts as an escrow service, mitigating risks for both buyers and sellers in Bitcoin transactions. Leveraging a Lightning Network node, Mostro generates hold invoices for sellers and pays buyers using regular Lightning invoices, ensuring a secure and efficient exchange.

### Establishing a Decentralized Network of Mostros

To avoid a single point of failure, the Mostro Network encourages the creation of multiple Mostros, each contributing to the reliability of the network. Operating a Mostro requires a lightning node with substantial liquidity, ensuring rapid and secure transactions. Mostros sustain themselves through fees charged on successful orders.

### Reputation System for Quality Assurance

Users have the power to rate Mostros, fostering competition among Mostros to attract more users. A robust reputation system ensures that subpar Mostros are rejected by users, losing incentives to persist.

## Order Flow: A Seamless Process

The order flow on Mostro Network follows a well-defined and secure process:

1. **Order Publication:**
   
   - Buyers and sellers communicate their intent by sending encrypted messages to Mostro.
   - Mostro creates Parameterized Replaceable Events for potential trades.

2. **Buyer Takes an Order:**
   
   - Buyers send regular invoices and encrypted messages to Mostro.
   - Mostro connects buyers with sellers by creating hold invoices.

3. **Mostro Puts Parties in Touch:**
   
   - After the seller pays the invoice, Mostro updates the order status to "Active."
   - Mostro facilitates communication between buyer and seller.

4. **Fiat Transaction Confirmation:**
   
   - The buyer sends fiat money to the seller and notifies Mostro through encrypted messages.

5. **Release of Funds:**
   
   - Mostro requests the release of funds from the seller.

6. **Invoice Settlement:**
   
   - Mostro settles the seller's invoice and pays the buyer's invoice, updating the order status accordingly.

The detailed specifications and communication protocols can be found in the Mostro documentation, providing a comprehensive guide for users and developers alike.

## Call to Rust Developers: Join the Mostro Revolution!

Mostro Network is in its early stages, and Rust developers are invited to contribute to this groundbreaking project. The journey has just begun, and early participants have the opportunity to shape the future of decentralized, censorship-resistant Bitcoin exchanges. Happy hacking!

## A New Frontier in Bitcoin Exchange

Mostro Network, hosted on the resilient platform of Nostr, emerges as a beacon of innovation in the realm of decentralized Bitcoin exchanges. With a focus on security, reliability, and censorship resistance, Mostro sets the stage for a new era in peer-to-peer transactions, empowering users globally to engage in Bitcoin transactions without compromising on privacy or succumbing to external pressures. As the project evolves, the Mostro Network promises to be a transformative force in the world of cryptocurrency.


## Communication with Mostro

All messages exchanged with Mostro adhere to Nostr event kind 4. The content field of the event is a crucial element, employing base64 encoding and AES-256-CBC encryption for security. The content field contains a JSON-serialized string with specific parameters:

- **version:** Indicates the protocol version (currently 1).
- **pubkey (optional):** The real pubkey of the user, used for message signing when sent from ephemeral keys.
- **action:** Specifies the action to be performed by the Mostro daemon.
- **content (optional):** Provides additional content based on the action performed.

Here's an example of a FiatSent Order message:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": "0001be6bd50247846a28cce439a10470a39b1b6c81d5c3be2475156a413e1e3a",
    "action": "FiatSent",
    "content": null
  }
}
```

## Key Management

Key management is crucial for secure communication. In the examples provided, the following keys are used:

- **Mostro's pubkey:** dbe0b1be7aafd3cfba92d7463edbd4e33b2969f61bd554d37ac56f032e13355a
- **Seller's real pubkey:** 00000ba40c5795451705bb9c165b3af93c846894d3062a9cd7fcba090eb3bf78
- **Seller's ephemeral pubkey:** 1f5bb148a25bca31506594722e746b10acf2641a12725b12072dcbc46ade544d
- **Buyer's real pubkey:** 0000147e939bef2b81c27af4c1b702c90c3843f7212a34934bff1e049b7f1427
- **Buyer's ephemeral pubkey:** 9a42ac72d6466a6dbe5b4b07a8717ee13e55abb6bdd810ea9c321c9a32ee837b

## Ephemeral Keys

Mostro clients are encouraged to use freshly generated keys for communication. The pubkey field indicates where the counterpart wants to be contacted. This practice ensures enhanced privacy, as orders and users cannot be easily linked. The buyer_pubkey and seller_pubkey fields represent the real pubkeys of each party.

By adhering to these specifications, users can engage with Mostro confidently, knowing that their communication is secure and their privacy is prioritized.

> "Secure communication is the cornerstone of Mostro's commitment to user privacy and a seamless peer-to-peer exchange experience."

# Creating a New Order on Mostro: A Step-by-Step Guide

## Introduction

Creating a buy order on Mostro becomes faster and more convenient when utilizing a Lightning address. This guide outlines the process, starting with the buyer sending a Nostr event kind 4 to Mostro. Follow the steps below to initiate and confirm a new order seamlessly.

### Step 1: Initiating a New Order

The buyer initiates the order by sending a Nostr event kind 4 with the following content:

```json
{
  "Order": {
    "version": 1,
    "pubkey": "0000147e939bef2b81c27af4c1b702c90c3843f7212a34934bff1e049b7f1427", // Buyer's real pubkey
    "action": "NewOrder",
    "content": {
      "Order": {
        "kind": "Buy",
        "status": "Pending",
        "amount": 0,
        "fiat_code": "VES",
        "fiat_amount": 100,
        "payment_method": "face to face",
        "premium": 1,
        "buyer_invoice": "mostro_p2p@ln.tips",
        "created_at": 0
      }
    }
  }
}
```

### Step 2: Nostr Event

Upon receiving the buyer's request, Mostro generates a Nostr event with the following structure:

```json
{
  "id": "cade205b849a872d74ba4d2a978135dbc05b4e5f483bb4403c42627dfd24f67d",
  "kind": 4,
  "pubkey": "9a42ac72d6466a6dbe5b4b07a8717ee13e55abb6bdd810ea9c321c9a32ee837b", // Buyer's ephemeral pubkey
  "content": "base64-encoded-aes-256-cbc-encrypted-JSON-serialized-string",
  "tags": [
    ["p", "dbe0b1be7aafd3cfba92d7463edbd4e33b2969f61bd554d37ac56f032e13355a"] // Mostro's pubkey
  ],
  "created_at": 1234567890,
  "sig": "a21eb195fe418613aa9a3a8a78039b090e50dc3f9fb06b0f3fe41c63221adc073a9317a1f28d9db843a43c28d860ba173b70132ca85b0e706f6487d43a57ee82"
}
```

### Step 3: Confirmation Message

Mostro acknowledges the order by sending a confirmation message (nip04 event) to the buyer:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": "0000147e939bef2b81c27af4c1b702c90c3843f7212a34934bff1e049b7f1427",
    "content": {
      "Order": {
        "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
        "kind": "Sell",
        "status": "Pending",
        "amount": 0,
        "fiat_code": "VES",
        "fiat_amount": 100,
        "payment_method": "face to face",
        "premium": 1,
        "master_buyer_pubkey": null,
        "master_seller_pubkey": null,
        "buyer_invoice": "mostro_p2p@ln.tips",
        "created_at": 1698870173
      }
    }
  }
}
```

### Step 4: Order Publication

Mostro publishes the order as an event kind 38383 with status "Pending." Sellers can view and take this order. After a seller accepts the order, Mostro handles the invoice payment when the seller releases the funds.

By following these steps, buyers and sellers can engage in efficient and secure transactions on Mostro.

> "Experience the convenience of Lightning-fast orders on Mostro – where speed meets security in peer-to-peer exchanges."

# Taking a Sell Order with a Lightning Address on Mostro: A Comprehensive Guide

## Introduction

To streamline the process of receiving funds and eliminate the need to create and send Lightning invoices for each trade, buyers on Mostro can utilize a Lightning address. This guide outlines the steps involved in taking a sell order with a Lightning address, from initiating the request to Mostro's response.

### Step 1: Initiating the Sell Order

The buyer sends a message to Mostro in a Nostr event kind 4 with the following content:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": "0000147e939bef2b81c27af4c1b702c90c3843f7212a34934bff1e049b7f1427",
    "action": "TakeSell",
    "content": {
      "PaymentRequest": [null, "mostro_p2p@ln.tips"]
    }
  }
}
```

### Step 2: Nostr Event

The buyer's message to Mostro generates a Nostr event with the following structure:

```json
{
  "id": "cade205b849a872d74ba4d2a978135dbc05b4e5f483bb4403c42627dfd24f67d",
  "kind": 4,
  "pubkey": "9a42ac72d6466a6dbe5b4b07a8717ee13e55abb6bdd810ea9c321c9a32ee837b",
  "content": "base64-encoded-aes-256-cbc-encrypted-JSON-serialized-string",
  "tags": [
    ["p", "dbe0b1be7aafd3cfba92d7463edbd4e33b2969f61bd554d37ac56f032e13355a"]
  ],
  "created_at": 1234567890,
  "sig": "a21eb195fe418613aa9a3a8a78039b090e50dc3f9fb06b0f3fe41c63221adc073a9317a1f28d9db843a43c28d860ba173b70132ca85b0e706f6487d43a57ee82"
}
```

### Step 3: Mostro's Response

Mostro responds to the buyer with a nip04 event containing a wrapped Order in the content:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": null,
    "action": "WaitingSellerToPay",
    "content": null
  }
}
```

### Step 4: Update on Order Status

Mostro updates the nip33 event with the "d" tag "ede61c96-4c13-4519-bf3a-dcf7f1e9d842" to change the status to "WaitingPayment." The updated event looks like this:

```json
[
  "EVENT",
  "RAND",
  {
    "id": "eb0582360ebd3836c90711f774fbecb27e600f4a5fedf4fc2d16fc852f8380b1",
    "pubkey": "dbe0b1be7aafd3cfba92d7463edbd4e33b2969f61bd554d37ac56f032e13355a",
    "created_at": 1702549437,
    "kind": 38383,
    "tags": [
      ["d", "ede61c96-4c13-4519-bf3a-dcf7f1e9d842"],
      ["k", "Sell"],
      ["f", "VES"],
      ["s", "WaitingPayment"],
      ["amt", "7851"],
      ["fa", "100"],
      ["pm", "face to face"],
      ["premium", "1"],
      ["y", "mostrop2p"],
      ["z", "order"]
    ],
    "content": "",
    "sig": "a835f8620db3ebdd9fa142ae99c599a61da86321c60f7c9fed0cc57169950f4121757ff64a5e998baccf6b68272aa51819c3e688d8ad586c0177b3cd1ab09c0f"
  }
]
```

By following these steps, buyers can efficiently take sell orders using Lightning addresses on Mostro, enhancing the trading experience with speed and convenience.

> "Experience hassle-free transactions with Lightning addresses on Mostro – where simplicity meets security in peer-to-peer exchanges."

# Initiating a Dispute on Mostro: A Step-by-Step Guide

## Introduction

Users on Mostro have the option to initiate a dispute in an order with the status "Pending" or "FiatSent." This guide outlines the process of starting a dispute, the responses from Mostro to the seller and buyer, and the subsequent actions taken by Mostro and administrators.

### Step 1: Initiating a Dispute

A user can start a dispute by sending the following action in a Nostr event:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": "00000ba40c5795451705bb9c165b3af93c846894d3062a9cd7fcba090eb3bf78",
    "action": "Dispute",
    "content": null
  }
}
```

### Step 2: Mostro's Response to the Seller

Mostro responds to the seller with the following message:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": null,
    "action": "DisputeInitiatedByYou",
    "content": null
  }
}
```

### Step 3: Mostro's Response to the Buyer

Mostro sends a message to the buyer:

```json
{
  "Order": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": null,
    "action": "DisputeInitiatedByPeer",
    "content": null
  }
}
```

### Step 4: Updating the Nip 33 Event

Mostro does not update the nip 33 event with the "d" tag "ede61c96-4c13-4519-bf3a-dcf7f1e9d842" to change the status to "Dispute." This is because the order is still active, and the dispute serves as a notification to administrators and the other party about a problem with the order.

### Step 5: Mostro's Nip 33 Event to Show the Dispute

Mostro broadcasts a nip 33 event to show the dispute, for example:

```json
[
  "EVENT",
  "RAND",
  {
    "id": "4a4d63698f8a27d7d44e5669224acf6af2516a9350ae5f07d3cb91e5601f7302",
    "pubkey": "dbe0b1be7aafd3cfba92d7463edbd4e33b2969f61bd554d37ac56f032e13355a",
    "created_at": 1703016565,
    "kind": 38383,
    "tags": [
      ["d", "efc75871-2568-40b9-a6ee-c382d4d6de01"],
      ["s", "Pending"],
      ["y", "mostrop2p"],
      ["z", "dispute"]
    ],
    "content": "",
    "sig": "00a1da45c00684c5af18cf292ca11697c9e70f2a691e6cd397211e717d2f54362dd401d7567da8184a5c596f48a09693479e67214c23e773523a63d0b1c3f537"
  }
]
```

### Step 6: Administrator Actions

Mostro administrators can view the dispute using the dispute ID "efc75871-2568-40b9-a6ee-c382d4d6de01" and take action:

```json
{
  "Dispute": {
    "version": 1,
    "id": "efc75871-2568-40b9-a6ee-c382d4d6de01",
    "pubkey": null,
    "action": "AdminTakeDispute",
    "content": null
  }
}
```

### Step 7: Confirmation to the Administrator

Mostro sends a confirmation message to the administrator with the order details:

```json
{
  "Dispute": {
    "version": 1,
    "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
    "pubkey": null,
    "action": "AdminTakeDispute",
    "content": {
      "Order": {
        "id": "ede61c96-4c13-4519-bf3a-dcf7f1e9d842",
        "kind": "Sell",
        "status": "Active",
        "amount": 0,
        "fiat_code": "VES",
        "fiat_amount": 100,
        "payment_method": "face to face",
        "premium": 1,
        "master_buyer_pubkey": "0000147e939bef2b81c27af4c1b702c90c3843f7212a34934bff1e049b7f1427",
        "master_seller_pubkey": "00000ba40c5795451705bb9c165b3af93c846894d3062a9cd7fcba090eb3bf78",
        "buyer_invoice": "lnbcrt11020n1pjcypj3pp58m3d9gcu4cc8l3jgkpfn7zhqv2jfw7p3t6z3tq2nmk9cjqam2c3sdqqcqzzsxqyz5vqsp5mew44wzjs0a58d9sfpkrdpyrytswna6gftlfrv8xghkc6fexu6sq9qyyssqnwfkqdxm66lxjv8z68ysaf0fmm50ztvv773jzuyf8a5tat3lnhks6468ngpv3lk5m7yr7vsg97jh6artva5qhd95vafqhxupyuawmrcqnthl9y",
        "created_at": 1698870173
      }
    }
  }
}
```

### Step 8: Broadcasting the Nip 33 Dispute Event

Mostro broadcasts a new nip 33 dispute event to update the dispute status to "InProgress":

```json
[
  "EVENT",
  "RAND",
  {
    "id": "2bb3f5a045bcc1eb057fd1e22c0cece7c58428a6ab5153299ef4e1e89633fde9",
    "pubkey": "dbe0b1be7aafd3cfba92d7463edbd4e33b2969f61bd554d
}
```

# Consider
In conclusion, the process of initiating a dispute on Mostro involves a series of simple steps outlined in this guide. Users can follow these steps to address issues with orders effectively. However, for a comprehensive understanding and detailed information, it is highly recommended to visit the official documentation at [Mostro Messages Overview](https://mostro.network/messages/overview.html). The documentation provides in-depth insights, additional details, and ensures a complete understanding of the Mostro dispute resolution system. Happy trading on Mostro!




