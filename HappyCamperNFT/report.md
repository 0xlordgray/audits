# HappyCamperNFT Smart Contract Audit

![HappyCamperNFT logo](https://pbs.twimg.com/profile_images/1538621928465997826/jvWWa6Id_400x400.jpg)

| Website | https://www.happycampernft.io/ |
| Reviewer | https://twitter.com/0xlordgray |
| Audit date | 26th August 2022 |

## Audit goals

The purpose of this audit is to perform the following:

- Identify major security issues
- Review compiler bugs
- Check and provide recommendations for best practices

## Contract details

| Type | NFT |
| Standard | ERC721A |
| Blockchain | ETH |
| Language | Solidity |
| Compiler version | v0.8.7+commit.e28d00a7 | 
| Optimisations | *Yes* with **1000** runs|
| License | MIT |
| Name | HappyCamperNFT |
| Symbol | HAPPY |
| Supply | 5000 |

The audited contract was deployed to Goerli Testnet network. To make sure no changes were made to the contract please review sha3 for source files.

| Deployment | https://goerli.etherscan.io/address/0xC95a6fbEacB66d9Af9568267F87A10edcde8BE83 |

### Source files (12)

| HappyCamperNFT.sol | 0f5334d92c54841506e5302d33261ebf9e126bd6925817c108a41b0e4397c7424d946c8539045d811911b27d17e779244f953a283fe8b5d59cf891351168bf04 |
| Ownable.sol | b9c836bce7fea85dce4836ef914b0c31b63e502ae292c506c0577519d625225727e920c54d846ebfe2708c7df9a2458ae5d9dda04804ffd7a07de56eff75347a |
| MerkleProof.sol | c0cccfb34cb09245df0dcb2896a0c979f78914e7fe3e1758a6baec1bce8fc7f2f9f1c0de48eb820caee80a490f458a359bb2bf41419642e2055ca4ae684043e7 |
| ERC721A.sol | 4e97f9921945bb4f0ccaf3dc9cd2fc71632539b457e5793a706465d50776bd25b63353145d92208b66533bb940125eeefdfeaf185b697e5e4325f5dc24b31948 |
| Context.sol | a5996e4fd75e4d201f6c567a60660fc3ee8df921bc6d1f05d56fe8cf2bf4126151af1a9348dbb95d6c543bb45031c9edd6a6afc673b62216beecc6c998835d5f |
| IERC721.sol | c81beb469b34b576f870cc2ce329de37eddf090f431792abb46a1a7a4d104bfb00799e04bec3c897a4eca535e284415d6e042f47371a4115400869b73c9d7e0d |
| IERC721Receiver.sol | 178ae409e8ed7f478baa97bcb7294c11f1445111e1306e3ff04e6f9e93e3592f3ee44168599ac8b4fd78f41162139171ea4dfd50c0dcaa478c03ae6c7952b7eb |
| IERC721Metadata.sol | f23562c4f39e22171b64879747799b007e1fa0e173dee482824a465bc243937e7967fb6290259ecf2391dfbb978ea1d7daa5a08b7b1521ae80b286012a5002a4 |
| Address.sol | 82eabd80857ebda5dc22afd78ed34de718e2f858c65370e879e464ba55b84e1fe40794a53e306cc5b8ccddfd90825695a8317e381f4ac2db9c727980d48bc523 |
| Strings.sol | 0d482eb9aee1bf991d8ca3fc81a8bb3e5ff1f5ba66730fec0ecc14db335a1c0f03bbcc2cc48adbf36371a3a20b81ae588c19a2467f005d008c875ee2d47ec974 |
| ERC165.sol | 418fb00887f4354f1fb5ba7216c73ffba7790c7276469c1b8292bd80fcb1d66ca21fdfaae7b566b336aad61d8e8d4413cadb8dc3dc5ea8b97625fcddf004b790 |
| IERC165.sol | 6a39db2a18be0fe2d5568b0dd8f312c25c2872e671593cea533af37dd75488826fb9e00301d6553ff41d602b51598f6dc5f401a88317eb83685c7529c7781dcc |