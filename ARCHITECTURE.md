# 3Box Architecture
## Data Model
Each user has two data stores. One for public data and one for private data. To keep track of these data stores there is a root store that points to the addresses of the two data stores. The user only needs to have access to the address of the root store in order to fetch all of the database content from both the private and public stores.

When a new database for a user is created in the `3box-js` library a DID is derived from the users ethereum address. A mapping from the ethereum address to the DID and from the DID to the root store address are stored on the `3box-address-server`. This server also pins the ipfs data from the users stores so that it's always available.


### Root Store
The root store is an orbitdb `feed`, basically a list of entries. The `feed` store allows us to add and remove entries. In our case we would add two entries to this feed, one for each store (with the possibility of adding more stores in the future).

The two entries would be the orbitdb addresses for the public and private stores. For example these could look like:
```
 /orbitdb/Qmd8TmZrWASypEp4Er9tgWP4kCNQnW4ncSnvjvyHQ3EVSU/<user-fingerprint>.public
```
for the public store and
```
 /orbitdb/Qmd8TmZrWASypEp4Er9tgWP4kCNQnW4ncSnvjvyHQ3EVSU/<user-fingerprint>.private
```
for the private store. Here `<user-fingerprint>` is the multihash of the users DID.


### Public Profile
The public profile store is a orbitdb keyvalue-store.

### Private Data Store
The private data store is an orbit-db KV-store with additional encryption.

#### Encryption
The encryption scheme for adding a key-value entry would work as follows:

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

![3Box Architecture Diagram](./3box_architecture_diagram.png)

### Creating a user profile

**A.** The dapp gets the users address from MetaMask (or any web3 compliant browser)

**B.** Dapp request public or private data from the users 3box

**C.** `3box-js` MM interactions
  1. `3box-js` requests consent for storing and retrieving private and public data. The signature is used as key material when creating the 3box DID.
  2. `3box-js` requests consent for linking the public profile to the users ethereum address

**D.** `3box-js` creates the root, private, and public stores. Then adds data to these stores.

**E.** `3box-js` sends the orbitdb address of the root store and the profile link to the `3box-address-server`. The server creates an instance of the users stores and syncs them.

**F.** Any updates that are made to any of the stores are replicated on the `3box-address-server` using orbitdb's internal replication system. This system uses ipfs pubsub to send the data between two ipfs nodes, which means that both nodes have to have the pubsub protocol enabled.


### Accessing user data

**A.** *Same as above*

**B.** *Same as above*

**C.** `3box-js` MM interactions
  1. `3box-js` requests consent for storing and retrieving private and public data. The signature is used as key material when creating the 3box DID.

**E.** `3box-js` sends a request to the `3box-address-server` to get the address of the root store.

**D.** `3box-js` syncs the root, private, and public store using the orbitdb pubsub replication. Any data in the database can now be accessed.

**F.** *Same as above*

