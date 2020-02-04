# HD Wallets Plugin

## Introduction

The plugin allows to derive child key (xprv, xpub) from a master key in a deterministic way, and/or sign transaction hashes for UTXO and ethereum type crypto coin.

## Use cases

The plugin can be used to

- Derive child key for UTXO
- Derive child key for ethereum
- Sign transaction for UTXO
- Sign transaction for ethereum

## Setup

- Generate HD-Wallets master key manually
**Example Master Key:** `xprv9s21ZrQH143K31xYSDQpPDxsXRTUcvj2iNHm5NUtrGiGG5e2DtALGdso3pGz6ssrdK4PFmM8NSpSBHNqPqm55Qn3LqFtT2emdEXVYsCzC2U` 
- Importe master key in SDKMS as secret raw key

## Input/Output JSON object format

**Input**

```
{
    "master_key_id": "<Master-Key-UUID>",
    "path": "<Child-Key-Path>"  ,
    "msg_hash": "<32-Byte-Message-Hash>",
    "coin": "<Coin-Type>"
}
```

**Output**

```
 "xprv": "<HD-Wallet-Private-Key>",
 "xpub": "<HD-Wallet-Public-Key>",
 "coin_signature": "<Bitcoin-canonicalized-ECDSA-signature>",
 "signature": "<ECDSA signature>"
```

* `master_key_id`: UUID of master key imported in SDKMS
* `path`: Path of key to be derived to sign e.g: m/0, m/1, m/2/10 etc
* `msg_hash`: 32 byte SHA-3 message hash
* `coin`: coin type utxo or eth
* `xprv`: BIP0032 private key
* `xpub`: BIP0032 public key
* `coin_signature`: Bitcoin canonicalized ECDSA signature
* `signature`: ECDSA signature

## Example Input/Output JSON object

**Input JSON object**

```
{
   "master_key_id": "0eae8ff0-553e-4f47-bb64-7c87f34bf5e5",
   "coin": "utxo",
   "path": "m/2",
   "msg_hash": "45a0ee821b05400f513891bbb567a99139f3df72e9e1d4b48186841cc5996d2f"
}
```

**Output JSON object**

```
{
  "xprv": "xprv9uZghWCSYwDho7us3q1WLBjVYx2xzVJNT8qNo4P9i8wa3tQJYbffzztTF6wXjuorG49NXahqraWsrVUmy3uTJLkvSYXyDLnHHU1GJibUk2t",
  "xpub": "xpub68Z371jLPJn11bzL9rYWhKgE6ysTPx2DpMkybSnmGUUYvgjT68yvYoCw6PP8Vo7YoZRC6iqrfpixEUG694KgHPYYnydGuEYDwjESStYxYxe",
  "signature": "3045022100af9bf94c4959328b56861ca5f175b5e59014cb5bd2a5fcee2e95b1563dbc652e0220411ff01751af64d6b7209908fc58f527b07a0a9258eee7be7aa5704136954b02",
  "coin_signature": "af9bf94c4959328b56861ca5f175b5e59014cb5bd2a5fcee2e95b1563dbc652e411ff01751af64d6b7209908fc58f527b07a0a9258eee7be7aa5704136954b02"
}
```

## References

- [bip-0032](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)

