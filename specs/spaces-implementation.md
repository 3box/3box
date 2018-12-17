Technical specification is [here](./spaces-specification.md)
# Spaces implementation

## API

`openBox` will have a new option:
```js
const opts = {
  spaces: {
    <name1>: 'public',
    <name2>: 'private',
    <name3>: 'both'
}
```
Passing this option you will open the given space(s) at the same time as opening the main space.

## `box.spaces.open(<name>, <mode>)`

Here *name* is the name of the space and *mode* is `'public'`, `'private'`, or `'both'`

The new space will be available as a keyValueStore as follows: 

`box.spaces.<name>.public`

`box.spaces.<name>.private`

## Key management

We add a new class to 3box-js called Keyring. This class can hold any number of (signing-key-pair, symmetric encryption-key) tuples. It also provides methods to symmetrically encrypt data. We can base it loosely on the keyring in muport-core, but lets use [https://www.npmjs.com/package/ethers](https://www.npmjs.com/package/ethers) instead of ethereumjs-wallet (we need to make sure that it is compatible, but it should be).

**Key derivation paths**

We can use the same derivation paths as in muport:

`BASE_PATH = m/7696500'/0'/0'`

Signing key: `BASE_PATH/0`

AsymEncryption key: `BASE_PATH/2`

SymEncryption key: `BASE_PATH/3`

But we also add a new derivation path for the salt for the private store:

Salt entropy: `BASE_PATH/4`

## Additional stores

When adding a new store we will simply create an orbitdb kv-store with the name `space.<name>.<mode>` e.g. `space.ujo.public`, `space.bounties.private`. The orbitdb-address of the created store is added to the rootStore. We also add the public encryption key of the space to the rootStore entry. This is not needed right away but results in flexibility for the future. The rootStore entry should look like this:
```js
{
  odbAddress: <orbitdb address of the space>,
  pubEncKey: <public encryption key derived above>
}
```

We have a research story for creating a better private kv-store that encrypts the keys instead of hashing them. If the research result is positive we should use that for the private spaces.
