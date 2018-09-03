# 3Box Architecture
## Data Model
Each user has their own root IPFS object, and associated public and private data stores. As long as the user has access to the hash of the root object, called the 3Box Hash, it can retrieve the entire data store from the IPFS network.

The hash of this object is stored in the `3box-hash-server`. The hash-server also stores a mapping from a DID that is created in the `3box-js` library to this hash, as well as a mapping between the users ethereum address to the DID.

![3Box Architecture Diagram](./3box_architecture_diagram.png)


### Root Object
The root object is an IPLD formated ipfs object that contains a link to the latest hash of the public profile and a link to the latest hash of the private data store. It have the following structure:

```js
{
  profile: {"/" : "zdpuAufy3hawb25akerURtR81y7D4BKfdxfqbpYZ7cJGjwgFW"},
  datastore: {"/" : "zdpuAufy3hawb25akerURtR81y7D4BKfdxfqbpYZ7cJGjwgDS"}
}
```

### Public Profile
The public profile is an IPLD formated ipfs object that contains the public information about the user such as name and picture. We use the Profile scheme from <http://schema.org/>, with extensions by [Blockstack](https://github.com/blockstack/blockstack.js/tree/master/src/profiles), and using IPLD links. We start with just the items `name` and `image`. Note that the `image` field is an array.

```js
{
  "@context": "http://schema.org/",
  "@type": "Person",
  "name" : "Christian",
  "image" : [{"@type": "ImageObject", "contentUrl": {"/" : "QmXXXX"}}].
}
```

### Private Data Store
The private data store is an orbit-db KV-store with additional encryption. The encryption scheme for adding a key-value entry would work as follows:

* Generate a random salt and store it encrypted (see below) under the `3BOX_SALT` plain text key.
* Compute the `key` by taking `h(PLAIN_KEY | salt)`
* Generate a random nonce `n`
* Add padding to `PLAIN_VALUE` so that its length is a multiple of `24`
* Compute the ciphertext: `nacl.secretbox(PLAIN_VALUE, n, secretKey)`
* Encode `value` as `{ nonce: Base64(n), ciphertext: Base64(ciphertext) }`

We can now store `key` and `value` in the orbit-db KV-store using the `put` method.

Optionally we can add an index of encrypted keys to the db.


## How it Works
Here's a technical walkthorough of how the system works.

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

