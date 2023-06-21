# PolygonNFT / NFT Royalty Smart Contract README
A smart contract for an nft collection on polygon that is streamlined for trading on opensea

This repository contains an implementation of an NFT contract with built-in royalty payments. The contract is based on the ERC721 standard and additionally supports the ERC2981 royalty standard.

The contract is written in Solidity and can be deployed on Ethereum and Polygon networks. It can be interacted with via various environments like Hardhat and Remix IDE. 

## Features

The contract supports the following features:

### Owner-Only Functions

- `setContractURI(string memory newContractURI)`: This function allows the contract owner to set the URI for the contract's metadata.
- `grantMinterRole(address newMinter, uint256 minTokenId, uint256 maxTokenId)`: This function allows the contract owner to grant the minter role to an address, specifying a range of tokenIds that the minter is allowed to mint.
- `setRoyaltyRecipient(address newRoyaltyRecipient)`: This function allows the contract owner to set the address to receive royalty payments.
- `setRoyaltyPercentage(uint256 newPercentage)`: This function allows the contract owner to set the percentage for royalty payouts. The value must be a fraction of 10^18, i.e., 10% would be represented as 100000000000000000.

### Minter-Only Functions

- `mint(address to, uint256 tokenId, string memory tokenURI)`: This function allows an address with the minter role to mint new tokens. The tokenId must be within the range set for the minter, and the tokenURI is the metadata URI for the new token.

### Public Functions

- `contractURI()`: This function returns the URI for the contract's metadata.
- `supportsInterface(bytes4 interfaceId)`: This function checks if the contract implements an interface and returns true if it does. It is overridden to add support for the ERC2981 royalty interface.
- `royaltyInfo(uint256 _tokenId, uint256 _salePrice)`: This function returns the address of the royalty recipient and the amount to be paid out for a given sale price. It is part of the ERC2981 standard.
- `isApprovedForAll(address owner, address operator)`: This function checks if an operator is approved to manage all of an owner's tokens. It is overridden to whitelist the OpenSea proxy contract for gasless transactions.

### Internal Functions

- `_msgSender()`: This function returns the original sender of the transaction. It is overridden to support metatransactions.
- `_msgData()`: This function returns the calldata of the transaction. It is overridden to support metatransactions.

# Development

In this section, we will cover the requirements and steps to set up a local development environment, how to compile and test the contract, and how to interact with it using Hardhat or Remix IDE. This guide assumes a basic familiarity with Ethereum smart contracts and Solidity.

## Prerequisites

1. **Node.js and npm:** Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine, and npm is the package manager for Node.js. You can download Node.js and npm [here](https://nodejs.org/en/download/). 

2. **Hardhat:** Hardhat is a development environment to compile, deploy, test, and debug your Ethereum software. It helps developers manage and automate the recurring tasks that are inherent to the process of building smart contracts and blockchain solutions. Install Hardhat globally using npm:

```sh
npm install --global hardhat
```

3. **Ethers.js:** Ethers.js is a library that makes it easier to interact with the Ethereum blockchain. Install it using npm:

```sh
npm install --save ethers
```

4. **OpenZeppelin Contracts:** OpenZeppelin Contracts is a library for secure smart contract development. Install it using npm:

```sh
npm install @openzeppelin/contracts
```

5. **Remix IDE:** Remix is a powerful, open-source tool that helps you write Solidity contracts straight from the browser. It is used for smart contract development, debugging, testing and deployment. You can access it [here](https://remix.ethereum.org/).

## Setup

After installing the prerequisites, follow these steps:

1. Create a new project folder:

```sh
mkdir nft-tutorial
cd nft-tutorial
```

2. Initialize the project with npm:

```sh
npm init
```

3. Install the project dependencies:

```sh
npm install --save-dev hardhat @nomiclabs/hardhat-ethers @nomiclabs/hardhat-etherscan @openzeppelin/contracts dotenv [email protected]^5.0.0 [email protected]
```

4. Initialize Hardhat in your project:

```sh
npx hardhat
```

This will create a `hardhat.config.js` file in your project root, where you can configure your Hardhat setup.

5. For Remix IDE, you can directly copy and paste the smart contract code into the IDE's editor. Make sure to select the correct compiler version and enable optimization in the compiler settings.

## Compilation

To compile the contract using Hardhat, run:

```sh
npx hardhat compile
```

This will compile all Solidity files in your project and output the artifacts into the `artifacts` directory.

For Remix IDE, you can compile the contract by clicking on the "Compile" button.

## Testing

Write tests for your smart contract using Hardhat's testing framework, which is based on Mocha and Chai. You can run your tests with:

```sh
npx hardhat test
```

In Remix, you can write tests using Solidity or JavaScript under the "Testing" tab, and then run them.

## Deployment

In order to deploy your contract, you will need to have a wallet with some Ether. For testing purposes, you can use the Rinkeby testnet and get Rinkeby Ether from a faucet.

In Hardhat, you can write a deployment script in the `scripts` directory and then run it with:

```sh
npx hardhat run scripts/deploy.js
```

In Remix, you can deploy the contract by going to the "Deploy & Run Transactions" tab, selecting the right environment and account, and clicking on "Deploy".

Remember to set up your contract after deployment

## Interacting with the Contract

After deploying the contract, you can interact with it in various ways.

In Hardhat, you can use the `hardhat console` to interact with your contract. Import the contract's artifacts and the ethers library, create a new instance of the contract, and then you can call its methods:

```sh
npx hardhat console
```

```js
const { ethers } = require("hardhat");
const contractAddress = ""; // replace with your contract's address
const Contract = await ethers.getContractFactory("YourContract");
const contract = Contract.attach(contractAddress);

// call a method
const result = await contract.yourMethod();
```

In Remix, you can interact with the contract under the "Deploy & Run Transactions" tab. After deploying the contract, it will appear under the "Deployed Contracts" section. You can expand it to see the contract's methods and call them.

## Polygon and Ethereum Interoperability

This project is developed with Ethereum in mind, but the contract can also be deployed on the Polygon network with minor or no modifications. Polygon is a Layer 2 scaling solution for Ethereum, offering faster and cheaper transactions. It is fully compatible with the Ethereum infrastructure, which means you can use the same tools (like Hardhat, ethers.js, and Remix) and the same wallet addresses.

Moreover, the NFT contract in this project uses the ERC721 standard, which is a standard interface for non-fungible tokens on Ethereum. This means it can be used on any network that supports this standard, including both Ethereum and Polygon. This allows for a wide range of interoperability, such as trading NFTs across different networks.

## License

This project is licensed under the MIT license, which is a permissive license that allows for reuse with few restrictions. The license allows others to copy, modify, distribute, and use the work for any purpose, including for commercial purposes, provided that they give appropriate credit and do not hold the original author liable.

---

This is a broad overview of the development process for this project. For more specific instructions and details, please refer to the individual files and comments in the code. If you have any questions or encounter any issues, feel free to open an issue on the project's GitHub page.
