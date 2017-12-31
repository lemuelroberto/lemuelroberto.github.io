---
layout: post
title: "Using GnuPG to encrypt your files"
date: "2017-12-31 19:00:00 -0300"
author: "Lemuel Roberto"
meta: "security cryptography GnuPG Open PGP privacy"
---

> A straight to the point guide to encrypt and secure your files using GnuPG.

## Problem to solve

You want to encrypt some files using a secure and simple to use tool.

## Chosen solution: GNU Privacy Guard

[GNU Privacy Guard (GnuPG)](https://www.gnupg.org) is a 20 years old tool for encrypt and sign your data and communications.

There are two approaches for encrypting information: [symmetric encryption](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) and [asymmetric encryption](https://en.wikipedia.org/wiki/Public-key_cryptography).

If you need to cipher some files without sharing your private key you can use faster and yet secure symetrical algorithms to encrypt your data.

If you need to exchange encrypted information without exchanging keys, you should use asymmetric encryption.

## Examples of use

See the gpg [man](https://linux.die.net/man/1/gpg) page for details.

### Encrypt file using AES256 algorithm

`gpg --symmetric --cipher-algo AES256 file.txt`

### Decrypt a file and save content into another file

`gpg --output decrypted-file.txt --decrypt file.txt.gpg`

### Encrypt with digest algorithm to mangle the passphrase

`gpg --symmetric --s2k-cipher-algo AES256 --s2k-digest-algo SHA512 --s2k-mode 3 --s2k-count 65011712 file.txt`

### Decrypt a file and open content with VIM

`gpg --decrypt file.txt.gpg | vim -`

**Warning from documentation:** In general, you do not want to use this option as it allows you to violate the OpenPGP standard.

### Compliance option

`gpg --openpgp ... file.txt`

**From documentation:** Reset all packet, cipher and digest options to strict OpenPGP behavior. Use this option to reset all previous options like `--s2k-*`, `--cipher-algo`,  `--digest-algo`  and  `--compress-algo`  to OpenPGP compliant values. All PGP workarounds are disabled.

## Configuring GnuPG application

GnuPG stores configuration files in the home directory (default `~/.gnupg`). You can change the default directory by setting the environment variable `$GNUPGHOME` or using the `--homedir` option.

> gpg.conf

```
# Encrypt with digest algorithm to mangle the passphrase.
s2k-cipher-algo AES256
s2k-digest-algo SHA512
s2k-mode 3
s2k-count 65011712
```

With this settings `gpg -c file.txt` is equivalent to `gpg --symmetric --s2k-cipher-algo AES256 --s2k-digest-algo SHA512 --s2k-mode 3 --s2k-count 65011712`.

> gpg-agent.conf

```
# Set the maximum time a cache entry is valid to 0 seconds.
# In other words, make sure we're always asked to type our passphrase when decrypting.
max-cache-ttl 0
```

> bash_profile

```
# Set environment variable $GNUPGHOME
export GNUPGHOME=$MY_CONFIGS/gnupg
```

**Note:** set `$GNUPGHOME` folder permissions to 700 and files to 600 to avoid GnuPG warnings.
