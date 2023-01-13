# standard-commit

Guidelines to standardize commit messages

[![license](https://img.shields.io/badge/License-MIT-blue.svg?style=flat)](LICENSE)

## Installation

- **commitlint** checks if your commit messages meet the [Conventional Commits](https://conventionalcommits.org/) specification
- **husky** will trigger the commitlint on each commit
- **commitizen** and **cz-conventional-changelog** helps format commit messages with a series of prompts
- **release-please** automates CHANGELOG.md, bump the version and generate a new release

### Step 1 - Install husky, commitlint, and cz-conventional-changelog locally

```sh
yarn add --dev husky @commitlint/cli @commitlint/config-conventional cz-conventional-changelog
```

### Step 2 - Install commitizen globally

```sh
sudo yarn global add commitizen
```

### Step 3 - Update package.json

```
{
  ...

  "config": {
    "commitizen": {
        "path": "./node_modules/cz-conventional-changelog",
        "disableScopeLowerCase": true
    }
  },

  ...
}
```

### Step 4 - Create a `commitlint.config.js` file in your project root directory

```
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'scope-case': [0],
  },
}
```

### Step 5 - Setup husky

#### Edit `package.json > prepare` script and run it once:

```
npm pkg set scripts.prepare="husky install"
yarn prepare
```

#### Add a hook to run commitlint

```
npx husky add .husky/commit-msg "yarn commitlint --edit"
```

### Step 6 - Configure commitizen

`commitizen init cz-conventional-changelog --save-dev --save-exact`

### Step 7 - Setup Release Please

#### Deploy release-please with GitHub Action

Create a `.github/workflows/release-please.yml` file with these contents:

```
on:
    push:
        branches:
            - main
name: release-please
jobs:
    release-please:
        runs-on: ubuntu-latest
        steps:
            - uses: google-github-actions/release-please-action@v3
              with:
                  release-type: node
                  package-name: release-please-action
```

## Usage

Basically, instead of typing `git commit` now you type `git cz` which will open a wizard and help you write a standardized message.

![Commitizen template](docs/img/commitizen_01.png)

### Commit with commitizen

Using commitizen to prompts a wizard.

```sh
git add .
git cz
git push --follow-tags
```

### Normal commit command

You can still use `git commit ...` but the commit will fail if the commit message is not properly formatted.

```sh
git add .
git commit -m "feat(blog): add comment section"
git push --follow-tags
```

## Credits

- Git hooks - [husky](https://github.com/typicode/husky)
- Lint commit messages - [commitlint](https://github.com/conventional-changelog/commitlint)
- Commit messages - [commitizen](https://github.com/commitizen/cz-cli)
- Generate release PRs - [release-please](https://github.com/googleapis/release-please)

## Contributing

Want to contribute? All contributions are welcome. Read the [contributing guide](CONTRIBUTING.md).

## Questions

If you have questions tweet me at [@sandro_m_m](https://twitter.com/sandro_m_m) or [open an issue](../../issues/new).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

**~ sharing is caring ~**
