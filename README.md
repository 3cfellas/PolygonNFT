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

## Development

### Prerequisites

The following tools are required to compile and test the contract:

- Node.js and npm
- Hardhat
- ethers.js
- openzeppelin contracts
- Remix IDE

### Installation

1. Create a new project folder and initialize it with npm:

```sh
mkdir nft-tutorial
cd nft-tutorial
npm init
```

2. Install the required dependencies:

```sh
npm install --save-dev hardhat @nomiclabs/hardhat-ethers @nomiclabs/hardhat-etherscan @openzeppelin/contracts dotenv [email protected]^5.0.0 [email protected]
```

3. Initialize Hardhat:

```sh
npx hardhat
```

### Testing

The contract can be tested using Hardhat's built-in testing framework.

## Deployment

The contract can be deployed to any Ethereum-compatible network using Hardhat or Remix IDE. For testing purposes, you can use the Rinkeby testnet and get Rinkeby Ether from a faucet.

Please note that the contract requires some initial setup after deployment, such as setting the

contract URI, granting the minter role, and setting the royalty recipient.

This contract can also be deployed on the Polygon network, a Layer 2 solution for Ethereum. Polygon provides faster and cheaper transactions compared to Ethereum's mainnet, making it a popular choice for many DeFi and NFT projects. As this contract is written in Solidity and compatible with the EVM, it can be deployed on Polygon with no modifications.

Interoperability between Ethereum and Polygon is facilitated by the Polygon Bridge, which allows for the easy transfer of assets (including NFTs) between the two networks. This means that NFTs minted on Polygon can be moved to Ethereum, and vice versa.

## Security

Keep your wallet credentials private. When creating your new MetaMask wallet, you'll be given a seed phrase of 12 randomly generated words. These words can give you (or anyone else!) access to your account to send transactions and add or remove funds from your account. Keep this seed phrase somewhere secure, and never share it on the internet. 

## License

The project is licensed under the MIT license.
