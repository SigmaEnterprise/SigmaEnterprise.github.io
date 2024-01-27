# Nostr: The Decentralized and Secure Way to Connect Online

In the world of online accounts and passwords, it can be challenging to keep track of all the personal data we share with various platforms. However, with Nostr, a decentralized protocol, there is no need to register for an account using personal information. Instead, all you need is a set of keys - a public key and a private key.

## How Nostr Works

When you create an account with Nostr, you will be given a set of two keys:

- 🏷️A public key, which will act as your username. This key can be shared and will be public to everyone.
- 🔑A private key, which is like your password. You need to keep it secret, hence the name. This key will grant you access to your account in any platform that is powered by Nostr.

To obtain your set of keys, all you need to do is choose a client for the Nostr protocol, such as [Snort (web)](https://snort.social/), [Damus (iOS)](https://damus.io/), or [Amethyst (Android](https://github.com/vitorpamplona/amethyst), and it will generate them for you. If you are using Nostr on the web, additional security measures can be taken, such as using an external signer application like the [Alby browser extension](https://getalby.com/) or the [Nos2x extension](https://github.com/fiatjaf/nos2x). You can also generate custom private keys with tools like [Rana](https://github.com/grunch/rana).

## Keep Your Private Key Safe

It is crucial to save your private key as it is the only way to recover and re-login to your account in the future. By keeping your private key secure and inaccessible to others, you can ensure that your Nostr account remains safe and secure.

In summary, Nostr provides a decentralized and secure way to connect online without the need for personal data. By using a set of two keys - a public key and a private key - you can create an account and access it on any platform that uses Nostr. Just remember to keep your private key safe and secure, and you'll be ready to connect with others in a decentralized and private way.

# Nostr: Events and Relays

Here's what an event looks like:

`{
"id": "c011...4c43",
"pubkey": "dec1...4fb3",
"created_at": 1671551112,
"kind": 1,
"tags": [],
"content": "good morning!",
"sig": "e1dc...5f1"
}`

Nostr is a decentralized protocol that revolves around events. An event is a small text-only structure that clients send to relays. The only object type in Nostr is the event, and it consists of several fields:

- **id**: A unique identifier for the event. It's a way to refer to the event in the network.
- **pubkey**: The public key of the user who created the event.
- **created_at**: The timestamp when the event was created.
- **kind**: Specifies the type of event. Nostr doesn't limit the event kinds, so developers can engineer any kind they want. For example, there's the plain text note event kind, and the end-to-end encrypted message event kind.
- **tags**: An arbitrary field that can contain any tags developers want to use. A common use is setting the ID of a replied message as a tag.
- **content**: The content of the event.
- **sig**: A cryptographic proof that the owner of the private key associated with the public key published the event.

Relays are the main piece of the Nostr protocol. They store the events received from clients, but they don't communicate with each other. This means that users must connect to at least one shared relay to see each other's events. Users can choose to read, write, or both from/to the relays they are connected to. This allows for flexibility in terms of privacy and control over one's data.

Setting up a relay is cheap and easy, and relays can run on low-end devices like smartphones. The fact that relays don't talk to each other makes it harder for censors to take down the entire network. There are currently [over 100 relays](https://nostr.watch/) spread around the globe, and the network is growing. Nostr has the potential to help fight censorship by allowing users to create portals anywhere they want and escape from censorship.

#### 📜 E2EE Text sharing

[Sendstr](https://sendstr.com/) is an online tool where you can share end to end encrypted text data between two devices through the **nostr** protocol.

#### 📝 Blogs

[Blogstack](https://blogstack.io/) - Write decentralized blogs over relay using nostr w/ ⚡ lightning tips

Here you have some awesome resources to get started:

[Nostr protocol specification](https://github.com/nostr-protocol/nips/blob/master/01.md)

[Nostr NIPS](https://github.com/nostr-protocol/nips)

[Awesome Nostr list](https://www.nostr.net/)

[Projects built with Nostr](https://nostrich.fun/)

[Nostr relay list](https://nostr.watch/)

[Guide: How to set up a Nostr relay](https://usenostr.org/relay.html)
