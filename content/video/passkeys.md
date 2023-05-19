---
title: 'Passkeys: Good or Bad?'
date: 2023-05-09
---

<div style="position: relative; padding-top: 56.25%; margin-bottom: 1rem;"><iframe title="Are Passkeys a Big Tech Tracking Nightmare? Let's Take a Look!" width="100%" height="100%" src="https://neat.tube/videos/embed/0fc71036-b3f1-4140-92c7-598df7fe64c9" frameborder="0" allowfullscreen="" sandbox="allow-same-origin allow-scripts allow-popups" style="position: absolute; inset: 0px;"></iframe></div>

Passkeys have really started taking off since Apple and Google announced native support for them in iOS and Android. They've been in the news again recently, because earlier this month Google announced support for passwordless authentication for Google accounts with Passkeys. So, with big tech companies seemingly going all-in on this technology, I want to take a look at how they work, whether they're better than passwords, and whether they're actually as private as Google claims.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "VideoObject",
  "name": "Are Passkeys a Big Tech Tracking Nightmare? Let's Take a Look!",
  "description": "Passkeys have really started taking off since Apple and Google announced native support for them in iOS and Android. They've been in the news again recently, because earlier this month Google announced support for passwordless authentication for Google accounts with Passkeys. So, with big tech companies seemingly going all-in on this technology, I want to take a look at how they work, whether they're better than passwords, and whether they're actually as private as Google claims.",
  "thumbnailUrl": [
    "https://neat.tube/static/thumbnails/96b86c0f-8543-49fe-9586-bb0bed312efe.jpg"
    ],
  "uploadDate": "2023-05-09",
  "duration": "PT7M35S",
  "embedUrl": "https://neat.tube/videos/embed/0fc71036-b3f1-4140-92c7-598df7fe64c9",
  "contentUrl": "https://neat.tube/w/2X12Cz1Uue2WvUtjNWVJX4"
}
</script>

- [Watch (and subscribe!) on YouTube](https://www.youtube.com/watch?v=4DamjB5lNVg)
- [Watch on Substack](https://jonaharagon.substack.com/p/passkeys-the-good-and-the-bad)
- [Watch on PeerTube](https://neat.tube/w/2X12Cz1Uue2WvUtjNWVJX4)

## What Are Passkeys?

Passkeys aren't some proprietary authentication technology Google and Apple have been cooking up, they're a W3C web standard, a new name for a not-so-new technology: _Discoverable WebAuthn/FIDO credentials_.

While the name "Passkey" itself was never introduced before Apple's 2021 Worldwide Developer Conference, [YubiKey](https://www.privacyguides.org/en/multi-factor-authentication/) has actually supported Passkeys since around 2018 in the YubiKey 5 series. I think Passkey has a much nicer ring to it, so I appreciate the branding. However, this means we actually know a lot about how Passkeys work already!

Passkeys operate with standard public-key cryptography, the same sort of encryption used by HTTPS or PGP. When you add a Passkey to an account, your device—whether that be your phone, a YubiKey, or another FIDO2 capable device—generates two related keys: a **public key** and a **private key**. The public key gets stored on the server of the website, while the private key never leaves your device.

This means that unlike passwords, or TOTP two-factor authentication, there is **no** shared secret at all being transmitted between your device and the server. One benefit of this is that the server does not need to protect the public key, which mitigates damage in the event of a database breach.

All of this makes Passkeys very strong, and very easy-to-use. There's nothing to remember, you just log in with the devices you already have.

### Phishing Protection

We know that passwords and TOTP 2FA codes can be easily phished by an attacker. Passkeys are fundamentally different: They can only be used on the same domain name they were originally registered with, and there's no way someone could be tricked into revealing their secret key. Even if you wanted to, there's no way to extract the secret key from your device.

## The Bad

### Compatibility

At the time of writing, Passkey support is noticeably absent in Firefox and [Linux](https://www.privacyguides.org/en/desktop/), and even Google's new passwordless logins aren't functional on ChromeOS. Passkeys are a work in progress, and it will likely take months or possibly even years for the Passkey ecosystem to be complete.

However, there **is** movement among virtually all OS and browser vendors to introduce Passkey support. Eventually, all the pieces should come together, and we should see broad support for Passkeys on all of these platforms.

### Vendor Lock-in

Another concern at the moment with Passkeys is Google and Apple pushing consumers to set up all their credentials via their phone's default password manager, namely Google Passwords or iCloud Keychain. This is yet another way these companies keep you locked in to their ecosystems.

Don't get me wrong, this isn't to say Google's password sync or iCloud Keychain aren't secure. According to [Ars Technica](https://arstechnica.com/information-technology/2023/05/passwordless-google-accounts-are-easier-and-more-secure-than-passwords-heres-why/), 1Password is planning on launching Passkey support in early June, and I don't doubt more [password managers](https://www.privacyguides.org/en/passwords/) will follow suit.

I suggest most people wait for more third-party options to become available before going all in on Passkeys, but the good news is that it doesn't seem like we'll be waiting long.

## Phone or YubiKey?

There is an important distinction between Passkeys on your phone, and Passkeys on a hardware security device such as a YubiKey. The Passkeys on your phone are **copyable**, because they are stored in a software database and synced between your devices, while Passkeys on a YubiKey are **non-copyable**, they are bound to the physical hardware and can't be copied, backed-up, or synced.

Hardware bound, non-copyable Passkeys are the **gold standard** for modern authentication. It makes security rather simple to understand too, either you have the device in your physical possession letting you log in, or you don't.

Copyable Passkeys in Google Passwords or iCloud Keychain are reduced to the security of your Google/Apple account and encryption passphrase. Still quite secure, especially if you follow the best practices for securing your account, but technically still susceptible to remote attacks.

## Common Misconceptions

### Persistent Tracking

One concern I've heard is that Passkeys could be used as a persistent identifier between websites. The reasoning goes that if you share your public key with two different websites, they could work together and see you’re the same user, with the same public key.

**This is false.** When you register for a website, your device generates a brand new public and private key specifically for that website. When you register for another site, that site gets its own public key from your device, completely independent from the first one.

The public keys shared with the website operators have no personal information attached, and can’t be correlated by websites operators colluding together.

### Biometrics

Another common concern I've seen is that Passkeys require a face or fingerprint scan to be used. However, these biometrics are the exact same as the ones used to unlock your device, and they are never transmitted to a third-party. In fact, we actually suggest most people _do_ use biometric unlock on their phones, because it reduces the risk of PIN theft via shoulder surfing.

If you're really concerned about the use of biometrics, you can always use Passkeys with a passcode or PIN instead.

## Should You Use Them?

Again, I caution the use of vendor password management ecosystems like iCloud Keychain. However, when Passkeys are supported by the password management service you prefer—or if you have a YubiKey!—I would absolutely suggest switching to Passkey authentication. The benefits over passwords are significant.

----------

I’m currently writing an additional blog post for Privacy Guides, which will look at some of the privacy aspects of Passkeys in more detail than this, but the general takeaway is that Passkeys **are** private, and they’re the natural evolution of authentication online.
