# html-nft-starter

This small web app exists within an NFT. The idea is to condense an entire album into a single NFT Collectible where the user may also playlist the album inside the NFT. This allows for a few things the first being the entire experience can be enjoyed in the metaverse or virtual NFT Gallery. The second this showcases how interactive NFT's can be. If a webapp can exist within an NFT then what else can be created???? No more monkey jpgs!

Wᒷ'∷ᒷ ℸ ̣ ⍑ᒷ ᔑꖎ╎ᒷリᓭ, ∴ᒷ ⋮⚍ᓭℸ ̣ ⎓𝙹∷⊣𝙹ℸ ̣.

Dᒷᓭ╎⊣リᒷ↸ ʖ|| l||⊣⍑ℸ ̣ c𝙹↸ᒷ


example on [OpenSea](https://opensea.io/assets/matic/0xa924ead9001efe0edb96353c0a356b63e3714389/2)

## Creating a NFT project

Use this as a starter or create your own HTML NFT project. The most important part is configuring the metadata parameter "animation_url:".
This example repo is deployed with vercel. You can use whatever deployment service you'd like just change the animation_url to your deployment URL.
Configuring this parameter in the [metadata.json](https://github.com/LyghtCode/html-nft-starter/blob/main/src/lib/images/webnft.json) will insure OpenSea and other marketplaces display the NFT correctly.

```bash
{
    "name": "LyghtCode Web NFT",
    "symbol": "MAYA",
    "description": "Wᒷ'∷ᒷ ℸ ̣ ⍑ᒷ ᔑꖎ╎ᒷリᓭ, ∴ᒷ ⋮⚍ᓭℸ ̣  ⎓𝙹∷⊣𝙹ℸ ̣.",
    //
    "animation_url": "https://digital-album-nft-v1.vercel.app/"
  }
```

## Deploying

Once you've configured your metadata pin the metadata with NFT Storage, Pinata or your own IPFS Node. I used Pinata for this example.


## Building/Designing your own NFT

Any SSR functionality will break the NFT even though in localhost it will seem okay. 500 error is most common error when making this type of NFT. 
CSR Only or follow this reddit [thread](https://www.reddit.com/r/sveltejs/comments/ste8za/500_error_object_is_not_defined/).
Don't use UI frameworks it will cause problems when displaying the NFT (MaterialUI, Chakra, etc).
Svelte>Next>React for this type of project. It's in the way it compiles ;)
Routing is buggy, stick to Single Page Applications
External Links don't work!!! Don't even try :(


> Designed by LyghtCode have fun get creative.
