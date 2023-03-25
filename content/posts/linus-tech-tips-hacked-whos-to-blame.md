---
title: Linus Tech Tips Hacked. Who's to Blame?
date: 2023-03-24
---

First, some background: Henry and I discussed this topic on [Episode 8](https://dispatch.techlore.tech/p/linus-tech-tips-hacked-what-happened) of the Techlore Talks podcast, and if you watch YouTube yourself and haven’t been living under a rock, you probably already know: Early in the morning (Pacific Time), Linus Media Group’s (LMG) three biggest channels were hacked, with the branding changed and livestreams posted promoting cryptocurrency scams.

Within a matter of hours, all three channels were completely gone, with links to the channels and any of their videos reporting that the channels had been terminated for YouTube community guideline violations. One of the biggest tech personalities on the platform was just gone.

## The Hack

By the time you’re reading this, Linus Tech Tips has not only been restored, but they’ve [posted](https://www.youtube.com/watch?v=yGXaAWbzl5A) a video themselves with more detail about what went wrong, and there’s a lot of interesting takeaways here for both YouTube and LMG.

To Linus’ credit, he covered a lot of the potential attacks and solutions that we discussed in this response video, so it’s clear that his team — and likely Google’s by extension — are considering all of these things already, but I’ll share a bit more of my insight into all of this here.

### Google's Advanced Protection Program

One glaring issue with Google’s protection of their own high-profile users is the lack of awareness around Google’s [Advanced Protection Program](https://landing.google.com/advancedprotection/), we touched on this in our podcast a bit, and it’s now clear from this video that Linus was not enrolled. In the video he states that Google Prompt 2FA cannot be disabled and is susceptible to “[fatigue attacks](https://www.beyondtrust.com/resources/glossary/mfa-fatigue-attack)“ where attackers will constantly send prompts hoping eventually you accidentally approve one, which is completely true! …For regular Google accounts anyways. Accounts enrolled in the Advanced Protection Program have 2FA methods other than Hardware Security Keys completely disabled, including Google Prompts.

However, in this case two-factor authentication — or even password theft — was ultimately not the issue at hand.

### Stolen Account Session Tokens

One attack possibility we considered was a malware-based attack that has been going around targeting YouTubers large and small, and this appears to have been what compromised Linus’ channels at the end of the day.

When you log in to a website like YouTube, an authentication token is stored as a cookie in your browser, and if that token is somehow stolen your entire account is at risk. In the YouTube space, a very common method hackers use to steal your browser cookie information is to send content creators sponsorship offers with malware-laden PDF attachments. Open it up and within a matter of seconds your channel can be automatically taken over in exactly the same manner as Linus Tech Tips. Some sales employee at LMG did exactly this, and the credentials stored in their browser were enough to take half of the company completely offline.

### YouTube Content Manager Access

Of course, Linus is not completely ignorant when it comes to account security! He isn’t sharing the username and password for his main channel accounts with every employee in the company. Instead, they delegate management access to the channel via a feature in YouTube Content Manager which allows you to grant certain permissions to other Google accounts. That way, each employee can have the access they need secured behind their own account.

This is a double-edged sword as Linus discovered though. In an attack like this, it can be difficult to find and secure the account which was actually impacted. As Linus put it in his explainer video: You are essentially going from having to secure one giant vault door, to twenty smaller vault doors, each of which might ultimately end up in the same place.

However, Linus also made a critical mistake when setting this access up. Henry covered this well in our podcast episode yesterday, but it sounds like LMG failed to follow the “[principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege)” when delegating access to Content Manager, giving their employees too much access to the channels than they probably needed. This is usually done to make certain operations more convenient, but if the sales rep whose browser was compromised only had the specific access to the channel that they needed for their daily work, it’s likely that this compromise wouldn’t have happened.

### Google is at Fault

It is easy to blame the victim when it comes to attacks like these. LMG certainly could’ve employed better opsec, have trained themselves on how to respond to critical events like this ahead of time, and better educated themselves on the current state of cybercrime in their industry. Other prominent tech YouTubers have been [warning](https://www.youtube.com/watch?v=xf9ERdBkM5M) their fellow content creators about these attacks for a while now, and awareness might have prevented this specific attack from taking place.

However, Linus’ response to the attack as it was happening really highlights Google’s role in the whole thing, and ultimately this is something that needs to be improved on YouTube’s end.

For one thing, YouTube **needs** to restrict sensitive operations behind re-authentication prompts if you’re already logged in. Posting a livestream is one thing, but changing the name and handle of a channel? The attackers should simply not have access to do that with session tokens alone regardless of the permissions the hacked account may have. If Google had asked for a password or 2FA prompt before allowing those changes, they would have been stopped in their tracks. This is commonplace for security-focused websites, GitHub calls this “[sudo mode](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/sudo-mode),” but is surprisingly uncommon for major social media sites like YouTube, and they need to do better. This same concept could be applied to mass changes. Of course it’s very convenient to unlist a video or two without being prompted for your password every time, but when the YouTube API is used to mass unlist every video on a channel, that should raise some red flags.

YouTube also needs better tooling to log out existing sessions and restrict existing user’s access. One of the very first responses Linus had to the attack was to change the primary account’s password, a common and reasonable first response to a hack like this. That change should have immediately triggered all devices **and** connected users to be logged out of the channel until they individually re-authenticate, but it seems that this action alone does not invalidate session tokens, so the hackers were unaffected and precious time was wasted.

When Linus finally did get around to restricting his employee’s access to Content Manager, he also ran into issues with buggy software preventing the changes from being made. YouTube needs to have an intuitive way to quickly lock down an account in one click for critical situations like these, there can’t be any room for error or “refresh and try again” prompts for disaster response security actions.

## Businesses Are Responsible for User Security

If you run a business, your customers and partners **will** get hacked, and it is **your** responsibility — especially in the tech industry — to mitigate the damage that can be done by the hackers: the victims cannot shoulder the blame. With a high profile attack like this, there’s no doubt that teams at YouTube at the highest levels are now considering all of these things and working on solutions, but it should not have taken this long for those teams to start asking these questions. Smaller content creators have been plagued with this issue and similar problems for a long time, and proper security mitigations should have been the first thing implemented on YouTube’s end.

Finally, when you have optional security features you need to make sure that your users are aware of them. If you operate any sort of user-facing website with optional [multi-factor authentication](https://www.privacyguides.org/en/basics/multi-factor-authentication/) for example, the ability to enable that needs to be placed front and center for your customers, not hidden behind a setting they need to seek out. If you’re Google and you literally have a whole [program](https://landing.google.com/advancedprotection/) which provides advanced protection for high-profile accounts, high-profile content creators need to know about this program! It sounds like Linus still might not, and I’ve heard from other content creators facing similar hacks that their reps at YouTube only let them know about it following the attack. It might be nice for your creators to be ahead of the curve when it comes to things like this. It’s not clear whether the Advanced Protection Program would have protected them in this case, but it might have, because account sessions are much more strictly controlled for enrollees. And even if it wouldn’t have stopped this particular attack yet, it would prevent a wide range of other attacks that prominent YouTube content creators are susceptible to.

## Takeaways

Information security is something that every single person needs involvement in, and regular computer users can only go so far in [protecting their accounts and data online](https://www.privacyguides.org/en/). Internet-facing services need to be designed with a security-first approach in mind, especially when people’s livelihoods depend on them, an increasingly common occurrence these days.

Luckily, Linus’ channels were eventually restored, and it’s unlikely they’ll see long-term damage. But can the same be said for smaller creators on the platform? YouTube creators shouldn’t settle for inadequate protections for all but the largest and most popular channels.

---

I am a digital privacy advocate and educator working on the non-profit Privacy Guides knowledgebase and the Techlore YouTube channel, with the goal of making privacy and security resources accessible to anybody interested in protecting their data. If you like the work I do, please consider sponsoring my work on [Ko-Fi](https://ko-fi.com/jonaharagon) or [GitHub Sponsors](https://github.com/sponsors/jonaharagon), it would be hugely appreciated. Thanks for reading, and I hope you learned something new!
