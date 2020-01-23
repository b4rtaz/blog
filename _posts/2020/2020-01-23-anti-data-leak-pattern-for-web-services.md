---
layout: post
title: "Anti-Data-Leak Pattern for Web Services"
author: "b4rtaz"
image: "images/2020/anti-data-leak-pattern.png"
tags: programming idea
---

From one year to another, data leaks from cloud services are more frequent. Unfortunately, the recent data leak was more dangerous than a few years ago because people keep more sensitive data in the cloud. There are many methods to prevent data theft like a professional administration team, a complex network architecture, intelligent firewalls, etc. Generally, that method is expensive and challenging to implement. Especially for a small business. If we look at the success of securing data by blockchain, we can note that current cloud architectures aren’t designed for reliable security.

Current cloud services look similar; each has a database, which stores every sensitive data in plain text, credit card numbers, PIN codes, or personal ID numbers. To get all of this information, hackers must gain access to the database. Of course, this isn’t easy, but if they achieve it, they have every information that people sent to the service. The next significant weakness of this architecture is that many people can access the infrastructure. Developers, network administrators, back-up team, or cleaning staff, have access to the server room. That gives thousands of attack vectors.

With the help of asymmetric cryptography, we can alter many attack vectors, and make the theft of database resistant to data leak.

## End-To-End Encryption 

<img src="{{ site.baseurl }}images/2020/anti-data-leak-pattern-end-to-end-encryption.png" width="800" height="400" alt="End-To-End Encryption" />

If we stopped trusting the infrastructure and the server security, we would assume that a successful attack on our infrastructure would happen, the attacker would get access to the whole server, including every database. The conclusion of that is unfortunate, we should start to regard our infrastructure as potentially faulty and dangerous. We shouldn’t store sensitive data on our server, in a case where anybody who has access to the machine could read them. We can solve this problem by using end-to-end encryption.

<img src="{{ site.baseurl }}images/2020/anti-data-leak-pattern-encryption.png" width="800" height="400" alt="Encryption/Decryption by Derived Key" />

The plain text data are needed only in a few places, e.g., on a user’s computer, an administrator’s computer, the e-mail sending service, the credit card charging service, etc. In any other place, this data should be unavailable. The solution is as follows; we should separate our dangerous infrastructure from the clients. Every client receives its own, asymmetric encryption key, and encrypts every sensitive data before sending them to the server. That data should only be encrypted for sides who should have access to them. To encrypt the data we have to obtain an encryption key. For that there are many algorithms like RSA, but today recommended is using elliptic-curve cryptography like ECDH. ECDH allows us to create a cipher key from the private key of one side and the public key of the opposite side. By this method we can create a different key for every side, and independently encrypt the sensitive data for each side. For example, the user of the auction portal should encrypt sensitive personal data, e.g., e-mail for moderator and administrator. In this case three sides can read e-mails stored in the database.

<img src="{{ site.baseurl }}images/2020/anti-data-leak-pattern-table.png" width="800" height="400" alt="Anti-Data-Leak Database Table" />

There is a wide range of possibilities to make an access data relation. We can create a one-to-one relation or one-to-many relation. Every side can read, and override the opposite side data. Of course, we can limit these possibilities by the application logic. It is worth mentioning that, we can create different relations for different kinds of data. For example, the previously mentioned user of auction portal could encrypt the e-mail for moderator and administrator access, but a credit card can only be encrypted for administrator access.

## Architecture Separation

<img src="{{ site.baseurl }}images/2020/anti-data-leak-pattern-infrastructure.png" width="800" height="400" alt="Infrastructure Separation" />

We need to change the way of thinking for services, like the e-mail sending service or the credit card charging service. This kind of service should be treated as an external client. It’s critical to keep this service outside of our main infrastructure. Why? Because that kind of service must have a private key to decrypt the sensitive data. So this key cannot be available on the server, wherein, we have the database, because a hacker could find it and decrypt the sensitive data. We should keep these services far away from our main infrastructure. For example, if we use a cloud for our backend, our credit card charging service should be installed in another hosting provider. If we have our infrastructure, we should create a server in a separate network (e.g., without internet access) for that kind service. 

## Security of Private Key

<img src="{{ site.baseurl }}images/2020/anti-data-leak-pattern-private-key.png" width="800" height="400" alt="Private Key Encryption" />

This problem applies to all clients. We can’t store any private key in our main infrastructure, because in case of attack, a hacker could easily decrypt sensitive data. To prevent this, we can use a few methods. The simplest is to keep the private key on the client-side (e.g., system certificates store, the hardware security key). This method can work for the administrator or company workers. However, for ordinary users, this sounds unrealistic. The solution comes with cryptography. Every user has a password, so we can encrypt the private key by user password and store this in our server. It is crucial to encrypt and decrypt the private key only on the client-side.

But what happened if the user forgets the password? We should create a new asymmetric key for the user, generate a random password, and regenerate the user part of the encrypted data by a new key. Of course, we cannot do this on the server-side. This can do only client with access to user data like the administrator client. The procedure is similar to changing a password function.

## Asynchronous Data Validation

It must be noted, in that architecture, we cannot validate any encrypted data by the server application. What can we do with this? Of course, we can verify forms in the client application, but this is not enough. We can implement a more sophisticated validation flow. I mean, we can validate the date when we want to use them. For example, the credit card charging service, before charging, tries to validate decrypted data. If that data would be incorrect, the service should mark the row in the database as incorrect.

## Example Project

To comprehend a small example for Anti-Data-Leak Pattern, I’ve made a working example project. The example project is a web page, wherein a user can create an account, enter credit card information. Only an administrator can have access to all credit card data. The project is available on GitHub. The project contains two clients; the Angular client is for a user; a simple console client is for the administrator. The server application is made in the Slim Framework (PHP). I tried to write the code as simples I could because I think this is the best way to analyze the concluded logic. The project uses recent cryptography algorithms like ECDH or Argon2.

&#9658; [Anti-Data-Leak Pattern Example](https://github.com/b4rtaz/anti-data-leak-pattern-example) on GitHub

***

Icons: [streamline](https://www.webalys.com/), [outline style](https://www.iconfinder.com/ZFros)
