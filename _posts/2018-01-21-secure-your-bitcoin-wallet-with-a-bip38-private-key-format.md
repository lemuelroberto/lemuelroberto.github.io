---
layout: post
title: "Secure your Bitcoin wallet with a BIP38 private key format"
date: "2018-01-21 21:00:00 -0200"
author: "Lemuel Roberto"
meta: "bitcoin cryptocurrency bip38"
---

## Problem to solve

Store a paper wallet without expose the actual private key.

## Chosen solution: encrypt private key using BIP38 wallet format

We have the standart [Wallet Import Format (WIP)](https://bitcoin.org/en/glossary/wallet-import-format) to store private keys, but the [BIP38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki) format offers a standart method for encrypting and encoding a passphrase-protected Bitcoin private key.

The BIP38 will encrypt your Bitcoin private key using [AES256](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard).

## How-to

1. [download](https://github.com/pointbiz/bitaddress.org/archive/master.zip) the [Bitaddress](https://github.com/pointbiz/bitaddress.org) project
2. unzip the project and open the bitaddress.org.html file in your browser

### Generate a new Bitcoin BIP38 wallet

1. go the the "Paper Wallet" tab
2. check the "BIP38 Encrypt" checkbox
3. enter a long, hard to gess and easy to remember passphare
4. click the "Generate" button

![A "Paper Wallet" tab screenshot of the Bitaddress web application showing how to generate a new Bitcoin BIP38 private key][generate]

### Encrypt a Bitcoing private key you alread have using BIP38 format

1. go the the "Wallet Details" tab
2. enter your decrypted private key (WIF, WIFC, HEX, B64, B6, MINI)
2. check the "BIP38 Encrypt" checkbox
3. enter a long, hard to gess and easy to remember passphare
4. click the "Encrypt BIP38" button

![A "Wallet Details" tab screenshot of the Bitaddress web application showing how to encrypta a Bitcoin private key you alread have using the BIP38 format][encrypt]
![An example of a BIP38 Bitcoin encrypted private key][encrypted]

**WARNING:**
- do not share your private keys
- do not send Bitcoin to the example wallet here
- validate (on "Wallet Details" tab) your BIP38 private key before send funds to it
- always use a secure passphare and if possible a [password manager](https://en.wikipedia.org/wiki/Password_manager)

[generate]: https://lemuelroberto.github.io/images/2018-01-21-secure-bitcoin-wallet-generate.png "Generate a new Bitcoin BIP38 wallet"
[encrypt]: https://lemuelroberto.github.io/images/2018-01-21-secure-bitcoin-wallet-encrypt.png "Encrypt a Bitcoing private key you alread have using BIP38 format"
[encrypted]: https://lemuelroberto.github.io/images/2018-01-21-secure-bitcoin-wallet-encrypted.png "An encrypted Bitcoin BIP38 private key example"
