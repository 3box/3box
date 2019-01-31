# Key Conventions

The `key` parameter is used to get, set, and remove values in both the profile and the private store. It has to be a unique string. In order to facilitate collaboration and avoid any collisions between dapps we have created some simple rules.

## Dapp specific entries
Dapps can avoid collisions in their entries by using the following format:
```
<dapp-name>.<key-name>
```

An example for this would be,
```
ujo.description
```

## Common entries
There are lots of cases where it can be valuable for dapps to use the same entries/data, e.g. name and image in the profile, and email in the private store. Below are tables containing well known keys. Feel free to add more by making a PR :)

### Public Data

| Key | Description |
| -- | -- |
| name | a name chosen by the user |
| image | an ipfs hash of a profile image |
| attestari.skills | array of skills (object) listed on attestari.me |
| attestari.attestations | object containing all the attestations received by skill via attestari.me |

### Private Data

| Key | Description |
| -- | -- |
| email | the user's email address |
| consensys.employment | a claim the user works at ConsenSys |
| attestari.pendingAttestations | list of attestations waiting to be attested by other people via attestari.me |
| ipfsUploader.files | up to date array of ipfs file hashes uploaded by the user |
| ipfsUploader.files[ipfsHash].name | user given name of a file uploaded to ipfs |
| ipfsUploader.files[ipfsHash].date | unix timestamp of file uploaded to ipfs |

### Example entry data
Here are examples of the data that are stored in the above keys.
#### Public

##### name
A `String` e.g. `oed`

##### image
An array with data:
```json
[{"@type":"ImageObject","contentUrl":{"/":"QmNoyzwnzA6sGM2BGFZ1C6dVbGnjWy8QXWgQgQABRApkJk"}}]
```

#### Private

##### email
A `String` e.g. `oed@gmail.com`

