# 3Box Spaces specification

In the current design of 3Box, any dapp that the user authorizes will have full read & write access to the users stored data. The concept of *spaces* within 3Box is a way to segregate data between dapps in a way where the user needs to explicitly approve the read/write access to the data associated with a specific dapp. Data in these spaces are segregated from the "generic data" that the user approves access to using the current consent message.

We will use the terminology "Generic Space" to refer to the standard public and private data stores in the current architecture.

# Technical description

The user provides access to a Space by signing a consent message that specifically mentions that Space by using a label. For instance the Gnosis dapp might have the label “Gnosis”, and the consent message would then be something like "This dapp wants to access data in your 3Box associated with Gnosis". From the entropy in the signature we generate a signing key `k` and a symmetric encryption key `s` similar to the general case. However we do not generate a full muPort identity from this signature.

Suppose we are creating the Space for the first time. In the users 3Box root store we add the new Space as two additional orbitdb addresses, one for public data and one for private data.  If the dapp only requires public data we would only need to create the public orbitdb instance, and similarly for private data.

The access control to the orbitdb instances will use the signing key `k`. The public space is readable publicly, but from the design it follows that dapps need the private signing key `k` in order to update this public data. In other words the dapp needs explicit consent from the user to update or delete the public data in a specific Space.

The names of the orbitdb instances would be derived from the label of the Space used in the consent message (“Gnosis” in our example above). This way it is clear which orbitdb instance we attach to a specific Space.

The private store is only readable by a dapp if that dapp specifically asks the user to sign the consent message for that particular Space (i.e. if the dapp has acccess to the symmetric key `s`).

The encryption for the private store is done using the symmetric key in exactly the same way as for the Generic Space.

The user would still need to sign the default consent message in order to access the generic space and gain access to the root store where the addresses of the new orbitdb instances are added.

# User Experience

The user visits a dapp. They start by signing the generic consent message. If the dapp is using a Space `S` this dapp will then show the user the specific consent message for that Space and ask them to sign it.

After the user signs the message they see their private generic data and the private data from the Space `S`. They can update the private and public data from both the Generic Space and the Space `S`. The user will see the public data from any other Space but cannot update this data, and they will not see the private data from any other Space.

## UX Challenge

If a dapp requires read or write access to many different Spaces the user would be presented with  many different consent messages to sign, which would lead to a poor user experience.

A possible mitigation to this would be if Ethereum wallets supported batched signing of messages.
