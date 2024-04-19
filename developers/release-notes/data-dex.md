# Data DEX

## V1.14

**Main Features / Changes**

* Upgraded the "Get Whitelisted" page to "Get Verified," reflecting changes in verification processes and improving clarity for users.
* Implemented NFT pagination for the bonding admin dashboard, enabling easier navigation and management of bonding with Data NFTs.
* Introduced support for extra assets and viewing of extra media assets, expanding the range of supported content types.
* Added support for DataNFT PH (Placeholder) functionality, improving compatibility and interoperability across platforms.
* Added "Get Bitz Ready-to-Play" animation and dropdown, providing users with engaging visual elements and easy access to Bitz features.
* Implemented enhanced bonding UI and upgraded smart contracts for improved functionality and within the Data Dex.

***

## V1.13

**Main Features / Changes**

* Implemented IPNS (InterPlanetary Name System) support, enabling creators to enter IPNS for their data NFTs.
* Introduced "Get Bitz - XP System" Data NFT, offering a gamified experience for users.
* Activated the bonding feature on production, allowing creators to bond ITHEUM to their data NFTs for added functionality.

***

## V1.12

**Main Features / Changes**

* Improved validation in the minting form for better user experience.
* Enhanced mobile view in the marketplace for smoother navigation.
* Added a disclaimer when listing items below the floor price to inform users effectively.
* Bonding functionality was introduced on devnet for testing purposes.

***

## V1.11

**Main Features / Changes**

* Further improvements in UI/UX stability ensure a seamless browsing experience on the Data Dex platform.
* Now featuring grouped collection URL easy sharing, making it simple to share collections.
* Stay informed with quick access to our status page link, providing real-time updates on platform.

***

## V1.10

**Main Features / Changes**

* **Itheum Enterprise:** Unlock the power of data with launching and moderating data NFT collections, now available for enterprise users. Enterprise users can now curate their data NFTS; Freeze/Wipe Data NFTs.
* **Favorite NFTs Function:** Easily mark favorite data NFTs for quick access and tracking.
* **Marketplace View Grouped Collection:** Collections are now conveniently grouped in the marketplace view, providing a more organized browsing experience.
* **Misc. Performance & Code Base Improvements:** Fine-tuning Data Dex for optimal performance and reliability.

***

## V1.9

**Main Features / Changes**

* **Revamped UI/UX:** Experience the all-new Itheum Enterprise UI with a fresh design and enhanced dashboard functionalities, including the ability to claim royalties.
* **NFT Transaction Details:** Enjoy improved functionality as the NFT Details transactions table now works seamlessly, with or without web2 server availability.
* **Mobile Responsiveness:** Data Dex is now more responsive on mobile devices, providing an optimized user experience on the go.
* **xAlias (Google) Login:** Easily log in using your Google account, enhancing accessibility and convenience.
* **"View Data" Tips:** Get helpful reminders that "view data" is disabled when logged in through the xPortal hub, ensuring a smoother experience.
* **Cookie Acceptance:** A new cookie acceptance module has been implemented to enhance user interactions.
* **Miscellaneous Enhancements:** Various improvements, including route privacy reassessment, artifact cleanup, app icon review, NFT minting refinements, and library updates, have been made for an overall better experience.

***

## V1.8

**Main Features / Changes**

* **Alpha Release of Itheum Enterprise UI:** Introduces the ability to deploy minter contracts and create Data NFT collections directly through a user interface, leveraging the SDK.
* **Transition to New Devnet:** Successful switch to an updated development network for enhanced performance and stability.
* **Login Versioning for Data Dex and Explorer:** Implemented version control for logins. Users accessing with an outdated version are automatically logged out, addressing the issue of repeated refreshes.
* **General Improvements:** Minor bug fixes and user experience enhancements have been applied across the platform.
* **Optimized Interaction Table on NFT Details Page:** Enhanced performance and added support for various marketplaces.
* **Data Stream Live check Update:** Modified to better support specific requirements of private networks.

***

## V1.6

**Main Features / Changes**

* Users will no longer inadvertently land on the Devnet. This clear segregation ensures a smooth user experience.
* Clicking "Explore" on a Data NFT now seamlessly redirects users to the Itheum Explorer, with automatic login for added convenience.

***

## V1.5

**Main Features / Changes**

* Integration with Native Auth via the Data Marshal on Data DEX. Users can now use the "View data" feature without the sign message workflow, enhancing the overall UX of the platform.

***

## V1.4

**Main Features / Changes**

* Early preview release of "Data Creator' profile pages. Click on any address in the Data DEX and discover more activity about the Data Creator or Data Owner.
* Logged in user can also see their "Profile Page".
* Significant speed updates on interactions like list, marketplace paging, price updates, delist etc. Achieved via an asynchronous api layer that sits between the DApp and Blockchain.
* Significant performance updates by remove React Context based chainMeta method. This will allow for less complex releases in future.
* Major redesign of the Data NFT Creator onboarding whitelist page.
* Added an explore button for the multiversX infographics app.
* New UI design and style updates, new default fonts etc
* Redesigned the horizontal scroll bar in the marketplace and wallet to be more user-friendly on mobile.
* On devnet - made the PlayStation test app onboarding form adaptive to various screen sizes.
* Adjusted the routing so that /markeplace/my now redirects to /marketplace.
* Updated the ChakraUI library.
* Fixed miscellaneous wab wallet UX issues when signing messages and opening files or conducing various web3 actions.



**Bug Fixing**

* Fixed UI issues on the details page of NFTs (curved edges overlapping sharp edges, space between copy button and price, showing "nothing here" even if there are offers, offers not aligned properly).
* Resolved the issue on the details page of NFTs where 0 offers were still showing "nothing here."
* Rectified the problem where manually refreshing was required to update the price.
* Fixed the profile page to show the correct listed data count.
* Corrected the issue in the Web Wallet where updating the price of a listed data NFT and signing the transaction redirected to the wrong tab.
* Addressed visual bugs (ensured Modals have the same color, improved Modal badges, ensured changing from marketplace data NFTs to listed data NFTs keeps the marketplace button disabled, improved appearance of the table age field).
* Fixed the guardRails page on the historic component to make back and forward buttons work.
* Made the xPortal modal responsive in light mode.
* Fixed the /settings page not loading.
* Resolved the issue where accessing a bad URL offer displayed a message for the user to be aware that the link is wrong or no longer available.
* Fixed the Details page to be aware of the environment variable for buy limitation.
* Corrected the View Data sign message prompt from transaction to message and added detection for ledger or xPortal.
* Fixed the Web Wallet signature on View Data when the button is clicked 2 or more times.
* Fixed the issue where Recent Data NFTs were not showing on the production build.
* Addressed the problem of devnet multiversX explorer being invoked from mainnet in a marketplace item.
* Fixed the disabled preview data button when the user is not logged in.



***

## V1.3

**Main Features / Changes**

* xPortal hub support
* Added the "explore" button for DATA-NFT's for the 1-click discovery of supported data visualizer apps on "Itheum Explorer"
* Show the "other offers" section on the details page
* Data DEX Web2 API is used to improve UX (like showing ordered other offers), but Data DEX gracefully falls back to full web3 mode if Web2 API is unavailable
* Make demo apps like Playstation passport / Strava etc. to be unavailable in mainnet until integration is complete
* Created an animation on hover DATA NFT to hint that clicking on it opens the details model view
* Changed DATA NFT detail drawer into a modal
* Changed the Terms of use and also added a feature that will alert the user to any changes to terms of use
* Redirect a non-logged-in user to the same offer page they were viewing after they connected their wallet
* Changed the confirm ledger modal to be more appealing
* Added a button for accessing the Canary Dashboard from mobile too

**Bug Fixing**

* Fixing burning and listing action to appear in the activity tab inside Wallet
* Fixed the problem of routes accessible without being logged in
* Fixed the item count inside the Marketplace tabs
* Fixed when trying to connect with web wallet and cancel redirect to /abort route
* Fixed on DATA-NFT details page didn’t show offers on every link even /tokenIdentifier and /tokerIdentifier/offer-\[number]
* Fixed the Recent Claim Transaction and Recent Data NFT Interaction pages to show a message to the user if no data appears
* Fixed DATA NFT details page to show a message to the user if no other offers are present
* Fixed on DATA NFT details page offers section to be mobile friendly
* Fixed whitelisted addresses to show correctly inside the Canary Dashboard page
* Fixed the marketplace Paused overlay to be full height
* Fixed the UI bug inside my listed data page that wouldn’t update the price of a DATA-NFT in real time when the user edited it
