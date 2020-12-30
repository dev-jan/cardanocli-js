# CardanoJs

## Overview

This is a library, which wraps the cardano-cli with JavaScript and makes it possible to interact with the cli-commands much faster and more efficient.

###### This library is brought to you by <b><a href="http://pipool.online/">Berry Pool</a></b>. You can support our work by delegating to our pool.

## Prerequisites

- `cardano-node 1.24.2`
- `node.js >= 12.19.0`

## Install

#### NPM

```bash
npm install cardanojs
```

#### From source

```bash
git clone https://github.com/Berry-Pool/CardanoJs
cd CardanoJs
npm install
```

## Getting started

```javascript
const CardanoJs = require("cardanojs");
const shelleyGenesisPath = "/home/ada/mainnet-shelley-genensis.json";

const cardanoJs = new CardanoJs({ era: "allegra", shelleyGenesisPath });

const createWallet = (accout) => {
  cardanoJs.addressKeyGen(accout);
  cardanoJs.stakeAddressKeyGen(accout);
  cardanoJs.stakeAddressBuild(accout);
  cardanoJs.addressBuild(accout);
  return cardanoJs.wallet(accout);
};

const createPool = (name) => {
  cardanoJs.nodeKeyGenKES(name);
  cardanoJs.nodeKeyGen(name);
  cardanoJs.nodeIssueOpCert(name);
  cardanoJs.nodeKeyGenVRF(name);
  return cardanoJs.pool(name);
};

const wallet = createWallet("Ada");
const pool = createPool("Berry");

console.log(wallet.paymentAddr);
console.log(pool.file("vrf.vkey"));
```

Check /examples for more use cases.

## API

- <a href="./API.md">API Documentation</a>

## Structure

All files will be stored and used in the directory you choose when instantiating CardanoJs (<code>dir</code>).
The directory is split in two subfolders <code>tmp</code> and <code>priv</code>.
In the <code>tmp</code> folder are stored protocol paramters, raw transactions, signed transactions and witnesses with unique identifiers.
The <code>priv</code> folder is again divided into two subolders holding on one site the pools <code>pool</code> and on the other side the wallets <code>wallet</code> (like <a href="https://cardano-community.github.io/guild-operators/#/">CNTools</a> structure).

Example structure:

```
dir
    tmp
        <tx_1.raw>
        ...
    priv
        pool
            Berry
                <Berry.node.vkey>
                <Berry.node.skey>
                <Berry.vrf.vkey>
                ...
        wallet
            Lovelace
                <Lovelace.payment.vkey>
                <Lovelace.stake.skey>
                ...
```
