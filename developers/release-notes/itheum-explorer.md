# Itheum Explorer

## V1.12

**Main Features / Changes**

* Various user interface improvements to enhance usability.
* Introduced the Time Capsule Widget.

***

## V1.11

**Main Features / Changes**

* Introducing the new NF-Tunes landing page, offering an immersive experience for exploring the world of NFT music.
* Enhancements in UI/UX stability for a smoother and more intuitive browsing experience.
* Introducing the time capsule data widget, allowing users to dive into historical data with ease.
* Quick access to our status page link for instant updates on platform.

***

## V1.10

**Main Features / Changes**

* **Misc. Performance & Code Base Improvements:** Fine-tuning Itheum Explorer for optimal performance and reliability.

***

## V1.9

**Main Features / Changes**

* **Integrated xPortal Hub:** Explorer now seamlessly integrates with the xPortal Hub, offering comprehensive view data functionality.
* **xAlias (Google) Login:** Conveniently log in using your Google account to enhance accessibility.
* **Lightweight Redesign:** Bootstrap and other libraries have been removed to create a more lightweight and efficient Explorer.
* **Improved Readability:** Enjoy improved readability, especially in light mode when using Ledger.
* **Bug Fixes:** Issues related to viewing data in the wallet after opening multiple NFTs in a row have been resolved.
* **Miscellaneous Enhancements:** Code cleanup, library updates, and other improvements have been implemented for a smoother Explorer experience.

***

## V1.8

**Main Features / Changes**

* **Integration with xPortal Hub:** New feature to view data directly in Explorer, enhancing data accessibility.
* **Autoplay Feature in NF-Tunes App:** Autoplay functionality has been implemented, offering a more seamless audio experience.
* **Continuous Improvements:** Ongoing minor bug fixes and user experience enhancements.

***

## V1.6

**Main Features / Changes**

* Dark mode refined with visual updates,  for a more immersive experience.
* Modal behavior has been fine-tuned, optimizing user interactions and navigation.
* MP3 app implemented in Explorer, based on nested streams.&#x20;

***

## V1.5

**Main Features / Changes**

* Support for NativeAuth login in the Explorer DApp. Users who are already logged can seamlessly access the Explorer DApp and "View Data" without having to re-sign transactions. This enhancement streamlines the user experience.
* Enhanced zooming mechanism for Bubbles app. Users can better pan and zoom on the Multiversx-bubbles app.

***

## V1.4

**Main Features / Changes**

* Added support for Multi-Page PDF documents in Explorer and launched the MultiversX Infographics custom app on the App Marketplace.
* Added enhanced support for the MultiversX Bubble App UX.
* Changed button text for Trailblazer modal from "Open Dialog" to "Launch Quest."
* Completely redesigned the app appearance.
* Deprecate bootstrap and added Tailwind as the styling library.
* Added balance and total supply to wallet cards.
* Updated mx libraries.
* Introduced security checks for "filter" issues in the wallet (for JSON, SVG) to inform users and provide advice for the next steps.
* Implemented signMessage using the correct approach as useSignMessage.
* Made MultiversX Bubble SVG links open in the same window.
* Added a message on the wallet page for View Data when using the Web Wallet since it's not supported yet.
* Provided a message to alert the user when opening a PDF in a new window.
* Enabled support for viewing SVGs as MultiversX Bubbles in a new tab.
* Fixed miscellaneous wab wallet UX issues when signing messages and opening files or conducing various web3 actions.



**Bug Fixing**

* Tweaked the Trailblazer view (changed title from "Itheum Trailblazer" to simply "Trailblazer," adjusted time to display the actual time instead of 00:00:00 GMT).
* Fixed an SDK error in the Explorer where creating data NFTs from the API wasn't displaying data.
* Rectified the issue on the View Data of items in the Wallet where Data NFT content wasn't rendering properly, and the Web Wallet wasn't working in the Explorer Wallet.
* Fixed the second modal on the View Data which was appearing at the bottom of the page during testing.
* Corrected the appearance of the login button to be displayed as an actual button in the navbar.
* Ensured that Listed Offers Cards have the same information as the marketplace.
* Renamed the login button from "Browser Wallet" to "DeFi Wallet."
* Resolved the Web Wallet signature failure when trying to view data 2 or more times.
* Fixed the issue of viewing a PDF from the wallet redirecting to a new tab.
* Corrected the problem where opening a PDF using Web Wallet redirected to an invalid page before signing the transaction.
* Addressed the design break when switching from dark to light mode.

***

## V1.3

**Main Feature / Changes**

* Trailblazer App: Added the web viewer for quest forms.
* Added mp3 file player support.
* Added a message to notify user to sign data from a Ledger or xPortal.
* Added detection for SVG file to be rendered as SVG so it can be interactive.

**Bug Fixing**

* Fixed the showing of supply 0 even if it’s not the case
* Fixed misc issues on My Listed and My Wallet pages to reflect accurate data from on-chain lookup

\
