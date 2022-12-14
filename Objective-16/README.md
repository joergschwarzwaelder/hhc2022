
# Objective 16: Exploit a Smart Contract
**Location: Cloud Ring**  
**Elf: ?**

This objective is about getting familiar with Merkle tree.
These are hash trees which can be used for proofing that a given element is contained in this tree whilst using limited resources.

For this we have to buy an BSRS NFT issued by a terminal. Only wallets included on the pre-sale list (managed on the blockchain) are eligible to buy one. In order to proof that we are on the pre-order list, we have to provide our wallet address and a proof on the purchase.

Using the script [merkle_tree.py](https://github.com/QPetabyte/Merkle_Trees) from Prof. Petabyte's repository we can calculate tree root and proof for given elements.
When adding our own wallet address along with a dummy address to the script, it calculates which root and proof values would be required.

```
allowlist = ['0xe5d7FcfF7ab197Dd9359ED3De8b2C7Fa42200b7B','0x0000000000000000000000000000000000000000']
```

As the root for the validation process is contained in the bsrs.js file of the web application (and not pulled from the blockchain), we can modify this to the value required according to Prof. Petabyte's script.

```
Root: 0x4350073a37d2ea7ffa09192ace76408beee7252f920b20c0423ca5712e19e0e5
Proof: ['0x5380c7b7ae81a58eb98d9c78de4a1fd7fd9535fc953ed2be602daaa41767312a']
```

![root changed in bsrs.js](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-16/bsrs.js.png)
Now we can validate our wallet and proof in the terminal:
![enter image description here](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-16/nft-validation.png)
And finally perform the purchase:
![enter image description here](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-16/nft-purchase.png)
**Achievement: Exploit a Smart Contract**



