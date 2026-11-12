---
title: Examples
description: Script tag examples for the most common setups.
---

Each example uses the `@latest` URL. For a production site, replace `@latest` with a release tag. See [Installation](/installation#pin-a-release-tag).

## Minimal setup

Use the defaults. The script captures the default parameters and keeps the first source.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"></script>
```

## Custom parameters and attribution journey

Capture your own list of parameters. Keep all the sources of a visitor.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-params="utm_,gclid,fbclid,ref,campaign_id"
  data-merge-params="true"
></script>
```

## More than one domain, with cookies

Store the data in a cookie. If cookies are not available, use localStorage. Change links to two domains.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-storage="cookie|localStorage"
  data-allowed-domains=".example.com,partner.com"
></script>
```

## Debug mode and custom excludes

Write messages to the browser console. Skip PDF files, ZIP files and links that contain `logout` or `admin`.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-debug="true"
  data-exclude-patterns="*.pdf,*logout*,*admin*,*.zip"
></script>
```

## Settings as JSON

Put all settings in one attribute. The other data attributes override the JSON.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-config='{"params": ["utm_", "gclid"], "mergeParams": true, "ttl": 90}'
></script>
```

## Run your own code on capture

Use `init()` with a callback. See [JavaScript API](/javascript-api) for the details.

```js
ParamsSaver.init({
  params: ["utm_", "gclid", "fbclid", "custom_"],
  storage: "localStorage",
  mergeParams: true,
  debug: true,
  onCapture: function (params, isFirstTouch) {
    console.log("Captured:", params, "First touch:", isFirstTouch);
  },
});
```
