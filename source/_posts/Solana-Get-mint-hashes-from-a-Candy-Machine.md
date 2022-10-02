---
title: 'Solana: Get mint hashes from a Candy Machine'
date: 2022-09-06 06:52:50
tags:
---

Solana is a pretty cool project, it's smart contract ecosystem is exquisite and detailed but the documentation and methodologies are pretty lacking. Especially those surrounding NFTs.

Recently I was working on a project that had to download mint hashes of NFT projects from their respective candy machine, after a bit of googling no solution came across as straight forward so I took the liberty to publish an NPM [package](https://www.npmjs.com/package/@alchemilla/solana-nft-tools) with the utilities that will help me with this project as well as others.  

It's pretty straight forward to use it, you can install it from NPM using

```bash
npm install @alchemilla/solana-nft-tools
```

And then use it in your code as such

```js
const  nftTools  =  require("@alchemilla/solana-nft-tools");
const  {  Connection  }  =  require("@solana/web3.js");
const  connection  =  new  Connection('RPC_URL','confirmed');

(async  ()  =>  {
	const  mintHashes  =  await nftTools.getMintHashesFromCandyMachine(connection,'CANDY_MACHINE_ID', CANDY_MACHINE_VERSION);
	console.log(mintHashes);  /* An array of mint hashes */
})();
```

Replace `RPC_URL` with either the solana official RPC url or something like [QuickNode](https://www.quicknode.com). From my experience the solana official RPC is extremely bad due to the fact that it rate limits you heavily.

Replace `CANDY_MACHINE_ID` with the candy machine with that of the one you want to get mint hashes of.

Replace `CANDY_MACHINE_VERSION` with the version of the candy machine you're retrieving mints from.

The process is slow and might take a few minutes especially for a lot of mints, so if you're using this in your project it's better to cache the array returned from the `getMintHashesFromCandyMachine` function.
