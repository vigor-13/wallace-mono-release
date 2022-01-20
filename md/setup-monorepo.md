# Setup monorepo

Setup monorepo by lerna & yarn-workspaces

[back to README.md](../README.md)

# Steps

1. Setting up `package.json` & Add some packages.
2. Install `lerna`.
3. Setting up `lerna.json`.

## 1. Setting up `package.json`

_package.json_

```json
{
  "private": true, // Required!
  "workspaces": ["packages/*"]
}
```

- workspaces are not meant to be published, so we’ve added this safety measure to make sure that nothing can accidentally expose them.

## 2. Install lerna

```shell
yarn add -W -D lerna
```

## 3. Setting up `lerna.json`

```shell
yarn lerna init --independent
```

```json
{
  "version": "independent",
  "npmClient": "yarn",
  "packages": ["packages/*"]
}
```

- Independent mode Lerna projects allows maintainers to increment package versions independently of each other. Each time you publish, you will get a prompt for each package that has changed to specify if it's a patch, minor, major or custom change.

# References

- [yarn doucment](https://classic.yarnpkg.com/lang/en/docs/workspaces/)
- [lerna document](https://github.com/lerna/lerna)
