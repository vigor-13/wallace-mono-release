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
yarn lerna init
```

```json
{
  "version": "0.1.0",
  "npmClient": "yarn",
  "packages": ["packages/*"]
}
```

# References

- [yarn doucment](https://classic.yarnpkg.com/lang/en/docs/workspaces/)
- [lerna document](https://github.com/lerna/lerna)
