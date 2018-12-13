# Threads: A p2p communication protocol

Created: Nov 20, 2018 9:05 PM
Status: Spec
Tags: 3Box.js

# Overview

Threads is a feature that enables one or multiple users to post messages in a sequence. This enables users to communicate asynchronously in many forms. For example it could be used for comments, chats, status updates, etc. Threads uses the orbitdb feedstore to create a log of messages that is eventually consistent. They can be public or private/encrypted. Each thread is initially only owned by the creator, but more users can be added as the thread evolves.

## Access control

Right now orbitdb doen't support adding and removing users to a given DB. However if we are fine with the constraint that users can only be added to the thread and not removed we can do the following. For a new thread we create a random seed `R`. From `R` we derive a signing key `k` and a symmetric encryption key `s`. The signing key `k` is given write permissions in the orbitdb feedstore. Each user has a public encryption key `E_<user>` associated with their 3box. If *Alice*  creates the thread, she encrypts `R` to her key `E_alice` and adds this encrypted blob as an entry in the thread. Now when *Alice* want's to grant access to *Bob* she simply encrypts `R` to `E_bob` and adds this encrypted blob as an entry in the thread. *Bob* can now see this encrypted entry and decrypt it to recover `k` and `s` which can be used to post in the thread.

OrbitDB is [working on adding](https://github.com/orbitdb/orbit-db/pull/495) support for access controllers. When they are released we can use them for write access to threads. There is not really any benefit in changing to this until they also add the ability to remove users.

## Encryption

We simply use `s` to symmetrically encrypt the entries in the thread if it's a private thread.

## Thread subscriptions

Users can subscribe to threads. This means that they will remember the thread next time they go online, and they can ask the network for updates. When a user subscribes to a thread it simply adds the thread-id and name to the rootStore of the users 3Box. When the user unsubscribes the thread entry is removed from the rootStore.

## Threads in spaces?

Is this something we want to enable? Maybe as a second iteration, it adds a lot of complexity.

## API

**List threads the user is subscribed to:**
```js
const threadNames = box.threads.list()
console.log(threadNames)
> ["3box-chat", "Bounties-issue432"]
```

**Create a new thread:**

The `open` parameter is a boolean that specifies if there is write permissions to the thread or not. Open threads anyone can post to, but there is no spam protection. Note that new threads are not automatically subscribed to.

```js
const thread = await box.threads.new(<name>, <open=false>)
```

**Get thread id**

the thread-id is simply the orbitdb-address (String) of the underlaying DB.

```js
const threadId = thread.getId() 
```

**Subscribe to an existing thread:**

```js
const thread = await box.threads.subscribe(<thread-id>, <name>) 
```

**Unsubscribe from a thread:**

```js
await box.threads.unsubscribe(<name>)
```

**Posting to a thread:**

```js
await thread.post(<json-object>) 
```

**Adding a user:**

```js
await thread.addUser(<eth-addr|muport-did>) 
```

**Reading a thread:**

We can probably design this similar to the [orbitdb feed iterator](https://github.com/orbitdb/orbit-db/blob/master/API.md#iteratoroptions-1). 

```js
const threadIterator = thread.iterator() 
```

**Watching for updates:**

```js
thread.onPost(post => {})
```
