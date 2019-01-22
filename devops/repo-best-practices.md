# Repo best practices
Here a bunch of best practices that should be used in all of our github repos are described.

## General
General things that applies to all repos

### Git flow / branching
We use a git flow like practice for managing git branches. There are two main branches `master` and `develop`.

 * the master branch only contains releases
 * the develop branch is where all development work gets merged before a release

#### Creating a feature branch
Feature branches are used for all development work that isn't a `hotfix`. To create a feature branch make sure to checkout the `develop` branch then do,
```sh
$ git checkout -b feature/<your-feature-name>
```

Once done make sure all tests are passing and make a PR against the `develop` branch

#### Creating a hotfix branch
Hotfix branches are for fixing errors and bugs that appear in the latest release (the latest code in the master branch). To create one make sure to checkout the `master` branch and then,
```sh
$ git checkout -b hotfix/<name-of-bug>
```

Once the bug is fixed bump the patch number (last/third number in semver) and then create a PR against the `master` branch. Once that is merged also make sure to merge `master` into `develop`

#### Making a release
When you are ready to make a release make sure you have `develop` checked out bump the version number and add a new entry in the `RELEASE-NOTES.md` file describing all changes that this version contain. Then make a PR against `master`. Once it is merged make sure to tag the merge commit by doing,
```sh
$ git checkout master
$ git pull
$ git tag vX.X.X
$ git push --tags
```

### Testing
For all our javascript repos we use **jest** for testing. To install:
```sh
$ npm install --save-dev jest
```
Then add jest into npm scripts in your `package.json`, this can be configured according to the projects needs.
```js
"test": "./node_modules/.bin/jest --coverage --runInBand",
```

### Code style standard
For all our javascript repos we use **standardjs** for testing. To install:
```sh
$ npm install --save-dev standard
```
Then add standard into npm scripts in your `package.json`, this can be configured according to the projects needs.
```js
"lint": "./node_modules/.bin/standard --verbose src/**",
```

### CircleCi
TODO - how to configure and set up CircleCi.

## Build and publish
There are different approaches to building an publishing code depending if it is a library of a server project. Below both are described.

### For libraries
In the `package.json` there should be an entry in the `scripts` section named `build` which builds the project. You should also make sure that `main` in the `package.json` points to the build.
We also want to make sure that the library is built before it is published. Therefor the following should be added to the `scripts` section,
```js
"prepublishOnly": "npm run test; npm run build",
```

### For servers and websites
TODO - how to set up CircleCi to publish builds to aws.
