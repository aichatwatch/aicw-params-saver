---
title: Installation
description: Load the script from the jsDelivr CDN, pin a release tag, or build and host the files yourself.
---

You can load the script from a CDN (content delivery network) or host it yourself. The project is not on npm.

## Load from the CDN

jsDelivr serves the files from the GitHub repository. Add this tag to your pages.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"></script>
```

The `@latest` part loads the newest release. A new release can change how the script works. For a production site, pin a tag.

## Pin a release tag

A release tag is a fixed version of the script. Tags are dates and times, for example `v20261031.113523`. Replace `@latest` with the tag.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@v20261031.113523/dist/aicw-params-saver.min.js"></script>
```

Find all tags on the [releases page](https://github.com/aichatwatch/aicw-params-saver/releases).

<Note>
The package is private in `package.json`. It is not published to npm. Use the CDN or build the files yourself.
</Note>

## Host the files yourself

If you do not want to use the CDN, build the files and copy them to your server.

<Steps>
  <Step title="Clone the repository">
    ```sh
    git clone https://github.com/aichatwatch/aicw-params-saver.git
    ```
  </Step>
  <Step title="Go to the folder">
    ```sh
    cd aicw-params-saver
    ```
  </Step>
  <Step title="Install the build tools">
    ```sh
    npm install
    ```
  </Step>
  <Step title="Build the files">
    ```sh
    npm run build
    ```
  </Step>
</Steps>

The build writes these files to the `dist` folder:

| File | Content |
|------|---------|
| `aicw-params-saver.js` | UMD build |
| `aicw-params-saver.min.js` | Minified UMD build. Use this file in a script tag. |
| `aicw-params-saver.esm.js` | ES module build |
| `aicw-params-saver.d.ts` | TypeScript declarations |

UMD is a file format that works in a plain script tag. Copy `aicw-params-saver.min.js` to your server and point the script tag at it.

```html
<script src="/js/aicw-params-saver.min.js"></script>
```

## Use the ES module build

The ES module build exports the object `paramsSaver` as the default export. The script tag attributes work only in a normal script tag. If you import the module, pass your settings to `init()`. See [JavaScript API](/javascript-api).

## Browser support

The code compiles to ES2018. It has no runtime dependencies.
