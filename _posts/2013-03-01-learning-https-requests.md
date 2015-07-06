---
layout: post
title: Learning like a 5yo about https requests
---

Because we value the security of our customers’ and celebrities’ data, we decided early on that both outbound and inbound requests would be served over SSL.

To configure SSL for a site, your DNS and web hosting vendors likely have clear instructions to follow. As for connecting to third-party services via HTTPS, I often felt incredulous that I didn’t come across any good and comprehensive guides online when I was figuring this stuff out, which is a bit weird since this must be a common task for many online companies. Like much of my recently acquired tech ops knowledge, I feel like each nugget of learning was hard-won, and I wish to share what I know here.

To make requests via HTTPS, your app needs a <strong>truststore</strong> that contains <strong>certificates</strong> from the parties that you expect to communicate with or from Certificate Authorities that you trust to identify other parties. There is also another concept called a keystore that contains private keys supposedly for implementing server-side SSL. Now, already things can get confusing. I got those definitions from [this stackoverflow discussion that says that truststore and keystore are different concepts](http://stackoverflow.com/questions/318441/truststore-and-keystore-definitions), and yet it really seems that truststore and keystore are used interchangeably. I’ve come to the conclusion to not allow this ambiguity to ruin my life.

## Download certificates

The first step is to download certificates from the sites and services with which your server will communicate via HTTPS. For example, visit [https://api.stripe.com](https://api.stripe.com) using Chrome, click the lock icon in the browser bar, and look for “Certificate Information.” You should see a certificate tree that looks something like:

<img src="/assets/certificate-tree-example.jpg"/> 

Each of those is a certificate with its own expiration date. Root-level certificates usually have expiration dates farthest in the future, whereas leaf certificates expire more frequently.

I recommend downloading all of the available certificates so that they can be imported into the keystore. You don’t want to have your app’s communication with crucial services broken without warning because a leaf certificate expired or was replaced. Ahem, yes, I learned that by experience.

## Import certificates into truststore

In a Scala/Java environment, the javax.net.ssl.trustStore system property will need to point to a keystore that includes the certificates of trusted third-party sites. (See? Very interchangeable.)

To prepare the truststore, you can run a command that looks like:
> keytool -import -alias stripe.com -file api.stripe.com.cer -keystore keystore

Do this on each certificate you want to import. There are plenty of [resources out there on keytool commands](http://www.sslshopper.com/article-most-common-java-keytool-keystore-commands.html).

Then fire up your app and you should be to communicate securely with APIs all over the interwebs!
