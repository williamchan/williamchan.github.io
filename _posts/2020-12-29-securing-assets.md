---
layout: post
title:  Securing your assets
date:   2020-12-29 14:38:59 -0800
---

I wrote this guide for myself, family, and friends. Hope you find it useful.

### Guiding principle

The goal is to safeguard our online assets such as brokerage and bank accounts. Be paranoid and assume that your usernames, passwords, email, phone number, and other secrets will be compromised. It is only a matter of time. How can we still safeguard our important assets?

### Minimum security practices

**Rule 1**: Use long, randomized passwords. Never use a password for more than one purpose. The password length should be at least 12, preferably 15 or 20.

The following are insufficient:
* Passwords that follow a pattern, such as 51$1**aapl**7WkU for use on apple.com and 51$1**goog**7WkU for use on google.com. Password databases are often leaked. If your pattern makes sense in your head, it can be discerned by a hacker with simple text processing software.
* Passwords that contain English words or identifying numbers.
* Passwords shorter than length 12.

On easily rentable hardware, many passwords can be cracked by amateur hackers within hours. By adding a [12th or 13th or 14th character](https://blog.1password.com/how-long-should-my-passwords-be/), your password becomes much harder to crack.

Use a password manager to comply with rule 1. 1Password and Lastpass are fine choices.

**Rule 2**: Use two-factor authentication (2FA) by time-based one-time password (TOTP).

Use [Authy from Twilio](https://authy.com/) when possible.

If possible, do not use a phone number, which can be easily ported by an employee or contractor who works at t-mobile/verizon/at&t. More on this below.

If a service does not support 2FA by TOTP, either avoid using that service or be aware of the risk you take by using SMS-based 2FA.

### Threat: sim swap scam

Your cell phone number can be easily ported by an employee or contractor who works at t-mobile/verizon/at&t. This is known as the sim swap scam or “simjacking.” This is how [Jack Dorsey was hacked](https://www.nytimes.com/2019/09/05/technology/sim-swap-jack-dorsey-hack.html). This is how Digits co-founder [Wayng Chang was hacked](https://threader.app/thread/1148066452835950593). This is how people get [millions in cryptocurrency stolen](https://www.nbcnewyork.com/news/national-international/mans-1m-life-savings-stolen-in-cell-phone-scam/1994262/). Do not assume your phone number is a secure “factor” for authentication.

Hackers can figure out your phone number and attempt to port your number onto a new phone. Be aware and contact your cell carrier if you mysteriously lose cell service.

The major cell carriers, including T-Mobile, support passcodes that should be checked by an employee when porting a number to a new phone. The family manager enables this passcode for phone numbers in the plan. However, this [validation step is not always followed by cell carrier employees](https://www.reddit.com/r/tmobile/comments/7nhr0a/psa_port_validation_apparently_does_nothing_to/).

T-Mobile has a secret feature called [NOPORT](https://www.vice.com/en/article/ywa3dv/t-mobile-has-a-secret-setting-to-protect-your-account-from-hackers-that-it-refuses-to-talk-about) that is a software switch to disallow the porting out of phone numbers to another carrier. This feature is only available to previous victims of sim swap scams.

Assuming your phone number will be ported out from under your phone, how do you protect your online accounts? Do not use your phone number as your 2FA. Rely instead on true TOTP by authentication app.

### Threat: password hacked

Successful hacks have taken place at major retailers, banks, even the [US Treasury](https://krebsonsecurity.com/2020/12/u-s-treasury-commerce-depts-hacked-through-solarwinds-compromise/). Every few months, security researchers discover entire databases of personal data including login names, email addresses, phone numbers, and passwords in plain text, often enriched with even more personal data from social media like LinkedIn. These databases are sometimes found on unsecured AWS servers, and sometimes traded amongst hackers.

Any password that is used in more than one location is a security lapse. Any password that follows a discernable pattern is not as safe as you might think.

Assuming your password will be discovered, how do you protect your online accounts? By now, the case for using 2FA by TOTP (time-based one-time password) and a password manager should be clear.

### Recommendations for password manager

As of 2021, the [Wirecutter](https://www.nytimes.com/wirecutter/reviews/best-password-managers/) recommends [1Password](https://1password.com/). [Lastpass](https://www.lastpass.com/) is fine also but its ownership by a private equity group may be reason to choose 1Password instead. With 300+ passwords already stored in my Lastpass, the cost of switching is fairly high for me.

Any of these password managers are easily usable on both a laptop and mobile device. Creating and storing a 20-character password is trivially easy.

The important thing is to use a very long and very strong master password.

Also, enable 2FA on your password manager.

### Recommendations for 2FA application

[Authy from Twilio](https://www.authy.com) is the best. Google has stopped improving its Google Authenticator app. Use Authy even when a website suggests using Google Authenticator.

Authy supports 1) porting your TOTP generators from an [old phone to a new phone](https://support.authy.com/hc/en-us/articles/115012672088-Restoring-Authy-Access-on-a-New-Lost-or-Inaccessible-Phone) and 2) recovering your TOTP generators by a process that takes 24 hours and can involve verification checks by Authy.

Authy also supports [installation on multiple devices](https://authy.com/blog/multi-device/) which may be helpful for some use cases. Changes you make to generators will sync across devices.

Authy requires a login, so be sure to use a strong password! See the rules and recommendations above.

Some services offer [Symantec VIP Access](https://vip.symantec.com/) as the *only* TOTP option. Those services include Schwab, Fidelity, and Etrade. These are unfortunate examples of vendor lock-in. Symantec VIP Access is actually the worst 2FA application because each device contains exactly one passcode generator, meaning that the passcodes are shared in common between Schwab, Fidelity, and any website that specifically uses Symantec VIP.

### 2FA app versus hardware key

A hardware key, like YubiKey, is more secure for TOTPs than mobile apps because the hardware key is dedicated whereas the mobile app runs on a device shared by lots of other apps and web browsers. The drawback is that you have to carry around a physical fob on your keychain. Hardware keys are commonly used by IT professionals.

Consider getting a hardware key for your most sensitive account.

### Recovery scenario: what if I lose my phone?

You need to regain your 2FA generators and setup a new phone with the same phone number.

For 2FA generators, let’s talk about Authy and Symantec VIP Access separately.

You can regain your Authy passcodes by:
1. Already having Authy setup on a backup device. You can use that backup device to remove your lost device.
2. Setup Authy on a new device either with the backup flow or the recover flow. Either way, you need access to your phone number.
    * The **[backup flow](https://authy.com/features/backup)** requires that you had multi-device enabled and a backup passcode set. This option might not be available to you if you follow the recommendation to keep multi-device disabled except for when you are setting up a new device.
    * The **[recover flow](https://authy.com/phones/reset/?proceed=true)** takes 24 hours and may require identification -- [monitor your email](https://support.authy.com/hc/en-us/articles/115012672088-Restoring-Authy-Access-on-a-New-Lost-or-Inaccessible-Phone).
3. If you cannot do either of the above, you have to contact each service for which you had 2FA configured, prove your identity, and regain access to your accounts one-by-one.

Make sure you clearly understand the above.

With Symantec VIP Access, you cannot automatically recover your codes. You will have to reinstall the Symantec app on your new phone and then contact the service to update your Credential ID.

As for setting your phone number up on a new phone, the carrier should require you to provide a passcode before your phone number is ported to the new device. (Notify your family plan manager if that’s not you.)

### Recovery scenario: what if my phone number is sim swapped?

Recognize when this may have happened to you, ie your phone loses cell signal even though you are in an area with good coverage and others around you still have cell signal. ASAP, contact your cell carrier and your family plan manager. Without your phone number, you will need to get in touch via website or another phone.

### Recovery scenario: what if my password manager is hacked?

[LastPass](https://www.lastpass.com/) and [1Password](https://1password.com/) have many safeguards to protect your passwords such that even if they were hacked, your passwords would not be compromised. Even employees cannot view your stored passwords.

If a hacker obtains your master password, your accounts with 2FA are still protected. If you still have access, change your master password immediately. If the hacker has already changed your master password, contact support and tell them your account has been taken over.

Make sure your master password is damn strong. Not guessable or comprised of real words. Do not lose this, or you lose your entire password vault. In that case, you would have to start over with an empty password vault and you would have to go to each site to reset your passwords one-by-one.

### Q: What if my financial account is hacked?

* A hacker can *definitely* make trades and view your transactions and statements.
* A hacker can *probably* transfer out a few thousand USD by ACH transaction.
* A hacker can *maybe* make a large wire transfer. In the worst case, a hacker drains your account despite additional security measures like picking up on your sim-swapped phone number and correctly responding to verification questions.
* A hacker learns your net worth, address, contact info, and beneficiaries. You could be extorted under threat of violence.

Banks and brokerages guarantee against losses due to fraud, but let’s not test how that all works ([story](https://www.newsbtc.com/tech/silicon-valley-execs-targeted-in-sim-swap-hacking-1-million-in-crypto-stolen/) and [lawsuit](https://www.cnn.com/2020/03/13/tech/sim-hack-million-dollars/index.html)).

### Q: Should I use unique login names?

Many sites require your email address be the login name. Schwab and Fidelity allow you to choose your login name. When possible, use a unique login name that you do not use anywhere else.

### Q: Should I use voiceprint to safeguard financial accounts?

It probably does not hurt, but do not rely on the voiceprint as your only second factor. Voice biometrics are a new front in the deepfake battle. Anyone with a recording of your voice can synthetically imitate your voice. I expect financial firms that use voice biometrics to err on the side of accepting the caller’s voice to avoid telling customers, “you don’t sound like you.” Do not allow voiceprints to lull you into a false sense of security.

### Q: Should I use an private email only for financial accounts?

Probably. From a great [reddit post](https://www.reddit.com/r/fatFIRE/comments/f6kqnj/a_fat_guide_to_cybersecurity/):

> “Use two emails, one which you use publicly and the other privately. Use the public one for whatever: social media accounts, receiving forwarded articles from your crazy grandpa, applying to jobs, etc. The private one should be used only for your financial accounts, such as banks, brokerages, and credit cards. You can also use this email for Lastpass. You should never provide this email to anyone, ever. This will make it very hard for someone, even someone who knows you, to guess what email you use for your finances. Ideally, you’d be using a separate computer, like a $200 chromebook, as the only computer/phone from which you access this email or financial accounts, but that’s pretty paranoid and not necessary. Both of these Gmail accounts should use unique, strong passwords you have memorized, and not be stored in a password manager, just in case.”

### Q: What is the most secure computing environment?

Probably a [Chromebook](https://www.nytimes.com/wirecutter/reviews/best-chromebook/). Each app/webpage is sandboxed. If malware is installed, the "Verified Boot" startup process will reset its OS. Chromebooks probably offer the best balance of security and ease of use.

To secure a cloud instance, there is actually a [long checklist of steps](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/best-practice-checklist/#Security) to take for security, the kind of things that IT professionals do for their corporate networks. A hacker who can successfully access your cloud instance could also gain root access.

### Q: Are security questions bad?

Yes, they suck. The following are not secrets: your mother’s maiden name, the street you grew up on, your best friend from childhood, etc.

If a website requires you to set security questions, only provide the most esoteric answers or fake answers and store them as records in your password manager.

### Personal security audit checklist

Enable 2FA (TOTP if possible) and remove phone number as 2FA method at...
1. email address (ie [Google account](https://account.google.com/))
2. banks and brokerage accounts
3. services with debit access to your financial accounts (PayPal, Venmo, Square, Coinbase, Gusto)
4. phone service -- set a passcode
5. document stores (Dropbox, Docusign, Turbotax)
6. any other service with possible debit access (internet, utilities, water, garbage)
7. ecommerce (Amazon, Uber) and social networks (Github, LinkedIn, Twitter, fb)
8. Remove your phone/email/birthdate from your LinkedIn/Github/seekingalpha profiles.
9. Use credit cards instead of debit where possible. You have more privileges when disputing a fraudulent credit charge than debit.

You likely have many passwords, so it is important to prioritize.

As of Jan 2021, unfortunately it is the case that...
* apple.com (retail site), BofA, Box, Chase, Square, Venmo, Wells Fargo only offer SMS-based 2FA.
* Amazon requires your phone number as one 2FA method.

### Security preschool

Let’s assume you already do the following...
* Protect your home wi-fi network with a password (that is only used for your wi-fi network).
* Avoid saying your name and contact information loudly in public (in cafes or grocery stores).
* Avoid discussing investing or money in public. Use pseudonyms on seekingalpha, reddit, etc.
* Recognize **phishing emails**. Do not click on these emails. The emails often look real and the links often lead to fraudulent websites that look very much like the website they are spoofing.
* Do not respond to personal questions when someone calls you and tells you they work at your bank, phone company, or IRS. If you receive such a call, get their contact info to verify that it matches the public number for that bank/etc or web domain (ie ends in “@mybank.com”), and *hang up the call*. Then, either get back in touch or report the **phone phishing** attempt.

### Conclusion

Once you have implemented this document, reach out to someone close in your life and help them protect themselves.
