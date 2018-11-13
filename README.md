# 3Box
![Twitter Follow](https://img.shields.io/twitter/follow/3boxdb.svg?style=social&label=Follow)

3Box is a distributed database that supports public and private data for Ethereum users. All data is publicly available, but private data can only be decrypted by dapps that the user has given explicit permission. *This project is under active development.*

![3Box Logo](./3Box_widelogo.png)



[![button](./3box_button_community.png)](https://discord.gg/Z3f3Cxy)



## Getting Started
### New Users
👤 Create an Ethereum Profile at [3box.io](https://alpha.3box.io)

### Dapp Developers
👩‍💻 Want to integrate with 3Box? [Explore `3box-js`](https://www.github.com/uport-project/3box-js)

### 3Box Community  

💬 Want to chat with our community or ask questions? [Join 3Box Community HQ](https://discord.gg/Z3f3Cxy)

📬 Want to receive the 3Box newsletter? [Sign up here](https://mailchi.mp/c671ca2b8093/3box)

➡️ Have you integrated 3Box? [Add your dapp to 3Box Dapp Universe!](./COMMUNITY-PROJECTS.md)

📝 Want to reach out about a potential integration? [Complete this form!](https://airtable.com/shrDYkQCnzlVUvHGe)

🛠 Want to collaborate on code? [View the Guide to Contributing](./CONTRIBUTING.md)

## Goals
* Make it easy for users to share information publicly, while preserving privacy when desired
* Improve the onboarding experience for decentralized applications by making it easy for developers to get information about Ethereum users
* Improve Ethereum usability with distributed database infrastructure that works in production today
* Provide a decentralized system, but pragmatically utilize centralized components to facilitate the transition

## 3Box DB
3Box DB consists of two components: [`3box-js`](https://www.github.com/uport-project/3box-js) which is a client library, and [`3box-address-server`](https://www.github.com/uport-project/3box-address-server) which is a server. Together they are used to keep track of user data stored in [`orbit-db`](https://github.com/orbitdb/orbit-db) instances. Learn more about the [3Box architecture and how we do access control with encryption](./ARCHITECTURE.md).

### 3Box JS
[`3box-js`](https://www.github.com/uport-project/3box-js) is the client side library used to read, write, and delete public and private data associated with the user. This library is used to get profile information about an address.

We assume that end users have a web3-compatible browser or wallet (such as MetaMask or Status) which supports personal_sign.

### 3Box Address Server
[`3box-address-server`](https://www.github.com/uport-project/3box-address-server) is a server utilizing a REST-API that is used to associate an Ethereum address with its latest 3Box address. This is what must be looked up to sync the user's data.    

## 3Box Dapp
The 3Box dapp is how users manage their 3Box data, including profile information and other. Coming soon to 3box.io.

### Web App
[`3box-dapp`](https://www.github.com/uport-project/3box-dapp) is a [web interface](https://alpha.3box.io/) that allows users to interact with 3Box.
    

### Activity Feed
[`3box-activity`](https://www.github.com/uport-project/3box-activity) is an API that makes it easy to construct activity feeds for Ethereum users. Part of Ethereum Profiles on the 3Box web app.

## Other Resources
* Here's a [list of proposed improvements](./IMPROVEMENTS.md)
* Here's a [GDrive with other documents](https://drive.google.com/drive/folders/16lZWMVFLKLk2nAZJQ7xQyzHKZzK734Ov?usp=sharing)

