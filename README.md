# @release-git-plugins/lerna-changelog

This package is a [release-git](https://github.com/release-git/release-git) plugin
(using [`release-git`'s plugin
API](https://github.com/release-git/release-git/blob/master/docs/plugins.md)) that
integrates [lerna-changelog](https://github.com/lerna/lerna-changelog) into the
`release-git` pipeline.

## Usage

Installation using your projects normal package manager, for example:

```
# npm
npm install --save-dev @release-git-plugins/lerna-changelog

# yarn add --dev @release-git-plugins/lerna-changelog
```

Once installed, configure `release-git` to use the plugin.

Either via `package.json`:

```json
{
  "release-git": {
    "plugins": {
      "@release-git-plugins/lerna-changelog": {}
    }
  }
}
```

Or via `.release-git.json`:

```json
{
  "plugins": {
    "@release-git-plugins/lerna-changelog": {}
  }
}
```

## Configuration

`@release-git-plugins/lerna-changelog` supports one configuration option, `infile`. When
specified, this option represents the file name to prepend changelog
information to during a release.

For example, given the following configuration (in `package.json`):

```json
{
  "release-git": {
    "plugins": {
      "@release-git-plugins/lerna-changelog": {
        "infile": "CHANGELOG.md",
        "launchEditor": true
      }
    }
  }
}
```

The two options that `@release-git-plugins/lerna-changelog` is aware of are:

### `infile`

`infile` represents the file to prepend the generated changelog into.

### `launchEditor`

When specified, `@release-git-plugins/lerna-changelog` will generate the changelog
then launch the configured editor with a temporary file. This allows the person
doing the release to customize the changelog before continuing.

There are a few valid values for `launchEditor`:

* `false` - Disables the feature.
* `true` - If present the `process.env.EDITOR` value will be used as the
  command to invoke, if `process.env.EDITOR` is not found `process.env.PATH`
  will be searched for a command named `editor` (which is commonly used on
  Debian / Ubuntu systems to point to the currently configured editor). The
  temporary file for editing is added as an argument (i.e.
  `$EDITOR /some/tmp/file`).
* any string - This string will be used as if it were a command. In order to
  interpolate the temporary file path in the string, you can use `${file}` in
  your configuration.

Each release will run `lerna-changelog` and prepend the results into `CHANGELOG.md`.

## License

This project is licensed under the [MIT License](LICENSE.md).
