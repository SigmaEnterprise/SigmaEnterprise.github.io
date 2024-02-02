# The Evolution of NoStream Relays: Monetizing the Future with ZBD API

![](https://image.nostr.build/84c811f371510ec24026299cd37907a242c8314d6946801fd7128ba4379c66d6.gif)

---

If you've been keeping up with the latest in decentralized data protocols, NoStream is likely on your radar. NoStream, a versatile communications protocol, has been gaining traction, particularly in the realm of social media. Platforms like Snort, Damus, and Amethyst are ushering in a new era by adopting NoStream.


*NoStream Officially on the Apple App Store with Damus*

The growth of NoStream has been nothing short of extraordinary. With a surge in client apps, advanced relay implementations, and a bustling developer community, NoStream is evolving rapidly. GitHub stars serve as a testament to its popularity, surpassing similar protocols like Bitcoin, IPFS, and LND.

### Network Growth

As the NoStream network expands, discussions around monetization models become crucial. The distributed relay infrastructure, responsible for storing events, handling compute cycles, and relaying data to users, incurs trivial costs. Currently, enthusiasts run all NoStream relays, bearing the financial burden themselves. For sustainable growth, incentivizing relay operators through monetization is possible

### Fee Monetization

While conceptualizing monetization strategies for NoStream relays is exciting, implementing them presents unique challenges. The innovation lies in leveraging Bitcoin for monetization, utilizing its decentralized nature and Lightning Network for seamless, low-cost transactions.

#### Storage (Pay per Size)

Charging users based on the data they store on NoStream relays offers a viable model. Relay operators could consider pricing in satoshis per megabyte of stored event data.

#### Publication (Pay per Event)

A 'pay-for-what-you-use' model, charging users per event, is another avenue worth exploring. However, friction and microtransactions may pose challenges to widespread adoption.

#### Admission (Pay per Pubkey)

A simpler approach involves a whitelist of users who pay an admission fee set by the relay operator. This not only monetizes the service but also acts as a deterrent against spam and ensures a stable NoStream experience.

### Enter NoStream + ZBD

**NoStream**, particularly the feature-rich implementation called **NoStream (Nostream)**, stands out. Authored and maintained by Ricardo Arturo, a core NoStream contributor, Nostream is written in TypeScript and offers extensive features, including support for NIPs, rate limiting, blocklisting, and more.

#### Paid Relay Access

Nostream's latest feature introduces paid relay access through the ZBD API. By connecting a ZBD API key and configuring a few settings, relay operators can monetize their services through the Lightning Network.

### How It Works

- Visit the paid Nostream relay [nostr.land]https://nostr.land/().
- Users encounter a one-time admission fee screen along with customizable Terms of Service.
- Payment orchestration occurs through the Bitcoin Lightning Network, offering a seamless experience.
- Once payment is complete, the user's public key joins the relay's allowlist, granting access.

*Note: [Ricardo](https://eden.nostr.land) runs a paid Nostream relay instance at [eden.nostr.land](https://eden.nostr.land) for users to experience the payment flow.*

This innovative approach paves the way for simplified monetization of NoStream relays, addressing storage, compute, and bandwidth costs. With ZBD integration, NoStream takes a leap towards a sustainable and scalable future.

### Future Paths

Even with the initial implementation, potential future paths emerge:

- Defining NIPs for relays to send payment requests directly to clients.
- Exploring subscription services to notify users about impending access termination without payment.

In the face of NoStream's rapid user influx, one fact remains evident: free relays struggle under demand, while paid relays offer reliable services.

*Recommended: Consider adopting NoStream relays with ZBD integration for a seamless and monetized user experience.*


# Exploring the NoStream Revolution with CodeSpaces

In the dynamic landscape of decentralized communication protocols, NoStream stands out as a revolutionary force. This article delves into the heart of the NoStream repository, exploring its features, functionalities, and the power it holds in reshaping the way we communicate.

## NoStream: Unleashing the Future

[NoStream](https://github.com/Cameri/nostream) is a generic communications protocol that has gained significant attention, particularly in the realm of social media. Developed by a dedicated community, the repository serves as the epicenter of innovation for NoStream applications and relays.

### Getting Started with CodeSpaces

Before we delve into the repository, let's explore the convenience of [CodeSpaces](https://github.com/features/codespaces), GitHub's integrated development environment. CodeSpaces allows you to spin up a fully functional development environment directly within your browser. It streamlines the setup process and ensures a consistent and collaborative coding experience.

```bash
# Clone the NoStream repository
git clone https://github.com/Cameri/nostream.git
cd nostream
```

Now, let's initiate CodeSpaces for seamless development:

1. Click on the "Code" dropdown on the NoStream repository.
2. Select "Open with CodeSpaces."

Voila! You're now equipped with a fully configured environment to explore and contribute to NoStream.

## Nostream Features

```plaintext
Features
NIPs with a relay-specific implementation are listed here.

 NIP-01: Basic protocol flow description
 NIP-02: Contact list and petnames
 NIP-04: Encrypted Direct Message
 NIP-09: Event deletion
 NIP-11: Relay information document
 NIP-11a: Relay Information Document Extensions
 NIP-12: Generic tag queries
 NIP-13: Proof of Work
 NIP-15: End of Stored Events Notice
 NIP-16: Event Treatment
 NIP-20: Command Results
 NIP-22: Event created_at Limits
 NIP-26: Delegated Event Signing (REMOVED)
 NIP-28: Public Chat
 NIP-33: Parameterized Replaceable Events
 NIP-40: Expiration Timestamp
Requirements
Standalone setup
PostgreSQL 14.0
Redis
Node v18
Typescript
Docker setups
Docker v20.10
Docker Compose v2.10
Local Docker setup
Docker Desktop v4.2.0 or newer
mkcert
WARNING: Docker distributions from Snap, Brew or Debian repositories are NOT SUPPORTED and will result in errors. Install Docker from their official guide ONLY.
```

## Contributing to the Revolution

NoStream is a community-driven project, and contributions are not just welcome but encouraged. Whether you're a seasoned developer or a newcomer, the repository provides a fertile ground for collaboration. Check the [contributing guidelines](https://github.com/Cameri/nostream/blob/main/CONTRIBUTING.md) to understand how you can be part of this exciting revolution.

## # Harnessing the Power of NoStream: A Guide to Accepting Payments

Embracing the decentralized communication revolution, NoStream has become a pivotal force in reshaping how we connect. In this guide, we'll explore the intricacies of accepting payments on NoStream, unlocking a world of possibilities for developers and content creators.

## Before You Begin: Quick Start

To embark on the journey of accepting payments via NoStream, ensure you've completed one of the Quick Start guides provided in the documentation. Additionally, create a `.env` file and make specific changes in the `.nostr/settings.yaml` file to set the stage for payment integration.

```bash
# Example .env file setup
SECRET=your_secret_key_here
# Other environment variables as per your configuration
```

Now, let's delve into the specific changes needed in the `.nostr/settings.yaml` file:

- Set `payments.enabled` to true.
- Enable admission fees by setting `payments.feeSchedules.admission.enabled` to true.
- Adjust `limits.event.pubkey.minBalance` to the minimum balance required in msats (e.g., 1000000 for a balance of 1000 sats).

## Choosing Your Payment Processor

NoStream provides flexibility in choosing payment processors. Below, we'll explore the setup process for some prominent options.

### 1. ZEBEDEE Integration

[ZEBEDEE](https://zebedee.io/) offers a seamless payment integration experience with NoStream. Follow these steps:

- Sign up for a ZEBEDEE Developer Dashboard account.
- Create a new LIVE Project and obtain the Project's API Key.
- Set the `ZEBEDEE_API_KEY` environment variable in your `.env` file.

```bash
ZEBEDEE_API_KEY=your_zebedee_api_key_here
```

- Configure settings in the `.nostr/settings.yaml` file for ZEBEDEE integration.
- Restart NoStream for changes to take effect.

For a detailed guide, refer to [Set Up a Paid Nostr Relay with ZEBEDEE API](https://github.com/Cameri/nostream/blob/main/docs/guides/zebedee.md).

### 2. Nodeless Integration

[Nodeless](https://nodeless.com/) brings simplicity to the payment integration process. Here's how to set it up:

- Sign up for a Nodeless account and create a new store.
- Generate an API key and note the store ID.
- Configure the `.env` file with `NODELESS_API_KEY` and `NODELESS_WEBHOOK_SECRET`.

```bash
NODELESS_API_KEY=your_nodeless_api_key
NODELESS_WEBHOOK_SECRET=your_nodeless_webhook_secret
```

- Update settings in `.nostr/settings.yaml` for Nodeless integration.
- Restart NoStream for the changes to take effect.

### 3. OpenNode Integration

[OpenNode](https://www.opennode.com/) provides a robust platform for payment processing on NoStream:

- Sign up for a new OpenNode account and get verified.
- Create a new API Key with Invoices permission.
- Set the `OPENNODE_API_KEY` environment variable in your `.env` file.

```bash
OPENNODE_API_KEY=your_opennode_api_key
```

- Adjust settings in `.nostr/settings.yaml` for OpenNode integration.
- Restart NoStream to apply the changes.

### 4. LNbits Integration

[LNbits](https://lnbits.com/) brings Lightning Network capabilities to NoStream:

- Create a new wallet on your public LNbits instance.
- Obtain the wallet Invoice/read key.
- Set the `LNBITS_API_KEY` environment variable in your `.env` file.

```bash
LNBITS_API_KEY=your_lnbits_api_key
```

- Configure settings in `.nostr/settings.yaml` for LNbits integration.
- Restart NoStream to activate the changes.

### 5. LNURL Provider Integration

Integrate any LNURL Provider with LNURL-verify support:

- Create an account with an LNURL Provider if you don't have one.
- Update `.nostr/settings.yaml` with the chosen LNURL provider details.
- Restart NoStream for the configuration to take effect.

## Testing Your Payment Integration

To ensure a seamless payment experience, follow these steps:

1. Visit your NoStream domain.
2. Complete the admission fee form presented.
3. Pay the invoice as instructed.
4. Wait for the payment confirmation.
5. Add your relay URL to your preferred Nostr client.
6. Send test notes to validate the integration.

## Docker Compose Quick Start

For those preferring Docker Compose, follow these steps:

```bash
# Clone repository and enter directory
git clone https://github.com/yourusername/nostream.git
cd nostream
# Generate a secret and paste it into an .env file
echo "SECRET=$(openssl rand -hex 128)" > .env
# Start NoStream
./scripts/start
```

## Running as a Service

To run NoStream as a service, consider setting it up using systemd:

1. Create a systemd service file (replace placeholders):

```ini
[Unit]
Description=NoStream TS Relay
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=5
User=your_username
WorkingDirectory=/path/to/nostream
ExecStart=/path/to/nostream/scripts/start
ExecStop=/path/to/nostream/scripts/stop

[Install]
WantedBy=multi-user.target
```

2. Enable and start the service:

```bash
systemctl enable nostream
systemctl start nostream
```

3. View logs with:

```bash
journalctl -u nostream
```

## Standalone Quick Start

For a standalone setup, configure the environment variables and initialize the database:

```bash
# Set environment variables
# Example variables, adjust as needed
DB_HOST=localhost
DB_PORT=5432
DB_NAME=nostr_ts_relay
DB_USER=postgres
DB_PASSWORD=postgres
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_USER=default
REDIS_PASSWORD=nostr_ts_relay
SECRET=your_secret_key_here

# Create the nostr_ts_relay database
psql -h $DB_HOST -p $DB_PORT -U $DB_USER -W
postgres=# create database nostr_ts_relay;
postgres=# quit

# Start Redis and set the default password
redis-cli
127.0.0.1:6379> CONFIG SET requirepass "nostr_ts_relay"
OK
127.0.0.1:6379> AUTH nostr_ts_relay
Ok
```

Continue with the repository setup:

```bash
# Clone repository and enter directory
git clone https://github.com/yourusername/nostream.git
cd nostream
# Install dependencies
npm install -g knex
npm install
# Run migrations
NODE_OPTIONS="-r dotenv/config" npm run db:migrate
# Start NoStream
npm run start
```

## Testing and Development

For testing and development, execute the following commands:

```bash

# Run unit tests

npm run test:unit

# Run unit tests in watch mode

npm run test:unit:watch

# Run unit test coverage

npm run cover:unit

# Run integration tests with Docker Compose

npm run docker:test:integration

# Run integration test coverage



# Closing Thoughts

Running three relay databases in the context of NoStream can be perceived as a small and trivial cost, especially when considering the broader utility and the potential for monetizing interactions within friend-to-friend tribes. Let's break down the reasons behind this perspective:

1. **Decentralization and Redundancy:**
   
   - NoStream operates on a decentralized model where multiple relay databases contribute to the network. This decentralization ensures redundancy and fault tolerance.
   - Running multiple relay databases distributes the load and mitigates the risk of a single point of failure. If one relay goes down, others continue to function, maintaining the availability of the NoStream network.

2. **Resilience to Network Growth:**
   
   - As the NoStream network continues to grow, the demand for relay services increases. Having multiple relay databases accommodates this growth seamlessly, ensuring a consistent and reliable user experience.
   - Distributing the load across multiple relays helps in scaling the network infrastructure efficiently.

3. **Cost-Effective Scaling:**
   
   - The cost of running three relay databases is often relatively small compared to the benefits gained in terms of network reliability, scalability, and performance.
   - NoStream's lightweight protocol and the distributed nature of relays make it feasible to maintain multiple instances without incurring exorbitant costs.

4. **Monetization Opportunities:**
   
   - Monetizing friend-to-friend interactions within tribes becomes more viable with the reliability and scalability provided by multiple relay databases.
   - Each relay database can potentially serve as a monetization point, allowing relay operators to earn returns on their server infrastructure provisioning.

5. **Enhanced User Experience:**
   
   - Having three relay databases contributes to a smoother and more responsive user experience. Users interacting within friend-to-friend tribes benefit from reduced latency and faster access to shared notes and events.

6. **Incentivizing Relay Operators:**
   
   - Introducing a monetization model encourages relay operators to invest in maintaining and expanding their infrastructure. This incentive structure ensures that there's a continual commitment to providing reliable relay services.

7. **Security and Anti-Spam Measures:**
   
   - Running multiple relay databases aids in implementing effective security measures and anti-spam protocols. It becomes easier to detect and mitigate adversarial conditions, ensuring the integrity of the NoStream network.

In conclusion, the decision to run three relay databases is strategic and aligns with the principles of decentralization, scalability, and incentivization within the NoStream ecosystem. While the initial cost may be considered trivial, the long-term benefits in terms of network robustness and the potential for monetization make it a prudent and forward-thinking approach.

---
