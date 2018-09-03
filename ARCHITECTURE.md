# 3Box Architecture
## Diagram

![3Box Architecture Diagram](./3box_architecture_diagram.png)

### User Model
Each user has their own root ipfs object, and associated public and private data stores. 

The hash of this object is stored in the `3box-hash-server`. The hash-server also stores a mapping from a DID that is created in the `3box-js` library to this hash, as well as a mapping between the users ethereum address to the DID.

### How it Works (Technically)
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

