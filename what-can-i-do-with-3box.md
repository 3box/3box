# How can I use 3Box?
APIs for Identity, Authentication, Profiles, Storage, Messaging

## Develop Fully-Featured Apps Faster with Easy-to-Use APIs

### 🆔 Identity
**Identity API** methods allows developers to perform various user identity and account functionalities, such as getting the identity (DID) of a user (address), linking new addresses to the DID, and adding new authentication methods to the DID. 

Available in `3Box.js` and `IdentityWallet.js`.

### 🔐 Authentication
**Authentication API** methods allow developers to request access to a user's 3Box profile and spaces. Authentication is required to update any data, decrypt private data, and generally interact with the user's data stores in a meaningful way. 

Available in `3Box.js` and `IdentityWallet.js`.

*Onboarding (SSO): The Authentication API, combined with the Profiles API and Spaces API, enable frictionless user onboarding and SSO using 3Box. Developers can authenticate a user and then read existing data from their profile and spaces to streamline the onboarding process.*

### 👩 Profiles
**Profiles API** methods allow developers to perform various actions on the user's general profile, including getting and setting public and private profile information. The general profile is used to keep information that can easily be shared across apps, such as name, image, group affiliations, and public social verifications. 

Available in `3Box.js`.

### 📂 Storage
**Storage (Spaces) API** methods allow developers to perform various actions on the user's spaces, including getting and setting public and private information. Spaces are sandboxed stores used to keep information specific to an application or context, such as user generated content, documents, preferences, settings, and more sensitive information. 

Available in `3Box.js`.

### 💬 Messaging
**Messaging (Threads) API** methods allow developers to perform various actions on messaging threads including creating threads, getting and setting data to threads, and adding moderators. Threads are feed stores that are great for supporting social messaging, commenting, and chat systems between 1 or many users, for any application. They're also great for creating single or multi-user content streams.

Available in `3Box.js`.
