
# Objective 16: Exploit a Smart Contract
**Location: Burning Ring of Fire / Bored Sporc Rowboat Society Terminal**  
**Hints from hidden chests (2x)**

This objective is about getting familiar with Merkle tree.
These are hash trees which can be used for proofing that a given element is contained in this tree whilst using limited resources.

For this we have to buy an BSRS NFT issued by a terminal. Only wallets included on the pre-sale list (managed on the blockchain) are eligible to buy one. In order to proof that we are on the pre-order list, we have to provide our wallet address and a proof on the purchase.

Using the script [merkle_tree.py](https://github.com/QPetabyte/Merkle_Trees) from Prof. Petabyte's repository we can calculate tree root and proof for given elements.
When adding our own wallet address along with a dummy address to the script, it calculates which root and proof values would be required for a successful validation.

```
allowlist = ['0xe5d7FcfF7ab197Dd9359ED3De8b2C7Fa42200b7B','0xa1861E96DeF10987E1793c8f77E811032069f8E9']
```

As the root for the validation process is contained in the `bsrs.js` file of the web application (and not pulled from the blockchain), we can modify this to the value required according to Prof. Petabyte's script.

```
Root: 0x96155cb9f0bd419a88a5fc2d3c678652fd460d3dd84db8faa3a8028d426884db
Proof: ['0x3ca7b0f306be105d5e5b040af0e2bc35fb95026afcd89f726e8e94994c312f79']
```

Now we can put the calculated root into the `bsrs.js` file and are able to validate our wallet and proof in the terminal:
![enter image description here](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-16/nft-validation.png)
And finally perform the purchase:
![enter image description here](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-16/nft-purchase.png)
![BSRS #000026](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-16/BSRS26.png)

**Achievement: Exploit a Smart Contract**



