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

# Goals
* Make it easy for users to share information publicly, while preserving privacy when desired
* Improve the onboarding experience for decentralized applications by making it easy for developers to get information about Ethereum users
* Improve Ethereum usability with distributed database infrastructure that works in production today

# Components
3box consists of two major components `3box-root-hash-tracker` which is a server component and `3box-js` which is a client side library. Together they are used to keep track of user data stored in [`orbit-db`](https://github.com/orbitdb/orbit-db) instances.

### 3box-js (3Box Client)
3box-js is the client side library used to read, write, and delete public and private data associated with the user.

[*3box-js data structure specification*](./3BOX-JS-DATA-STRUCTURE.md)

[*3box-js api specification*](./3BOX-JS-API.md)

### 3box-root-hash-tracker (3Box Server)
The root hash tracker is a server utilizing a REST-API that is used to associate an Ethereum address with its latest IPFS Root Hash. This is what must be looked up to locate the user's data.

[*3box-root-hash-tracker specification*](./3BOX-ROOT-HASH-TRACKER.md)

# Requirements
* We assume that end users have a web3-compatible browser or wallet (such as MetaMask or Status) which supports eth_sign or personal_sign.


[3box documents folder](https://drive.google.com/drive/folders/16lZWMVFLKLk2nAZJQ7xQyzHKZzK734Ov?usp=sharing)
