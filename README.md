![3Box Logo](./3Box_widelogo.png)

# 3Box
![Twitter Follow](https://img.shields.io/twitter/follow/3boxdb.svg?style=social&label=Follow)

3Box is a distributed user data network that supports public and private data for Ethereum users. All data is publicly available, but private data can only be decrypted by dapps that the user has given explicit permission. We provide a [social profiles dapp](https://3box.io) and a web3 [developer API](https://github.com/3box/3box-js) that makes it easy to onboard users and set/get data from their profile.


[![button](./3box_button_community.png)](https://discord.gg/dxjM74J)



## Getting Started
### Dapp Users
👤 Create or sign in to your web3 social profile at [3box.io](https://3box.io)

### Dapp Developers
👩‍💻 Explore [`3box-js`](https://www.github.com/3box/3box-js) to integrate with 3Box

### 3Box Community  

💬 Join [3Box Community Discord](https://discord.gg/Z3f3Cxy) to chat with the core team and developer community

📬 Sign up to [receive our newsletter](https://mailchi.mp/c671ca2b8093/3box)

🛠 Want to contribute to the project? View our [contributors guide](./CONTRIBUTING.md)

➡️ Have you integrated 3Box? [Add your project to 3Box Dapp Universe](./COMMUNITY-PROJECTS.md)


# System Overview
The 3Box system primarily consists of a dapp and data network.

## 3Box User Data Network
The 3Box data network consists of a few main components: 
* [`3box-js`](https://www.github.com/3box/3box-js) is a client-side JavaScript library that allows applications to integrate with the 3Box network

* [`3box-pinning-server`](https://www.github.com/3box/3box-pinning-server) is a service that pins user data on the IPFS network to ensure availability

* [`3box-address-server`](https://www.github.com/3box/3box-address-server) is a service that maps an Ethereum address to its decentralized identifier (DID) to which data is addressed 

Together these components are used to keep track of user data stored in [`orbit-db`](https://github.com/orbitdb/orbit-db) instances. Learn more about the [3Box architecture and how we do access control with encryption](./ARCHITECTURE.md).

### 3Box JS
[`3box-js`](https://www.github.com/3box/3box-js) is the client side library used to read, write, and delete public and private data associated with the user. This library is used to get profile information about an address.

We assume that end users have a web3-compatible browser or wallet (such as MetaMask or Status) which supports personal_sign.

### 3Box Address Server
[`3box-address-server`](https://www.github.com/3box/3box-address-server) is a server utilizing a REST-API that is used to associate an Ethereum address with its latest 3Box address. This is what must be looked up to sync the user's data.    

## 3Box Dapp
The [3box.io](https://3box.io) dapp is how users manage their 3Box data, including profile information and other.

### Web App
[`3box-dapp`](https://www.github.com/3box/3box-dapp) is a [web interface](https://3box.io/) that allows users to interact with 3Box.

### Activity Feed
[`3box-activity`](https://www.github.com/3box/3box-activity) is an API that makes it easy to construct activity feeds for Ethereum users. Part of Ethereum Profiles on the 3Box web app.

## Project Goals
* Make it easy for users to share information publicly, while preserving privacy when desired
* Improve the onboarding experience for decentralized applications by making it easy for developers to get information about Ethereum users
* Improve Ethereum usability with distributed database infrastructure that works in production today
* Provide a decentralized system, but pragmatically utilize centralized components to facilitate the transition

## Other Resources
* Here's a [list of proposed improvements](./IMPROVEMENTS.md)
* Here's a [GDrive with other documents](https://drive.google.com/drive/folders/16lZWMVFLKLk2nAZJQ7xQyzHKZzK734Ov?usp=sharing)

