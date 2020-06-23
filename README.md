## Bug

This is an example of trying to replace a local file with a installed module
via the `browser` field in `package.json`.

`noop-universal` exports `noop-native` from all it's files `index.js` and
`sub.js`, but in the browser `index.js` should be replaced with
`noop-javascript`, and `sub.js` should be replaced with `noop-javascript/sub`.

Excerpt from `noop-universal/package.json`:

```json
{
  "browser": {
    "./index.js": "noop-javascript",
    "./sub.js": "noop-javascript/sub"
  }
}
```

## Dependency tree

The fictional packages are installed as `file:` dependencies here, making the
directory structure a bit confusing. The real tree is here (from `npm ls`):

```
browserify-browser-replace-bug@1.0.0 ./browserify-browser-replace-bug
└─┬ noop-universal@1.0.0 -> ./browserify-browser-replace-bug/noop-universal
  ├── noop-javascript@1.0.0
  └── noop-native@1.0.0
```
