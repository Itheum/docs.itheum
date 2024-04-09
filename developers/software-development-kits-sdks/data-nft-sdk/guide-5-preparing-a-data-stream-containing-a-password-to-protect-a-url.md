# Guide 5: Preparing a Data Stream containing a password to protect a URL

This guide walks you through how to use Data Streams configured to expose an otherwise publicly available URL that is protected through a password that you can expose through a Data NFT.

Let's begin...

***

## Step 1: Create the file that you want to set as your initial Data Stream

Here is a full sample file for you to inspect the JSON file you have to create:

{% code fullWidth="true" %}
```json
{
  "data_stream": {
    "category": "Video Game",
    "name": "BoberRunV2",
    "creator": "Sylla",
    "created_on": "2024-04-03",
    "last_modified_on": "2024-04-03",
    "host": "https://myhost.com/gamelink",
    "token_query_param": "password",
    "token": "myPassword"
  }
}
```
{% endcode %}



In the data format above, here's what everything means :

* The general JSON file skeleton structure seen above needs to be maintained.
* `category` represents the type of data that should be expected from your link
* `name`represents the name you want to give to your project
* `creator` should be your name in order to be able to take credits for your work
* `created_on` and `last_modified_on` should respect the above shown date format. The first one should be the date when you initially created the data stream and the other one should be updated whenever you update your data stream
* `host` should be the URL where your data resides that is protected by a password
* `token_query_param` is an optional field that hints to other developers that they should include your password after the query param that this key has as value.
* `token`  should represent the password that you want the users having the Data NFT to use

By creating the JSON file like this you are preparing it to be fetched by people that want to view data inside of your Data NFT and use it (even programatically if needed)



## Step 2: Hosting the file on Zedge Storage

You can host your file wherever you want that suits the Data Stream URL rules, but hosting it on [Zedge Storage](https://www.zedgestorage.com/) is one of the easiest ways

1. First login using your MultiversX wallet
2. Click on "My Data Bunker" in the header of the app
3. Click on "Create New Data Asset"
4. Choose "Dynamic Data Storage" and click "Next"
5. Choose "Uplaod my files" and click "Next"
6. Choose "Decentralized / Web3 Storage" and click "Next"
7. Choose "IPNS + IPFS" and click "Next"
8. Make sure the "Nested Stream" option is checked and upload your JSON
9. Choose a name and a creator for the given dataset
10. Click "Upload Data" and wait for the files to be uploaded
11. Copy "Your Asset's IPNS location" to your clipboard and use that as a URL to mint your Data NFT link any other normal link. As a note on this step, you can also open the link to your asset via the link provided inside Zedge Storage. You can see that the app created a manifest file which sends users to your actual file. This is important in the interaction with the Data Marshal, which powers the privacy of Data NFTs
12. Use the IPNS location (e.g. ipns://k51qzi... ) you copied to your clipboard to mint a Data NFT. When inputing that as a Data Stream in the Data Dex make sure to also add this at the end of the URL:

    `?dmf-nestedstream=1`&#x20;

Your IPNS should look like this at the end:

`ipns://hash?dmf-nestedstream=1`

13. Just mint it! If you use this, anyone owning the NFT will be able to use the Nested Stream View Data feature in order to access your game.

That's all! Using the above method will help you mint a Data NFT with an updatable, file that contains the password to your password-protected URL. You can always go to Zedge Storage to upload a new file under the IPNS hash you have created. IPNS is just like IPFS, but muttable (a bit more complicated than that, but that's for another tutorial/guide)
