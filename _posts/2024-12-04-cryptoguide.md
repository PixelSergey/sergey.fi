---
layout: post
category: [cyber]
title: "A tinfoil hat guide to cryptography [incomplete]"
author: PixelSergey
permalink: /crypto/
---

I think that the people who obsess over cryptography, privacy, and opsec are _cool_.
There really is no end to the number of techniques you can use,
with each one adding a new layer of [tinfoil hat](https://en.wikipedia.org/wiki/Tin_foil_hat) around your head.
This post is intended to be a guide for those who want to try this for themselves:
I'll keep adding sections here as I find out what kind of things are possible to do in the opsec world.

Please please please [contact me](https://sergey.fi/about/) if you have any good ideas that I've missed here!

# Table of contents

Here are the topics I want to cover for now:
- Generating a PGP key
- Signing Git commits with PGP
- Encrypting email with PGP
- Adding yourself to the web of trust
- Generating cryptocurrency wallets

Note: all the instructions here are for Debian-based Linux distros (e.g. Ubuntu) and NixOS.
In my opinion, everyone should use NixOS, but that's just me :D
If you're on Windows or Mac... good luck, I guess. 

# Topics

## Generating a PGP key

The basis of all good opsec is a way to encrypt, decrypt, sign, and verify data.
This is where a PGP key comes in!

#### Step 1: Install GnuPG

- On Debian/Ubuntu: run `sudo apt install gnupg`
- On NixOS: add `pkgs.gnupg` to your configuration

#### Step 2: Generate the key

1. Run `gpg --full-gen-key`
1. Pick either `RSA and RSA` or `ECC (sign and encrypt)`
  - `ECC` is now the preferred method
  - If you pick `ECC`, select the option `Curve 25519`
  - If you pick `RSA`, select a keysize of `4096` 
1. Make the key expire after a number of years
  - 5 years is good
  - This doesn't mean you lose your key after 5 years: you can always renew it
  - An expiry date is recommended since it will prevent misuse and confusion if you accidentally lose your keys
1. Enter your details
  - The name must be your REAL name if you want to be added to the web of trust later on
  - The email should be your primary email, you can add others later on
  - The comment is just a nickname or a username you use everywhere (optional)
