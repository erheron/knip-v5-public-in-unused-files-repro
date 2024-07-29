Knip `@public` modifier, if placed above an exported function, promises to make Knip not count this export as unused (even if it is)
However, if the exported unused function is placed in a file, where all exports are unused, `@public` modifier seems to have no effect

This is somewhat contradictory and perhaps presents an inconsistency in knip modifiers

This repository is a reproduction for https://github.com/webpro-nl/knip/issues/742

We have three files here:
* `src/unused-files.js` is a file where all exports are unused, and one of them is marked with `/** @public */` JSDoc modifier
* `src/partially-unused-file` exports a function which is later used in `src/main.js`

Moreover, in knip config `knip.jsonc`  we explicitly include `"files"` in knip report

If you clone this repo and run `yarn knip` you get this report: 

```sh
Unused files (1)
src/unused-file.js
Unused exports (1)
unused_getID  function  src/partially-used-file.js:5:17
```

So knip reports `src/unused-file.js` as an unused file (which it actually is), but also it means that `@public` modifier makes no effect there.
