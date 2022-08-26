# HappyCamperNFT Smart Contract Audit

![HappyCamperNFT logo](https://pbs.twimg.com/profile_images/1538621928465997826/jvWWa6Id_400x400.jpg)

<table>
  <tr><td>Website</td><td>https://www.happycampernft.io</td></tr>
  <tr><td>Twitter</td><td>https://twitter.com/HappyCamperNFT</td></tr>
  <tr><td>Reviewer</td><td>https://twitter.com/0xlordgray</td></tr>
  <tr><td>Audit date</td><td>26<sup>th</sup> August 2022</td></tr>
</table>

## Audit goals

The purpose of this audit is to perform the following:

- Identify major security issues
- Review compiler bugs
- Check and provide recommendations for best practices

## Contract details

<table>
  <tr><td>Type</td><td>NFT</td></tr>
  <tr><td>Standard</td><td>ERC721A</td></tr>
  <tr><td>Blockchain</td><td>ETH</td></tr>
  <tr><td>Language</td><td>Solidity</td></tr>
  <tr><td>Compiler version</td><td>v0.8.7+commit.e28d00a7</td></tr>
  <tr><td>Optimisations</td><td><strong>Yes</strong> with 1000 runs</td></tr>
  <tr><td>License</td><td>MIT</td></tr>
  <tr><td>Name</td><td>HappyCamperNFT</td></tr>
  <tr><td>Symbol</td><td>HAPPY</td></tr>
  <tr><td>Supply</td><td>5000</td></tr>
  <tr><td>Max per TX</td><td>5</td></tr>
</table>

The audited contract was deployed to Goerli Testnet network. To make sure no changes were made to the contract please review sha3 for source files.

<table>
  <tr><td>Deployment</td><td>https://goerli.etherscan.io/address/0xC95a6fbEacB66d9Af9568267F87A10edcde8BE83</td></tr>
</table>

### Source files (12)

| File | SHA3 |
|:-|:-|
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

### Severity Table

|  | Severity | Description |
| --- | --- | --- |
| 🔴 | High | Malicious code that subverts the intended functionality. Requires immediate attention. |
| 🟡 | Medium | Non reverting problems that arise when users interact with the contract. Recommended fixes. |
| 🔵 | Low | Minor issues or failure to follow standard conventions and potential gas optimizations. Optional fixes. |

## Found issues

| Level | Count |
| --- | --- |
| 🔴  High | 0 |
| 🟡  Medium | 1 |
| 🔵  Low | 1 |
| Total Issues | 2 |

### Issue 1: The return value of a message call is not checked

External calls return a boolean value. If the callee halts with an exception, `false` is returned and execution continues in the caller. The caller should check whether an exception happened and react accordingly to avoid unexpected behavior. For example it is often desirable to wrap external calls in require() so the transaction is reverted if the call fails.

```solidity
    // WITHDRAW
    function withdraw() public onlyOwner {
        uint256 contractBalance = address(this).balance;
        bool success = true;

        (success, ) = payable(0xFA9A358b821f4b4A1B5ac2E0c594bB3f860AFbd8).call{
            value: (45 * contractBalance) / 1000
        }("");
        (success, ) = payable(0x44230C74E406d5690333ba81b198441bCF02CEc8).call{
            value: (45 * contractBalance) / 1000
        }("");
        (success, ) = payable(0xe9b9691Bee2252235D79d4ba874337B018d2A7F1).call{
            value: (100 * contractBalance) / 1000
        }("");
        (success, ) = payable(0x2f0e10a8e21A85c4951fdD909eDCFF6a0B2EbD13).call{
            value: (486 * contractBalance) / 1000
        }("");
        (success, ) = payable(0x09228B35C37Ec6562B0242Ae8A67501e57D61B87).call{
            value: (324 * contractBalance) / 1000
        }("");
        require(success, "Transfer failed");
    }
```

<table>
  <tr><td>🟡 Medium</td><td><a href="https://swcregistry.io/docs/SWC-104">SWC-104</a></td></tr>
</table>

### Issue 2: A floating pragma is set

The current pragma Solidity directive is `">=0.8.0<0.9.0"`. It is recommended to specify a fixed compiler version to ensure that the bytecode produced does not vary between builds. This is especially important if you rely on bytecode-level verification of the code.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.8.0 <0.9.0;
```

<table>
  <tr><td>🔵 Low</td><td><a href="https://swcregistry.io/docs/SWC-103">SWC-103</a></td></tr>
</table>

## Conclusion

The contract audit found only minor issues. None of the issues are critical and can safely be ignored. 

Max supply, cost per mint (allowlist and public) and max per TX can all be changed by the contract owner at any time. During allow list minting the allowance per address can also be set to a lower value (can also be set to higher if max per TX is changed). Be advised that there is no limit set for the number of tokens minted during allowlist phase, meaning all supply can be minted during this phase (although this could be enforced by lowering max supply).

The withdraw method has predefined splits and addresses where the funds will be withdrawn, meaning that the funds cannot be withdrawn to any other addresses other than the ones provided. Make sure to review they are correct before deploying to mainnet.

| Split | Address |
|:-|:-|
| 4.5% | 0xFA9A358b821f4b4A1B5ac2E0c594bB3f860AFbd8 |
| 4.5% | 0x44230C74E406d5690333ba81b198441bCF02CEc8 |
| 10% | 0xe9b9691Bee2252235D79d4ba874337B018d2A7F1 |
| 48.6% | 0x2f0e10a8e21A85c4951fdD909eDCFF6a0B2EbD13 |
| 32.4% | 0x09228B35C37Ec6562B0242Ae8A67501e57D61B87 |

Due to the time constraints of this report no actual tests were performed - project owner should test on testnet before launching to make sure everything is working correctly.

Additionally only the smart contract audit was performed, any other application code that is interacting with the smart contract is outside of the scope of this report.

### Disclaimer

This report is for informational use only and does not constitute financial advice. No audit guarantees there will be no remaining bugs or vulnerabilities. Project owners follow our recommendations of their own accord, and auditor is not responsible for any actions taken by project owners. The smart contract security and analysis is based on auditors findings at the time of the audit. The examination of the smart contract's code base was performed following industry best practices at the date of the audit. This report provides no warranties or guarantees on the security of the code. You should not rely solely on this report as a measure of the smart contract's security profile, and performing multiple independent third-party audits is recommended. Smart contract anaylsis was made with best intentions; however, you may not make claims against the auditor given what the report says or does not say. This report and its findings only cover the smart contract's source code, and no applications or code apart from the smart contract were reviewed.
