# 3Box
3Box is a distributed database that supports public and private data for Ethereum users. All data is publicly available, but private data can only be decrypted by dapps that the user has given explicit permission.

## Quick Links

### For Ethereum Users (Coming Soon)
👤 Create an Ethereum Profile at 3box.io.

### For Ethereum Dapp Developers (Coming soon)
👩‍💻 Want to integrate 3Box data? [Explore 3box-js](https://www.github.com/uport-project/3box-js)

### For Our Community
👍 Want to collaborate on code? Submit an issue or a PR!  

🐱 Want to chat with our community or ask questions? [Join our chat!](https://chat.uport.me/#/room/#3box:chat.uport.me)

➡️ Have you integrated 3Box? [Add yourself to our Dapp Universe!](./COMMUNITY-PROJECTS.md)

## Goals
* Make it easy for users to share information publicly, while preserving privacy when desired
* Improve the onboarding experience for decentralized applications by making it easy for developers to get information about Ethereum users
* Improve Ethereum usability with distributed database infrastructure that works in production today

## Components
3box consists of two major components `3box-hash-server` which is a server component and `3box-js` which is a client side library. Together they are used to keep track of user data stored in [`orbit-db`](https://github.com/orbitdb/orbit-db) instances.

### 3box-js (3Box Client)
3box-js is the client side library used to read, write, and delete public and private data associated with the user.

[*3box-js data structure specification*](./3BOX-JS-DATA-STRUCTURE.md)

[*3box-js api specification*](./3BOX-JS-API.md)


##### Requirements
We assume that end users have a web3-compatible browser or wallet (such as MetaMask or Status) which supports eth_sign or personal_sign.

### 3box-hash-server (3Box Server)
The Hash Server is a server utilizing a REST-API that is used to associate an Ethereum address with its latest 3Box Hash. This is what must be looked up to locate the user's data.

[*3box-hash-server specification*](./3BOX-HASH-SERVER.md)

### 3box-dapp (3Box Dapp)(Coming Soon)
The 3box-dapp is how users manage their 3Box data, including profile information and other. Coming soon to 3box.io.

## Architecture
A high level overview of the 3box architecture, followed by a brief description.

![3Box Architecture Diagram](./3box_architecture_diagram.png)


Each user has their own root ipfs object, and associated public and private data stores. The hash of this object is stored in the `3box-hash-server`. The hash-server also stores a mapping from a DID that is created in the `3box-js` library to this hash, as well as a mapping between the users ethereum address to the DID.


**A.** The dapp gets the users address from MetaMask (or any web3 compliant browser)

**B.** Dapp request public or private data from the users 3box

**C.** 3box-js MM interactions
  1. 3box-js requests consent for storing and retrieving private and public data. The signature is used as key material when creating the 3box DID.
  2. 3box-js requests consent for linking the public profile to the users ethereum address

**D.** 3box-js stores and retrieves data from ipfs. Using two separate orbit-db instances for public and private data, and a separate ipfs objects which always links to the latest hash of the two orbit-db instances.

**E.** All ipfs data is automatically pinned in the infura ipfs cloud.

**F.** 3box-js hash-server interactions
  1. 3box-js publishes the link between ethereum address and DID
  2. 3box-js publishes a new root hash (this is the hash of the latest ipfs object linking to the two orbit-db instances)


[3box documents folder](https://drive.google.com/drive/folders/16lZWMVFLKLk2nAZJQ7xQyzHKZzK734Ov?usp=sharing)

