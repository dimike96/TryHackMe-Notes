# THM - Cryptography for Dummies

[TryHackMe | Cryptography for Dummies](https://tryhackme.com/room/cryptographyfordummies)

> Michael Jack | 06/2022https://tryhackme.com/room/cryptographyfordummies

---

## Task 1 - Intro

> Without encryption communications over the internet will be very insecure, and it would be very easy for someone to see your data. 
> Fortunately this isn't true, and almost all of the data you get/send over the internet is encrypted and cannot be seen in plain text by someone who got access to it.

---

## Task 2 - Types of Cryptography

There are two different categories of cryptography. **Symmetric** and **Asymmetric**.

This rerers to how in symmetric cryptography the keys used to encrypt and decrypt are the same, hence the process is *symmetric*.

In asymmetric cryptography the keys used for encoding and decoding are different. The encryption key is typically called the *Public* key and the decryption key the *Private* key.

An example of asymmetric cryptography:

> Alice wants to talk to Google
> Google gives Alice the Public key.
> Alice encrypts her message with the public key and sends it to Google.
> Google decrypts the message with his private key and sends back what Alice wanted.  
> And that's how the conversation goes...

### Questions

> What type of cryptography is more secure?

```
asymmetric
```

> What type of cryptography is faster?

```
symmetric
```

> What type of cryptography will a Bank site use?

```
asymmetric
```

> What will you use to encrypt your messages in asymmetric cryptography?

```
public key
```

> What will you use to decrypt messages in asymmetric cryptography?

```
private key
```

> Does symmetric cryptography use two different keys for encryption/decryption? (aye/nay)

```
nay
```

---

## Task 3 - What is a hash?

A **hash** is the result of a **hashing algorithm**. These are special because they are one-way operations that cannot be reversed to get what the input was. 

Common hashing algorithms are **MD5** (Message Digest 5), and **SHA** (Secure Hashing Algorithm). *Note: There are different versions of SHA such as SHA256 and SHA512

**To get md5 hash of string in terminal use:**  ```echo -n "string" | md5sum``` 

### Questions

> What's the MD5 hash of "hashes are cool"?

```
f762d32e3c160900d94b683e927555b9
```

> What does MD5 stand for?

```
Message Digest 5
```

> Who created MD5?

```
Ronald Rivest
```

---

## Task 4 - Decoding/Encoding

> There's difference between encoding and encrypting. Let's say you have an encrypted file, the only way to decrypt it is using key. 
> While encoded data can be decoded immediately, without keys. It's **NOT** a form of encryption, it just a way of representing data.

### Questions

> Encode the string "cryptographyisuseful" with Base64

```
Y3J5cHRvZ3JhcGh5aXN1c2VmdWwK
```

> Decode the string dGhlIHNlY3JldCB3b3JkIGlzIDogd2F0ZXJtZWxvbg== . What is the secret word?

```
the secret word is : watermelon
```

---

