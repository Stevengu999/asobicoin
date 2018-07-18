# ASOBI COIN Smart Contract

This repository contains the
[ERC-20](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md) smart
contract code for the ASOBI COIN token based on the Ethereum blockchain.

It also contains everything necessary to

- test basic token functionality,
- flatten the smart contract code to upload and verify on
  [Etherscan](https://etherscan.io/), and
- audit the smart contract code once it has been deployed.

Currently, ASOBI COIN has not been deployed on the main Ethereum network. As
soon as this happens, the ASOBI COIN smart contract address will be added to
this README file.

## Quickstart

```
git clone git@github.com:asobicoin/asobicoin.git
# or
git clone https://github.com/asobicoin/asobicoin.git
cd asobicoin
npm install
npm test
```

The following commands are available:

| Command            | Description |
|--------------------|-------------|
| `npm run compile`  | Compile all smart contracts using truffle |
| `npm run lint-fix` | Try to automatically fix lint issues found by ESlint and Solium |
| `npm run lint`     | Run ESlint and Solium to lint all JavaScript and Solidity code |
| `npm test`         | Run all smart contract tests using truffle |

## About ASOBI COIN

ASOBI COIN is a token that is emitted as part of the [ASOBI
COIN](https://asobimo.io/en/) token sale. There will be up to 16,500,000,000
tokens emitted as part of the sale -- if fully sold out.

| | Value |
|-|-------|
| Decimals | 18 |
| Full Name | ASOBI COIN |
| Symbol | ABX |
| Token Cap | 16,500,000,000 |

## Token Usage Steps

1. Flatten the contract (refer to [this
   section](#flattening-smart-contract-code-for-etherscan) to learn how) and
   copy to clip board.
2. Paste the contract code in [Remix IDE](https://remix.ethereum.org/) and
   deploy it to the main Ethereum Network. Refer to [ETH Gas
   Station](https://ethgasstation.info/) for a recommended Gas price.
3. Document the deployed address in this document.
4. Add the verified source code on Etherscan by using the same contract that
   was deployed using Remix.
5. Audit the contract.
6. Revise the contract if changes are required and go back to step 1.
7. Add all audit results to this repository.
8. Once the token sale is finished: `.mint()` tokens to all token purchasers,
   keeping in mind the correct decimal conversion.
9. Call finishMinting() on token contract.

After that, no more steps shall be necessary and the token can be used
normally.

## Flattening Smart Contract Code for Etherscan

In order to flatten and print `contracts/AsobiCoin.sol`, the following command
can be run:

```bash
npm run flatten
```

You will see the following output:

```
pragma solidity ^0.4.13;

contract ERC20Basic {
  function totalSupply() public view returns (uint256);
  function balanceOf(address who) public view returns (uint256);
  function transfer(address to, uint256 value) public returns (bool);
  event Transfer(address indexed from, address indexed to, uint256 value);
}

// ... here be contracts

contract AsobiCoin is CappedToken {
    string public name = "ASOBI COIN";
    string public symbol = "ABX";
    uint256 public decimals = 18;
    constructor() public CappedToken(300000000 ether) {
    }
}

library SafeMath {

// ... here be SafeMath

}
```

For extra comfort, you can copy the code directly to the X clipboard:

```bash
npm run flatten | xclip -sel clipboard
```

You can then hand the code over to [Etherscan](https://etherscan.io/). You can
upload the code directly when viewing the deployed smart contract on Etherscan
after deployment. You can also upload it using the [Verify Contract
Code](https://etherscan.io/verifyContract) form, provided you know have the
contract address at hand.

## Project Organization

```
.
├── bin
│   └── flatten
├── .circleci
│   ├── config.yml
├── contracts
│   ├── AsobiCoin.sol
│   ├── Escrow.sol
│   └── Migrations.sol
├── .editorconfig
├── .eslintrc.yml
├── .gitignore
├── LICENSE
├── migrations
│   └── 1_initial_migration.js
├── .npmrc
├── package.json
├── package-lock.json
├── README.md
├── soliumignore
├── soliumrc.json
├── test
│   └── AsobiCoin.js
└── truffle.js
```

| File                                | Description                      |
|-------------------------------------|----------------------------------|
| `bin/flatten`                       | Flatten Solidity smart contracts |
| `.circleci`                         | CircleCI configuration files |
| `.circleci/config.yml`              | CircleCI configuration YAML file |
| `contracts/`                        | Contain Solidity smart contracts |
| `contracts/AsobiCoin.sol`           | Contain ASOBI COIN smart contract |
| `contracts/Migrations.sol`          | Contain Truffle Suite migration smart contract |
| `.editorconfig`                     | [EditorConfig](https://editorconfig.org/) file |
| `.eslintrc.yml`                     | [ESLint](https://eslint.org/) configuration |
| `.gitignore`                        | gitignore file |
| `LICENSE`                           | MIT License |
| `migrations/`                       | Contain Truffle Suite smart contract migrations |
| `migrations/1_initial_migration.js` | Initial migration |
| `.npmrc`                            | NPM configuration file |
| `package.json`                      | NPM package file |
| `package-lock.json`                 | NPM package lock file |
| `README.md`                         | README file |
| `.soliumignore`                     | Solium ignore file |
| `.soliumrc.json`                    | Solium configuration file |
| `test/`                             | Solidity smart contract tests run by Truffle Suite |
| `test/AsobiCoin.js`                 | Test ASOBI COIN smart contract |
| `truffle.js`                        | Configuration for Truffle Suite |

## Project Dependencies

To use ASOBI COIN in other projects, only the following dependency is necessary.

| Name                                                                   | Version  |
|------------------------------------------------------------------------|----------|
| [OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-solidity/) | `1.10.0` |

To develop ASOBI COIN, the following dependencies are used

| Name | Version |
|--------------------------------------------------------------------------------|-|
| [assert-rejected](https://www.npmjs.com/package/assert-rejected)               | `>= 1.1.1 < 2.0.0` |
| [ESlint](https://www.npmjs.com/package/eslint)                                 | `>= 4.15.0 < 5.0.0`|
| [eth-gas-reporter](https://www.npmjs.com/package/eth-gas-reporter)             | `>= 0.1.9 < 1.0.0` |
| [solc-js](https://www.npmjs.com/package/solc)                                 | `0.4.24` |
| [Solium](https://www.npmjs.com/package/solium)                                 | `>= 1.1.8 < 2.0.0` |
| [solium-plugin-zeppelin](https://www.npmjs.com/package/solium-plugin-zeppelin) | [Git `aec043`](https://github.com/OpenZeppelin/solium-plugin-zeppelin/commit/aec043c) |
| [truffle](https://www.npmjs.com/package/truffle)                               | `>= 4.1.13 < 5.0.0` |
| [truffle-flattener](https://www.npmjs.com/package/truffle-flattener)                               | `1.2.5` |
| [web3-utils](https://www.npmjs.com/package/web3-utils)                   | `>= 1.0.0-beta.34 < 2.0.0` |
