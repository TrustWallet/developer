# Wallet Operations Guide

We present here an overview of the basic wallet operations.  More detailed, language-specific samples are provided in step-by-step [guides](wallet-core/integration-guide.md).

The covered basic operations are:

* Wallet management
  * Creating a new multi-coin wallet
  * Importing a multi-coin wallet
* Address derivation (receiving)
  * Generating the default address for a coin
  * Generating an address using a custom derivation path (expert)
* Transaction signing (sending)
  * Coin-specific transaction signing
  * Coin-independent method ('AnySigner')

For the examples we use *Bitcoin*, *Ethereum* and *Binance Coin* as sample coins/blockchains.

Note: Wallet Core does not cover communication with blockchain networks (nodes): 
address derivation is covered, but address balance retrieval not; 
transaction signing is convered, but broadcasting transactions to the network not.

## Wallet Management

### Multi-Coin Wallet

The Multi-Coin Wallet is a structure allowing accounts for many coins, all controlled by a single recovery phrase.  It is a standard HD Wallet (Hierarchically Derived), employing the standard derivation schemes, interoperable with many other wallets (BIP39, BIP44).

### Creating a New Multi-Coin Wallet

When a new wallet is created, a new seed (and thus recovery phrase) is chosen at random.  
*After creation, the user has to be informed and guided to backup the recovery phrase.*

The random generation employs secure random generation, as available on the device.

```swift
let wallet = HDWallet(strength: 128, passphrase: "")
```

Input parameter | Description
---|---
*strength* | The strength of the secret seed.  Higher seed means more information content, longer recovery phrase.  Default value is **128**, but 256 is also possible.
*passphrase* | Optional passphrase, used to encrypt the seed.  If specified, the wallet can be imported and opened only with the passphrase (Not to be confused with recovery phrase).

### Importing a Multi-Coin Wallet

A previously created wallet can be imported using the recovery phrase.  Typical usecases for import are:
* re-importing a wallet later, into a later installation, or
* importing into another device, or 
* importing into another wallet app.

If the wallet was created with a passphrase, it is also required.

```swift
let wallet = HDWallet(mnemonic: "ripple scissors kick mammal hire column oak again sun offer wealth tomorrow wagon turn fatal", passphrase: "")
```

Input parameter | Description
---|---
*mnemonic* | a.k.a. *recovery phrase*.  The string of several words that was used to create the wallet.
*passphrase* | Optional passphrase, used to encrypt the seed.

## Account Address Derivation

Each coin needs a different account, with matching address.  Addresses are derived from the multi-coin wallet.
Derivation is based on a *derivation path*, which is unique for each coin, but can have other parameters as well.
Each coin has a default derivation path, such as `"m/84'/0'/0'/0/0"` for Bitcoin and `"m/44'/60'/0'/0/0"` for Ethereum.

### Generating the Default Address for a Coin

The simplest is to get the default address for a coin -- this requires no further inputs.
The address is generated using the default derivation path of the coin.

```swift
let address = wallet.getAddressForCoin(coin: .ethereum)
```

For example, the default BTC address, derived for the wallet with the mnemonic shown above, with the default BTC derivation path (`m/84'/0'/0'/0/0`) is:
`bc1qpsp72plnsqe6e2dvtsetxtww2cz36ztmfxghpd`.
For Ethereum, this is `0xA3Dcd899C0f3832DFDFed9479a9d828c6A4EB2A7`.

### Generating an Address Using a Custom Derivation Path (Expert)

It is also possible to derive addresses using custom derivation paths.
This can be done in two steps: first a derived private key is obtained, then an address from it.

> **Warning**: use this only if you are well aware of the semantics of the derivation path used!

> **Security Warning**: if secrets such as private keys are handled by the wallet, even if for a short time, handle with care!
> Avoid any risk of leakage of secrets!

```swift
let key = wallet.getKey(derivationPath: "m/44'/60’/1’/0/0")
let address = CoinType.ethereum.deriveAddress(privateKey: key)
```

For example, a second Ethereum address can be derived using the custom derivation path `”m/44'/60’/1’/0/0”` (note the 1 in the third position),
yielding address `0x68eF4e5660620976a5968c7d7925753D3Cc40809`.
