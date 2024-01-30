# Guide 3 : Using Nested Streams to Access Nested Data Assets from a Primary Data Stream

This guide walks you through how to use Data Streams configured to be “nested streams” and how client-side apps can use the Itheum SDK to interact with these nested streams.

Firstly, what are nested streams and who are they needed? As detailed in the [data-streams-guides](../../../integrators/data-streams-guides/ "mention"), we see that Data NFTs provide "web3 licensed" access to Data Streams, i.e., Data NFTs are a license to use your data. In most cases, your Data Stream will be "dynamic," where it can evolve to have its data change over time. An example of a dynamic Data Stream is could be some on-chain analytics data you have sourced, maintained, and kept updated, similar to the [MultiversX Bubbles Data NFT](https://explorer.itheum.io/multiversx-bubbles). The Data Marshal can "stream out" the complete Data Stream once ownership of the Data NFT has been proved. The Data Marshal is also responsible for protecting the primary Data Stream link and aims never to expose the original data location (it only streams out the content).

The "hide original URL location and stream" mechanism of the Data Marshal works well when those above mentioned "dynamic" Data Streams are mostly also "self-contained" and "complete" and don't contain links within them that need to be "hidden" as they are part of the original outcome of the Data Stream. For example, image files, PDFs, SVG documents etc are most likely "complete" documents. So, in this situation, the Data Marshal does not need to hide and protect any secondary links located within the original data.

But what if your use-case requires that you have nested links within the original Data Stream that you also want to "hide" and protect, and use the same "hide original URL location and stream" features of the Data Marshal?

This is where "nested streams" come into play, but to get your head around it - let's look at a real-world example of nested streams being built on Itheum.

### Building a "Music Playlist" Data NFT

You could build a music playlist or music player experience using Data NFTs, nested streams and the Itheum `Data NFT SDK`. In this use case, your primary Data Stream has a list of songs hosted in some location and would want the Data Marshal to mask/hide that data to protect the source/origin of the individual files. You can think of your primary "base" version of the Data Stream as a sort of manifest or instruction file that can use by the client app to unpack a complete user experience. Nested streams allow for this functionality; in the example of the music player, you can unpack the original Data Stream as usual, but if the origin Data Stream server has flagged it as the “nested stream,” the Data Marshal is smart enough to discover and hide the links within it that need to be protected.&#x20;

You can then use the Itheum `Data NFT SDK` to iterate and stream the nested links while preserving the origin location of all the nested data assets. In the context of the music player, you get the primary "base" version of the nested stream, which provides all the data needed to render the music interaction (song titles, album art, etc.), but then you use the `Data NFT SDK` to play the actual music assets when the user clicks on play, next, back etc. We will explore the code needed to do this below.

***

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* You need **@itheum/sdk-mx-data-nft v2.1.0** or above to follow this guide.
* This guide assumes that you are integrating with Itheum via an application built on the MultiversX blockchain, you use TypeScript/JavaScript as your programming language and that you use that use the **@multiversx/sdk-core** and **@multiversx/sdk-dapp** libraries to authenticate and sign and track on-chain transactions. Although, these libraries are optional and you can use any MultiversX tooling to interact with the blockchain.
* To open a Data NFT and view it's data using using the `Data NFT SDK`, you have implemented MultiversX Native Auth integration with Itheum as per this the guide [guide-2-unlocking-data-nfts-via-multiversx-native-auth.md](guide-2-unlocking-data-nfts-via-multiversx-native-auth.md "mention")
* You have control of the origin Data Stream publishing system (see Step 1 setup section below), as you will need to set HTTP Response Headers on the Data Stream.

***

## Target User Story:

_The target user story builds on the above **Building a "Music Playlist" Data NFT** section._

{% hint style="info" %}
As an integrator of Itheum web3 Data Brokerage infrastructure:

* I'd like to build a Music Player app that supports all Data NFTs that follow a standard "music player nested stream" format.
  * This Music Player app empowers the musicians who minted their songs as a Data NFT with the means to truly own their original music data.
  * This Music Player app can also evolve into a "decentralized Spotify," where I build and maintain the "front-end" music player features (and possibly charge a subscription fee for "premium" features), and musicians around the world can own their music data and earn royalties directly from the trade of their songs on my app.
{% endhint %}

Let's begin...

***

## Step 1: Configure Data Stream Origin "Backend" for Nested Streams

Your Data Stream could be hosted by any of the data hosting service options provided in[data-streams-guides](../../../integrators/data-streams-guides/ "mention"). If you are not requiring the behaviour of a "nested stream", you do not need to do anything extra above hosting your data and making it available as a public URL. But in the event you do need to configure your Data Stream as a nested stream, then your backend Data Stream server will need to send down a custom [HTTP Response Header](https://developer.mozilla.org/en-US/docs/Glossary/Response\_header).

We will make the "Response Header" name configurable, but for now as we are still in "beta" mode, the target header looks needs to be : &#x20;

```
x-amz-meta-marshal-deep-fetch = 1
```

<figure><img src="https://lh6.googleusercontent.com/PuyHcRHyFCfyza6ww7VaR1oxWMaZoF3ZL2Z88sc2j_9nAqoANmWmvMxGX03QBmHaj2yM7ISmvMVsB6maZaJnt4KYv9_ZW43HtOEPN414l7skyUJ0_mB1lygXX70BsqIn5v6tPy8e-3D42oIrfSEaisk" alt="" width="563"><figcaption><p>Example of how the response header is sent by the Origin Data Stream server</p></figcaption></figure>

When the Data Marshal sees this HTTP header during the transit traffic, it will respond as per the rules of a nested stream. If the header is not found, it defaults to the usual behaviour of a general Data Stream.

Your nested stream should ideally follow a data format that is similar to the below sample JSON document that details the nested stream payload for the Music Player app use-case mentioned above.

{% code fullWidth="true" %}
```json
{
  "data_stream": {
    "name": "tokentunes:musiverse:musicx",
    "creator": "Manu",
    "created_on": "2023-05-22T05:37:17Z",
    "last_modified_on": "2023-06-10T14:00:19Z",
    "marshalManifest": {
      "totalItems": 3,
      "nestedStream": true
    }
  },
  "data": [
    {
      "idx": 1,
      "date": "2023-01-02T00:00:00Z",
      "category": "Beats",
      "artist": "Emancipator",
      "album": "Soon It Will Be Cold Enough",
      "title": "Beats are best",
      "file": "https://itheum-static.s3.ap-southeast-2.amazonaws.com/hosteddataassets/musicblazer/manu-song-1.mp3",
      "cover_art_url": "https://521dimensions.com/img/open-source/amplitudejs/album-art/soon-it-will-be-cold-enough.jpg"
    },
    {
      "idx": 2,
      "date": "2023-01-09T00:00:00Z",
      "category": "Funk",
      "artist": "Emancipator",
      "album": "Soon It Will Be Cold Enough",
      "title": "Funk is best",
      "file": "https://itheum-static.s3.ap-southeast-2.amazonaws.com/hosteddataassets/musicblazer/manu-song-2.mp3",
      "cover_art_url": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT0hBNmQVoxqDWLdEKSZPnmbanHXKFMjzDrYA&usqp=CAU"
    },
    {
      "idx": 3,
      "date": "2023-01-16T00:00:00Z",
      "category": "Rock",
      "artist": "Emancipator",
      "album": "Soon It Will Be Cold Enough",
      "title": "Rock is best",
      "file": "https://itheum-static.s3.ap-southeast-2.amazonaws.com/hosteddataassets/musicblazer/manu-song-3.mp3",
      "cover_art_url": "https://coverartworks.com/wp-content/uploads/2021/05/yeter-750px.jpg"
    }
  ]
}

```
{% endcode %}

Here is a full sample file for you to inspect JSON content and HTTP response header:&#x20;

{% code fullWidth="true" %}
```json
https://itheum-static.s3.ap-southeast-2.amazonaws.com/hosteddataassets/musicblazer/stream_1.json
```
{% endcode %}

In the data format above, the most important items that need to be included are :

* General JSON file skeleton structure seen above needs to be maintained.
* The `data` key must exist as a first-level key and should have a list of data item objects.
* Each data item in the `data` list MUST have a `idx` , `date` and `file` field.
* `idx` can start with 0 or 1 depending on your choice. We prefer 1.
* `date` should be in the format "2023-01-16T00:00:00Z"
* The `file` should be a public Public URL that follows the standard [data-stream-url-rules.md](../../../integrators/data-streams-guides/data-stream-url-rules.md "mention")

\
When the Data Marshal sees the header as above, it will serve the contents of the file but it will filter out the `file` links to individual assets, but we will be able to programatically interact with the Data Marshal and fetch and stream these `file` links by using the `idx` index value.

Let’s now see how we can interact with the data marshal and get it to fetch and serve individual assets.



## Step 2: Installation of Itheum Data NFT SDK

In your NodeJS/JavaScript/TypeScript app, install the SDK `@itheum/sdk-mx-data-nft` by following the [instructions here](https://github.com/Itheum/sdk-mx-data-nft#usage-in-3rd-party-dapps). If you are using NPM then it would be.

```javascript
npm install --save @itheum/sdk-mx-data-nft
```



## Step 3:  Enable Native Auth Login via MultiversX SDK Core

This step was described in the guide section [#step-2-using-sdk-core-to-enable-multiversx-wallet-login-with-native-auth-enabled](guide-2-unlocking-data-nfts-via-multiversx-native-auth.md#step-2-using-sdk-core-to-enable-multiversx-wallet-login-with-native-auth-enabled "mention"), once you complete this you can come back to continue with the next steps.



## Step 4: Obtain a Auth "Session Token"

This step was also described in the guide section [#step-3-grab-a-native-auth-session-token](guide-2-unlocking-data-nfts-via-multiversx-native-auth.md#step-3-grab-a-native-auth-session-token "mention"), once you complete this you can come back to continue with the next steps.



## Step 5: "View Data" via a Native Auth session and handle the response

This step was also described in the guide section [#step-4-open-a-data-nft-and-view-data-via-a-native-auth-session](guide-2-unlocking-data-nfts-via-multiversx-native-auth.md#step-4-open-a-data-nft-and-view-data-via-a-native-auth-session "mention") and [#bonus-step-5-how-can-i-parse-non-json-data-streams](guide-2-unlocking-data-nfts-via-multiversx-native-auth.md#bonus-step-5-how-can-i-parse-non-json-data-streams "mention")once you complete these you can come back to continue with the next steps.

Please note that in addition to the code described above where you call `dataNftToOpen.viewDataViaMVXNativeAuth`, you may also want to use the `stream: true` setting to ensure the JSON version of the "base" data streams out and does not "auto-download" in your browser. See next step for a code example on using the `stream` param.



## Step 6: Working with the Nested Stream

If we followed all the steps as above, we now have access to the base version of the nested stream. If we print out the response from the previous, you will notice that you get the raw Data Stream contents, but as the Data Marshal has detected it to be a “nested stream”, it has extracted out and "hidden" all the `file` attributes from the `data` list. (Hint: compare the payload below with the original JSON document above to see the changes)

{% code fullWidth="true" %}
```json
{
  "data_stream": {
    "name": "tokentunes:musiverse:musicx",
    "creator": "Manu",
    "created_on": "2023-05-22T05:37:17Z",
    "last_modified_on": "2023-06-10T14:00:19Z",
    "marshalManifest": {
      "totalItems": 3,
      "nestedStream": true
    }
  },
  "data": [
    {
      "idx": 1,
      "date": "2023-01-02T00:00:00Z",
      "category": "Beats",
      "artist": "Emancipator",
      "album": "Soon It Will Be Cold Enough",
      "title": "Beats are best",      
      "cover_art_url": "https://521dimensions.com/img/open-source/amplitudejs/album-art/soon-it-will-be-cold-enough.jpg"
    },
    {
      "idx": 2,
      "date": "2023-01-09T00:00:00Z",
      "category": "Funk",
      "artist": "Emancipator",
      "album": "Soon It Will Be Cold Enough",
      "title": "Funk is best",      
      "cover_art_url": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT0hBNmQVoxqDWLdEKSZPnmbanHXKFMjzDrYA&usqp=CAU"
    },
    {
      "idx": 3,
      "date": "2023-01-16T00:00:00Z",
      "category": "Rock",
      "artist": "Emancipator",
      "album": "Soon It Will Be Cold Enough",
      "title": "Rock is best",      
      "cover_art_url": "https://coverartworks.com/wp-content/uploads/2021/05/yeter-750px.jpg"
    }
  ]
}

```
{% endcode %}

You can set up the UI with this “base” version as needed. In our case study, we can set a Music Player UI and load images, titles, etc.

And when a user selects a song and clicks on “play,” we can now interactively call the Data Marshal and “fetch” the nested `file` links.

For example, let’s assume the user wants to play **Beats are best** with `idx` “**1**”. Similar to the previous step where we "View Data", we now need to now call `viewDataWithNativeAuth` again, but we add the target `idx` of the link we want to stream as a new `nestedIdxToStream` param. Also, do not forget to use the `stream: true` setting to ensure the data streams out.

```javascript
const res: ViewDataReturnType = await dataNftToOpen.viewDataViaMVXNativeAuth({
  mvxNativeAuthOrigins: ["http://localhost:3000"],
  mvxNativeAuthMaxExpirySeconds: 3000,
  fwdHeaderMapLookup: {
    "authorization": `Bearer ${nativeAuthToken}`,
  },
  stream: true, // this ensure the data streams and "does not download"
  nestedIdxToStream: 1  // we want to stream the song "Beats are best" so we send it's "idx"
});
```

And that's it... using the above interactive coding method, we can iterate and interact with the "base" version of the Data Stream. by doing so, we can build a fully functional Audio Player app.



## Other Use Cases for Nested Streams

As you would have seen by now, nested streams enable unique flexibility to Data NFTs as they allow for some programmatic, interactive iteration of links placed within a "base" Data Stream file. There are many use cases for this that we can explore, for example:

1. Any use case that requires a "manifest" or "instruction" type "base" file that contains "URLs" to other assets:
   1. Audio Player
   2. Video Player
   3. Slideshows
   4. Live Streams etc
2. "Paginating" through large datasets

We'd love to see what you can build with nested streams...
