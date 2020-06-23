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

## Use-case

This is for `sodium-universal`, which wraps `sodium-javascript` and
`sodium-native`. `sodium-native` is a large native dependency, which it doesn't
make sense to split up. However to create minimal bundles in the browser,
`sodium-javascript` is modular. Being able to have a single module that exposes
both, and being able to automatically use either depending on context, comes
from `sodium-universal`, which mirrors `sodium-javascript`, but exports
`sodium-native` for Node.js usage. In the browser it should replace itself with
the relevant submodules from `sodium-javascript`.

## Dependency tree

The fictional packages are installed as `file:` dependencies here, making the
directory structure a bit confusing. The real tree is here (from `npm ls`):

```
browserify-browser-replace-bug@1.0.0 ./browserify-browser-replace-bug
└─┬ noop-universal@1.0.0 -> ./browserify-browser-replace-bug/noop-universal
  ├── noop-javascript@1.0.0
  └── noop-native@1.0.0
```
