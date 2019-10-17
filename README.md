# standard-commit

## Getting Started

### Installation

#### Step 1 - Install Husky, commitlint and standard-version locally

`yarn add --dev husky @commitlint/cli @commitlint/config-conventional standard-version`

#### Step 2 - Install commitizen globally

`sudo yarn global add commitizen`

#### Step 3 - Update package.json

```
{
  ...

  "scripts": {
    "release": "standard-version"
  },
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
     }
  },
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
  }
}
```

#### Step 4 - Create a `commitlint.config.js` file in your project root directory

```
module.exports = {
  extends: ['@commitlint/config-conventional']
};
```

#### Step 5 - Configure commitizen

`commitizen init cz-conventional-changelog --save-dev --save-exact`

#### Step 6 - Commit

```
git add .
git cz
yarn release
```