![Satoshi Approves](https://image.nostr.build/8df4394dfe7337e444b4750b0fcc2d81a59af210c1c1f306c97a380271e09ef9.jpg)

> “Another possible form of ecash could be based on Wei Dai's b-money. This is like hashcash, something which represents a measurable amount of computational work to produce. It therefore can't be forged. This could be a very robust payment system and is worth pursuing further.”

# Cashu: Privacy-Preserving Ecash System for Bitcoin

> **Cashu** is a free and open-source Chaumian ecash system designed specifically for Bitcoin. Offering near-perfect privacy for users of custodial Bitcoin applications, Cashu ensures that personal information, fund amounts, and transaction parties remain confidential.

## Cashu Protocol: Open and Implementable

> Cashu stands as an open ecash protocol available for implementation by anyone. The **Cashu NUTs** (Notation, Usage, and Terminology) outline the specifications for implementing the protocol, making it accessible for developers to build their own wallets.

### Libraries

> Various Cashu libraries provide developers with tools to create wallets, mints, and other services that leverage the Cashu protocol.

Certainly! Here's a rewritten article in Markdown format:

---

# The Cashu Protocol

> **Cashu** is an open-source ecash protocol designed for Bitcoin. Being an open protocol, it allows everyone to develop their own software, fostering interaction among various Cashu applications. Applications adhering to the specifications ensure compatibility within the broader ecosystem.

## BDHKE: Blind Diffie-Hellmann Key Exchange

> The **Blind Diffie-Hellmann Key Exchange (BDHKE)** serves as the foundational cryptographic scheme within the Cashu protocol for both signing and redeeming ecash tokens. In this model, three essential actors play distinct roles:

- **Sending user: Alice**
- **Receiving user: Carol**
- **Mint: Bob**

### Bob (Mint) - Key Components

- **k:** Private key of the mint (distinct for each amount)
- **K:** Public key of the mint
- **Q:** Promise (blinded signature)

### Alice (User) - Key Components

- **x:** Random string (secret message), corresponding to point Y on the curve
- **r:** Private key (blinding factor)
- **T:** Blinded message
- **Z:** Proof (unblinded signature)

#### Blind Diffie-Hellmann Key Exchange (BDHKE) Steps

1. **Mint (Bob):** Publishes public key \( K = kG \).
2. **Alice:** Picks secret \( x \) and computes \( Y = \text{hash\_to\_curve}(x) \).
3. **Alice to Bob:** Sends \( B_ = Y + rG \) with \( r \) being a random blinding factor (blinding).
4. **Bob to Alice:** Sends back blinded key \( C_ = kB_ \) (DH key exchange and signing).
5. **Alice:** Calculates unblinded key as \( C_ - rK = kY + krG - krG = kY = C \) (unblinding).
6. **Alice to Carol:** Takes the pair \( (x, C) \) as a token and sends it to Carol.
7. **Carol to Bob:** Sends \( (x, C) \) to Bob, who checks that \( k \times \text{hash\_to\_curve}(x) == C \) (verification). If valid, treats it as a spend of a token, adding \( x \) to the list of spent secrets.

## NUTs: Notation, Usage, and Terminology

> **Cashu NUTs** provide detailed specifications for the Cashu protocol. For a comprehensive understanding and implementation guide, refer to the [Cashu NUTs (Notation, Usage, and Terminology)
> ](https://github.com/cashubtc/nuts).

---

Feel free to replace "link-to-nuts" with the actual link to the Cashu NUTs documentation. Adapt the content as needed for your specific context.

## Implementations in Various Languages

### Python

```python
# Cashu Nutshell Python Library
import cashu_nutshell
```

### TypeScript

```typescript
// Cashu-TS TypeScript Library
import cashu_ts from 'cashu-ts';
```

### Rust

```rust
// Cashu Rust Libraries
use cashu_crab;
use cashu_rs;
```

### Golang

```go
// Cashu-Feni Golang Library
import "github.com/cashu-feni/cashu-feni";
```

### Kotlin

```kotlin
// Cashu Client Library in Kotlin
import cashu_client;
```

### Dart

```dart
// Cashu Dart Library
import 'package:cashu_dart/cashu_dart.dart';
```

## Cashu Mints

### Nutshell

> **Nutshell** serves as the reference mint implementation in Python.

### Moksha

> **Moksha** is a Rust-based Cashu wallet and mint, providing additional flexibility and functionality.

### Cashu-rs-mint

> **Cashu-rs-mint** stands as a Rust-based mint implementation, offering a robust solution for secure transactions.

### Feni

> **Feni** is a Golang mint, contributing to the variety of available mint implementations.

## LNbits Extension

> The **Cashu LNbits extension** empowers LNbits users to run their own Nutshell mint, enhancing their control over the security and privacy of their transactions.

---
