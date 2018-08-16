# 3Box
User-Managed Application Data for Web3.

[3box documents folder](https://drive.google.com/drive/folders/16lZWMVFLKLk2nAZJQ7xQyzHKZzK734Ov?usp=sharing)

## Technical specification
3box consists of two major components `3box-root-hash-tracker` which is a server component and `3box-js` which is a client side library. Together they are used to keep track of user data stored in `orbit-db` instances. Below are detailed specifications of how they are implemented.

### 3box-root-hash-tracker
The root hash tracker is a REST-API that is used to associate an ethereum address with an ipfs hash.

[*3box-root-hash-tracker specification*](./3BOX-ROOT-HASH-TRACKER.md)

### 3box-js
3box-js is the client side library used to read, write, and delete public and private data associated with the user.

[*3box-js data structure specification*](./3BOX-JS-DATA-STRUCTURE.md)

[*3box-js api specification*](./3BOX-JS-API.md)
