![3Box Logo](./images/3Box_widelogo.png)

# 3Box
[![Twitter Follow](https://img.shields.io/twitter/follow/3boxdb.svg?style=for-the-badge&label=Twitter)](https://twitter.com/3boxdb)
[![Discord](https://img.shields.io/discord/484729862368526356.svg?style=for-the-badge)](https://discordapp.com/invite/Z3f3Cxy)


3Box is a distributed user data network that supports public and private data for Ethereum users. All data is publicly available, but private data can only be decrypted by dapps that the user has given explicit permission. We provide a [social profiles dapp](https://3box.io) that allows users to create and manage their profile and a web3 [developer API](https://github.com/3box/3box-js) that makes it easy to onboard users, set/get data from their general profile and other application-specific datastores, and support decentralized comments and other messaging in their app.

<br>

[![button](./images/3box_button_community.png)](https://discord.gg/dxjM74J)

<br>

## Getting Started

### Users
👤 Create or sign in to your web3 social profile at [3box.io](https://3box.io)

### Developers
👩‍💻 Explore [`3box-js`](https://www.github.com/3box/3box-js) to integrate decentralized **Profiles**, **Storage**, or **Messaging/Comments** to your application

### Community

💬 Join [3Box Community Discord](https://discord.gg/Z3f3Cxy) to chat with the core team and developer community

📬 Sign up to [receive our newsletter](https://mailchi.mp/c671ca2b8093/3box)

🛠 Want to contribute to the project? View our [contributors guide](./CONTRIBUTING.md)

➡️ Have you integrated 3Box? [Add your project to 3Box Dapp Universe](./community/projects.md)

📜 Want to propose an improvement? [Create a 3IP](./3IPs/3ip-0.md)

<br>

# 3Box Overview
The 3Box user data storage network primarily consists of three main components:
* [3Box.js API](https://github.com/3box/3box-js): developer interface for setting/getting data
* Data pinning network: distributed network for pinning data on OrbitDB/IPFS
* [Profiles App](https://3box.io): user interface for managing profiles and data

## Developer Tools

### 3Box.js
[`3box-js`](https://www.github.com/3box/3box-js) is a client-side JavaScript library and API that allows applications to integrate with the full functionality of the 3Box data network. The 3Box.js API allows developers to read, write, and delete public and private data associated with the user. This library can be used to get profile information about an address, set profile information about an address, and onboard users. The 3Box.js API features the ability for users to encrypt their data, and allows applications to store data in an app-specific storage location, called a Space, and in peer-to-peer message feeds, called Threads. The 3Box.js API also features a GraphQL endpoint.

#### Profiles API
The Profiles API is a developer interface for creating and interacting with a user's profile, including getting, setting, and removing data. 3Box Profiles are great for storing and accessing general profile information such as name and image, basic affiliations, basic reputation, and other bits of information that you desire to easily share across all apps that a user accesses with 3Box. Public profile information is made available for all to read via the getProfile() method, while encrypted profile information is available only after the user signs a general consent message, which happens every time when logging in.

#### Spaces API
The Spaces API is a developer interface for creating and interacting with appliation-specific datastores inside of a user's 3Box, including getting, setting, and removing data. 3Box Spaces are great for storing and accessing specific, more sensitive information such as app settings and defaults, app-specific content, sensitive information, and other bits of data that developers desire to protect to a greater degree than if it were stored in the general profile where it would be available to all apps. Data within Spaces can still be shared between applications however. Public spaces information is made available for all to read via the getSpace() method, while encrypted spaces information is available only after the user signs a space consent message. Spaces must be explicitly requested by the developer and are not accessed by default upon logging in. This helps protect users' information privacy.

#### Threads API
The Threads API is a developer interface for creating and interacting with decentralized messaging threads, including creating a thread, posting in a thread, and getting posts in a thread. 3Box Threads are great for storing peer-to-peer messages in a log/feed format between one or multiple users. Use cases for threads include commenting systems, group and direct messaging systems, content-based social media functionalities, and storing lists of items. The current version of the Threads API is still experimental and does not support private (encrypted) threads or moderation.

### 3Box GraphQL API
[`3box-graphql`](https://github.com/3box/3box-js-graphql) is a GraphQL endpoint that allows developers to write more efficient 3Box.js getProfile() queries. Now developers can ask our API for specific common user profile fields instead of needing to return the entire profile. For example, this is useful when querying for name and image for hundreds or thousands of profiles at once.

Useful for: 
* efficiently getting common information from a user's public profile

### 3Box Profile Hovers
[`profile-hover`](https://github.com/3box/profile-hover) is the easiest way to replace hexadecimal addresses in your app's UI with 3Box profile information. Profile hover is a simple JavaScript plugin that allows applications to easily get profile data for ethereum users from the 3Box network, in order to populate their application with social profile information displayed in a hover overlay. Profile hovers are fully configurable, and integration requires only 2 lines of code. Hovers are especially great as a social overlay for leaderboard-type and discover-based social apps that display many user addresses on screen at once.

Useful for:
* easily replacing hexadecimal addresses in your app's UI with social profile data

## 3Box Data Network

### 3Box Data Network
The 3Box user data network consists of a few core components: a data [pinning server](https://www.github.com/3box/3box-pinning-server), an [address server](https://www.github.com/3box/3box-address-server), and an [identity model](https://github.com/3box/muport-core-js). Together these components are used to keep track of user data stored in [`orbit-db`](https://github.com/orbitdb/orbit-db) instances on IPFS. 

We assume that end-users have a web3-compatible browser or wallet (such as MetaMask or Status) which supports personal_sign. This is how users authenticate dapps to their 3Box. Learn more about the [3Box architecture and how we do access control with encryption](./ARCHITECTURE.md).

### 3Box Pinning Server
[`3box-pinning-server`](https://www.github.com/3box/3box-pinning-server) is a service operated by 3Box that pins 3Box user data on the IPFS network to ensure availability. Optionally, others can also run their own instance of the pinning-server to replicate the user data stored in the 3box network. In the future, this service will become more decentralized with a network of pinning nodes, allowing others to run their own node and host their own data if desired. 

### 3Box Address Server
[`3box-address-server`](https://www.github.com/3box/3box-address-server) is a server utilizing a REST API that is used to associate an Ethereum address with its 3Box DID (decentralized identifier), to which all user data is addressed. This is what must be looked up to retrieve and sync the user's data. In the future, we want to integrate the address -> DID mapping into the pinning node network, which will further decentralize our network.

### 3Box Identity
[`muport-core-js`](https://github.com/3box/muport-core-js) is a library that lets us associate a users 3Box and data with a lightweight muport DID (decentralized identity) rather than directly to an Ethereum address. This abstraction allows our system to interoperate with other decentralized identity providers and the DIF (Decentralized Identity Foundation) DID spec. DIDs allow multiple Ethereum addresses to be associated with the same 3Box, and allow for other security and usability features such as address rotation that allows users to change their Ethereum address without losing all of their data.

## User Tools

### 3Box Profiles Application
The [3box.io](https://3box.io) app is how users manage their 3Box data, including profile information, public activity, collectibles, and more.

#### Web App
[`3box-dapp`](https://www.github.com/3box/3box-dapp) is a [web interface](https://3box.io/) that allows users to interact with their 3Box profile. The 3Box app works with all standard desktop and mobile web3 browsers including MetaMask, Status, Coinbase Wallet, and others.

#### Activity Feed
[`3box-activity`](https://www.github.com/3box/3box-activity) is an API that makes it easy to construct activity feeds for Ethereum users. Part of Ethereum Profiles on the 3Box web app.

#### 3Box Verifications
[`3box-verifications`](https://github.com/3box/3box-verifications) is a service that allows [3box.io](https://3box.io) users to verify their email address, as well as their Github and Twitter social accounts and link them to their 3Box profile. The verifications issued by this service are DID-compatible verifiable claims in the form of JWTs.

### Service Endpoints
There is an overview of all 3box service endpoints [here](./devops/service-endpoints.md)

<br>

# Project Goals
* Make it easy for users to share information publicly, while preserving privacy when desired
* Improve the onboarding experience for decentralized applications by making it easy for developers to get information about Ethereum users
* Improve Ethereum usability with distributed database infrastructure that works in production today
* Provide a decentralized system, but pragmatically utilize centralized components to facilitate the transition

