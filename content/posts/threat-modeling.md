---
title: "Threat Modeling: The First Skill You Need To Begin Your Privacy Journey"
date: 2021-09-13
---

_I [originally](https://medium.com/privacyguides/threat-modeling-the-first-skill-you-need-to-begin-your-privacy-journey-2116fd81d7ac) wrote this piece for the_ Privacy Guides _blog, although the information herein has been largely superseded by my contributions to their [Threat Modeling](https://www.privacyguides.org/basics/threat-modeling/) and [Common Threats](https://www.privacyguides.org/basics/common-threats/) pages, which I recommend exploring._

---

The major trade-off with many privacy-centric services and software I’ve seen is that in general, the more private and secure something is, the more restricting or less convenient it is. This balancing act between high security and privacy, and usability and convenience is one of the trickiest problems to overcome both when creating software and services and when choosing which services to use.

“Convenience” is something I’ve seen many privacy advocates overlook or give little credence to, because it’s not really a technical problem that can be easily resolved, or it doesn’t jibe with their vision of what an **ideally** private and secure tool should look like. But social problems like these are still incredibly important to consider anyway, what good is a service that takes extreme steps to protect your privacy if you never want to use it?

When I was working with PrivacyTools, one of the complaints I heard most often was that the tools we would recommend were just too hard to start using in the first place!

If you wanted to use the _most_ secure tools available, you’d have to sacrifice a lot of usability. Even then, it’s impossible to guarantee any system is completely secure. There’s **high** security, but never **full** security. How do you decide how high is _high enough_ for you? Answering that question is where threat modeling comes into play.

## So, what even _are_ threat models?

A threat model is a list of the most probable threats to your security/privacy endeavors. Since it’s impossible to protect yourself against **every** attack(er), you should focus on the **most probable** threats. In computer security, a threat is a potential event that could undermine your efforts to stay private and secure.

By focusing on the threats that matter to you, this narrows down your thinking about the protection you need, so you can choose the tools that are right for the job.

Some examples:

- An investigative journalist’s threat model might be _protecting themselves against_ a foreign government.
- A company’s manager’s threat model might be _protecting themselves against_ a hacker hired by competition to do corporate espionage.
- The average citizen’s threat model might be _hiding their data from_ large tech corporations.

## Crafting Your Threat Model

The important thing to remember is that everyone’s threat model is different, and people have very different concerns for different reasons. To figure out what the best plan is for **you**, try answering these five questions:

1. What do I want to protect?
2. Who do I want to protect it from?
3. How likely is it that I will need to protect it?
4. How bad are the consequences if I fail?
5. How much trouble am I willing to go through to try to prevent potential consequences?

To demonstrate how these questions work, let’s look into what they are really asking and build a plan to keep your house and possessions safe.

### What do you want to protect?

If you think absolutely everything is worth protecting, a better way to think about this question could be: _what do you have that is worth protecting?_

An “asset” is something you value and want to protect. When it comes to protecting your home, your assets might include jewelry, electronics, important documents, or photos.

In the context of digital security, an asset is usually some kind of information. For example, your emails, contact lists, instant messages, location, and files are all possible assets. Your devices themselves may also be assets.

### Who do you want to protect these assets from?

To answer this question, it’s important to identify who might want to target you or your information. Any person or entity that poses a threat to your assets is an **adversary**. Examples of potential adversaries could include your former partner, your business competition, your government, or a hacker on a public network.

When it comes to securing your home, most people consider burglars as their primary adversary, but other adversaries to consider could include roommates and guests.

### How likely is it that you will need to protect your belongings?

Risk is the likelihood that a particular threat against a particular asset will actually occur. It goes hand-in-hand with capability. While your mobile phone provider has the capability to access a lot of your data, the risk of them posting your private data online to harm your reputation is low.

Assessing risks is both a personal and a subjective process. Many people find certain threats unacceptable no matter the likelihood they will occur because the mere presence of the threat at any likelihood is not worth the cost. In other cases, people disregard high risks because they don’t view the threat as a problem.

This question usually only leads to more questions, but thinking about them should give you a deeper understanding of what steps you actually need to take. In our example you might ask yourself:

- Does my neighborhood have a history of burglaries?
- How trustworthy are my roommates/guests?
- What are the capabilities of my adversaries?
- What are the risks I should consider?

### How bad are the consequences if you fail?

There are many ways that an adversary could gain access to the assets you’re protecting. These tactics and your adversaries’ motives vary widely. For example, a government trying to prevent the spread of a video showing police violence may be content to simply delete or reduce the availability of that video. In contrast, a political opponent may wish to gain access to secret content and publish that content without you knowing to harm your campaign.

Security planning involves understanding how bad the consequences could be if an adversary successfully gains access to one of your assets. To determine this, you should consider the capability of your adversary. For example, your mobile phone provider has access to all your phone records. A hacker on an open Wi-Fi network can access your unencrypted communications. Your government might have stronger capabilities.

In our home protection example, some things you could consider include:

- Do you have anything in your house that you cannot replace?
- Do you have the time or money to replace these things?
- Do you have insurance that covers goods stolen from your home?

### How much trouble are you willing to go through to prevent these consequences?

This is really a question of prioritization, and some of this comes down to operating within your means. Consider things like:

- Are you willing to buy a safe for sensitive documents?
- Can you afford to buy a high-quality lock?
- Do you have time to open a security box at your local bank and keep your valuables there?

No matter what security solution you choose to implement, there is usually a _better_ option out there. Always chasing that perfect solution can become a silly endeavor when the cost to you outweighs any potential benefit, or when it protects against a threat you’ll probably never face.

For cryptocurrency users a hardware wallet is the most secure way to handle your funds, but it probably does not make sense to spend $100 on a hardware wallet simply to protect $100 of cryptocurrency, maybe even $1000, etc.

For homeowners, outfitting your windows with bulletproof glass and installing steel doors probably doesn’t make sense when the threats you realistically face will probably be deterred by decent locks and an alarm system.

## Summary

Where all these lines are drawn will always come down to personal choice: Only you can determine what will work the best for you. Just remember that not everything is black and white, while there are [resources to point you in the right direction](https://privacyguides.org/), nobody can tell you exactly what to use to achieve some perfect level of privacy.
