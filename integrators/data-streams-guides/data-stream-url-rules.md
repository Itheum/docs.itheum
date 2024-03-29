# Data Stream URL Rules

## Specific rules relating to the URL

1. The URLs need to served via HTTPS (e.g. https://)
2. They can be "Unauthenticated" URLs if the data is non-sensitive.
3. They can also be "Authenticated" URLs if the data is sensitive as described in [guide-1-minting-a-custom-data-nft-collection-with-authenticated-data-streams-via-sdk.md](../../developers/software-development-kits-sdks/data-nft-sdk/guide-1-minting-a-custom-data-nft-collection-with-authenticated-data-streams-via-sdk.md "mention")
4.  They need to be "public" URLs and should be accessible on the World Wide Web

    1. A) Unauthenticated URLs should always return the [200 OK HTTP Code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200)
    2. B) Authenticated URLs should return the [403 FORBIDDEN HTTP Code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403) if the authentication failed and 200 OK HTTP Code if the authentication scheme passes

    _If you need any other HTTP code to be supported, reach out to us on_ [_Discord_](../../developers/tech-support-discord.md) _and we are open to discussing the use case._
5. If you are using a service like AWS S3 to host your URLs, it's recommended that you abstract the AWS S3 URL by putting domain name in front of it. This will future-proof your URLs and allow for the flexibility to move from AWS S3 to another origin. See [hosting-aws-s3-+-cloudflare](amazon-web-services-aws/hosting-aws-s3-+-cloudflare/ "mention") to learn more
6. It is advisable to treat your Unauthenticated as "Unlisted" content URLs. A good example of "unlisted" content URLs are YouTube's "unlisted videos", where the videos are fully public but you can only reach them if you know the exact URL. To make them "Unlisted":
   1. A) use a system like robots.txt or other such methods to prevent them from being indexed by search engines
   2. B) Never publicly link to these URLs from your websites or apps
   3. C) Make the URLs "random" (see next point)
7. To assist in making your URLs unlisted and un-guessable, it's best you have random paths in your URL. e.g. https://mydomain.bar/sdahjasdkkasd/hkkasdk2321313ka.json
8. Only have alphanumeric characters (a-z, 0-9) in your URL and do not include spaces or any symbols.&#x20;
9. When you mint your Data Stream URL into a Data NFT, note that your URL is case sensitive as the Data Marshal considers origin URLs as case sensitive. e.g. https://mydomain.bar/sdahjasdkkasd/hkkasdk2321313ka.json and https://mydomain.bar/SDahjasdkkaSD/HKKasdk2321313KA.json are considered separate URLs
10. Data Marshal starting V2 Brontes and above will also support `ipfs://{CID}` and `ipns:{HASH}` URLs



## Other rules related to content served from the URLs (origin)

10. Although this is NOT related to URL standards, note that the Data Marshal node (V1 Achilles) can only support a maximum data payload of 4.5MB but handle a lot of bandwidth request volume. Data Marshal node (V2 Brontes) can handle a much high limit data payload but may have some request bandwidth limitations for extreme high volumes.&#x20;
11. Your origin server can forward the following headers, which will be passed-through to your client app:

    1. content-length
    2. content-type&#x20;
    3. x-cache (bespoke header your can send to inform the client if a CDN-based origin HIT or MISSED. [Example flags you can use](https://developers.cloudflare.com/cache/concepts/default-cache-behavior/#cloudflare-cache-responses))

    _If you need any other pass-through headers supported, reach out to us on_ [_Discord_](../../developers/tech-support-discord.md) _and we are open to discussing the use case._
12. Your origin server can stream out any file type and indicate it via the content-type header; we've provided some [code guidance on handling the following types](../../developers/software-development-kits-sdks/data-nft-sdk/guide-2-unlocking-data-nfts-via-multiversx-native-auth.md#bonus-step-5-how-can-i-parse-non-json-data-streams) which we've personally tested. (This is not an exhaustive list and other formats are also supported)
    1. JSON
    2. PDF
    3. CSV
    4. AUDIO (e.g. mp3)
    5. TEXT
    6. SVG
    7. IMAGE  (PNG, JPG, GIF)

{% hint style="info" %}
On top of the above rules, it important to note that the Data Streams are "unlocked" via the [data-marshal-network.md](../../product/data-marshal-network.md "mention") node network, so it's also important to understand some additional features/limitations the Data Marshal nodes may enforce on your Data Streams. Learn about these here: [data-marshal-node-endpoints.md](../../developers/data-marshal-network/data-marshal-node-endpoints.md "mention")
{% endhint %}



Now, let's now jump into out platform specific guides of producing these Data Stream URLs using various platforms and architectures...
