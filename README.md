# Stellar Rust Fundamentals with Rustfinity <!-- omit in toc -->

## Get Started
Learn Rust fundamentals with Stellar and Rustfinity with Devcontainers. 

<div style="text-align: center;" align="center">
<strong>Devcontainers</strong>
</div><br/>

<div align="center">
<a href="https://github.com/codespaces/new?repo=anataliocs/stellar-rustfinity-rust-fundamentals&editor=web">
  <img src="https://github.com/codespaces/badge.svg" alt="Open in Codespaces">
</a>
</div>
<div align="center">
<a href="https://app.codeanywhere.com/#https://github.com/anataliocs/stellar-rustfinity-rust-fundamentals">
  <img src="https://codeanywhere.com/img/open-in-codeanywhere-btn.svg" alt="Open in Codeanywhere">
</a>
</div>

**Learn more about how Devcontainers are used in this repo:**
- Running [Devcontainers Locally](./devcontainer.md)
- Check out the [Devcontainer config](./.devcontainer/devcontainer.json)

## Installation
Stellar smart contracts are written in the [Rust](https://www.rust-lang.org/) programming language and can be deployed to the testnet or mainnet. 

### Prerequisites
To build and develop contracts you need only a couple prerequisites:

- A [Rust](https://www.rust-lang.org/) toolchain
- An editor that supports Rust
- [Stellar CLI](https://developers.stellar.org/docs/build/smart-contracts/getting-started/setup#install-the-stellar-cli)

See the [documentation](https://developers.stellar.org/docs/build/smart-contracts/getting-started/setup) for more prerequisites installation instructions. 

#### Create Identity
If an identity for signing transactions has already been created, this part can be skipped. 

When deploying a smart contract to a network, an identity that will be used to sign the transactions must be specified. Let's configure an identity called alice. Any name can be used, but it might be convenient to have some named identities for testing, such as alice, bob, and carol. Notice that the account will be funded using [Friendbot](https://developers.stellar.org/docs/learn/fundamentals/networks#friendbot). 

```
stellar keys generate --global alice --network testnet --fund
```

Get the public key of alice with this command: 

```
stellar keys address alice
```

See the [documentation](https://developers.stellar.org/docs/build/smart-contracts/getting-started/setup#configure-an-identity) for more information about identities.

### Clone Contracts
The example smart contracts don’t need installation, simply clone the repo:

```
git clone https://github.com/stellar/soroban-examples
```

*Note all smart contract examples are cloned, not individual contracts.*

### Run Smart Contracts
*Note: The `increment` contract is used in these instructions, but the instructions are similar for the other contracts, except for how to invoke the contracts.*

The smart contracts can easily be run by deploying them to testnet. Choose a contract and follow these instructions. 

#### Build
First the smart contract must be built with this command from the `increment` contract’s root folder:

```
cd increment
stellar contract build
```

A `.wasm` file will be outputted in the target directory, at `target/wasm32-unknown-unknown/release/soroban_increment_contract.wasm`. The `.wasm` file is the built contract.

#### Deploy
The WASM file can now be deployed to the testnet by running this command:

```
stellar contract deploy \
  --wasm target/wasm32-unknown-unknown/release/soroban_increment_contract.wasm \
  --source alice \
  --network testnet \
  --alias increment_contract
```

When the smart contract has been successfully deployed, the command will return the contract’s ID (e.g. CACDYF3CYMJEJTIVFESQYZTN67GO2R5D5IUABTCUG3HXQSRXCSOROBAN). This ID can be used to invoke the contract, but since an alias is added, the alias can be used for invoking the contract as well.

#### Invoke
Now the contract is on testnet, it can be invoked. For the increment contract there’s only one function to invoke, and that’s the increment() function. Look at the code for the other contracts to see which function to invoke as every example contract is different.

Run this command to invoke the increment contract (the added alias is used as the contract ID):

```
stellar contract invoke \
  --id increment_contract \
  --source alice \
  --network testnet \
  -- \
  increment 
```

The contract will return 1 the first time it’s run, run it again and see the returned value is being incremented.

## Licence
The example smart contracts are licensed under the Apache 2.0 license. See the LICENSE file for details.

## Contributions
Contributions are welcome, please create a pull request with the following information: 

- Explain the changes/additions you made
- Why are these changes/additions needed or relevant?
- How did you solve the problem, or created the suggested feature?
- Have your changes/additions been thoroughly tested?

## Relevant Links:
- [Smart Contract Documentation](https://developers.stellar.org/docs/build)
- [Getting Started Guide](https://developers.stellar.org/docs/build/smart-contracts/getting-started)
- [Example descriptions in the documentation](https://developers.stellar.org/docs/build/smart-contracts/example-contracts)
- [Stellar Developers Discord server](https://discord.gg/stellardev)

