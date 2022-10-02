---
title: In defense of NFTs
date: 2022-08-12 22:35:35
tags: nfts, crypto, bitcoin, blockchain
---

![monkey-nft](https://imagedelivery.net/SM0H54GQmiDTGcg4Xr4iPA/4214267f-521b-4503-3d0c-834a38117e00/1692)

What emotion does the image above invoke in your mind? For an overwhelming amount of people I've seen recently it's either confusion or sheer anger. Neither of which is innately positive, I believe that the lack of understanding of the novel idea of NFTs is the cause for both. Just for posterity I too hate these monkey jpegs but I want to delve into the possibilities where NFTs could actually serve a viable purpose.

## What are NFTs?

According to wikipedia

> Non-fungible tokens are a financial security consisting of digital data stored in a blockchain, a form of distributed ledger. The ownership of an NFT is recorded in the blockchain, and can be transferred by the owner, allowing NFTs to be sold and traded. NFTs can be created by anybody, and require few or no coding skills to create.[1] NFTs typically contain references to digital files such as photos, videos, and audio. Because NFTs are uniquely identifiable assets, they differ from cryptocurrencies, which are fungible.

I remember the first time I read this, the term fungible was foreign to me (perhaps due to english not being my first language). What does it actually mean? Well it basically means that not all NFTs are of same value. For instance 1 USD = 1 USD or 1 ETH = 1 ETH but one NFT doesn't necessarily (almost never) equal in value to another one. 

That seems simple enough, right? I mean we have a lot of non-fungible items in our lives. Our identity cards, land deeds, insurance documents, **artwork**, etc etc. Not all NFTs necessarily need to have a particular value either, not everything has a price.

## A tangible use case

This is the part of the post where I'm supposed to *defend* the idea of NFTs, well since the very first moment I read about these things I couldn't stop thinking about one thing which is storage for documents that are particularly unique. I'm talking about things like identity cards, certificates and perhaps real estate documents. 

Let's take the case of real estate documents, in India where I'm from land deeds look like this.

<p align="center">
<img width="512px" src="https://imagedelivery.net/SM0H54GQmiDTGcg4Xr4iPA/46c6c744-b2ba-408f-b6cd-d68e71d98300/1692" alt="land deed">
</p>

A lot of it still stored in hard copies, albeit with a lot of [push](https://economictimes.indiatimes.com/news/economy/policy/digitizing-land-records-in-india-centres-challenge-to-alleviate-concerns-around-it-and-bring-states-on-board/articleshow/91859437.cms) from the government for the digitization of such documents. 

An initiative that aims to achieve complete digitization is [Digilocker](https://www.digilocker.gov.in/), although it's pretty cool to have a state sponsored digital locker, it still poses grave concerns as to how private it actually is. Security of aforementioned documents are paramount in a country where such documents being leaked could lead to unpleasant situations, sometimes disputes arising from doctored documents taking so long as 20-30 years to clear up. With Digilocker making it harder for non-techies to access and perhaps manipulate these documents, it just opened up it's doors to a new kind of [threat](https://dynamicciso.com/indian-digilocker-flaw-let-hackers-accessover-3-8-crore-accounts-without-password/).

### The role of NFTs

Now the process for acquiring and safe keeping of real estate documents goes something like this: 

Person purchases land → Land deed acquired from the government or the seller of the property → Person stores the documents safely in both hard copy and soft copy online.

Now both the hard copy and soft copies of this document are not invulnerable to threats, the hard copies can be stolen and the soft copies, well we've seen [this](https://dynamicciso.com/indian-digilocker-flaw-let-hackers-accessover-3-8-crore-accounts-without-password/) before. 

Now imagine the following flow:

Person purchases land → Land deed which is an encrypted document which is stored on [IPFS](https://en.wikipedia.org/wiki/InterPlanetary_File_System) is acquired -> Person stores the IPFS hash as an NFT on the blockchain for proof of ownership.

This would mean, the person having said documents can both claim ownership (without providing an NFT metadata that predates the document in question no one else can prove ownership prior to the current owner) as well as keep it private using good old AES or some other encryption standard (this key can be shared to authorities for verification in times where verification is needed).

## Conclusion

I created a simple demo NFT available [here](https://testnets.opensea.io/assets/rinkeby/0x88b48f654c30e99bc2e4a1559b4dcf1ad93fa656/115698739412528589057515172288870538128850639087955430963416544495406187282433) to showcase how cool this can actually be! 

It's an encrypted image of the land deed I featured above, now immortalized on the rinkeby testnet using opensea. I skipped a few steps like IPFS storage and AES encryption for ease of demonstration, but I hope you get the idea.
