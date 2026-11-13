---
title: Configuration
description: Every data attribute and setting, with its type and default value.
---

You set options with `data-` attributes on the script tag. You can also pass the options to `init()`. See [JavaScript API](/javascript-api).

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-params="utm_,gclid,custom_"
  data-storage="localStorage"
  data-merge-params="true"
  data-debug="true"
></script>
```

## Data attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `data-params` | Comma-separated list | `utm_,gclid,fbclid,msclkid,ref` | Parameter names to capture. Each entry matches names that start with it. |
| `data-storage` | Text | `localStorage` | `localStorage`, `sessionStorage`, `cookie`, or a list with pipes, for example `cookie\|localStorage`. |
| `data-merge-params` | `true` or `false` | `false` | `true` keeps all sources of a visitor. `false` keeps the first source. |
| `data-allowed-domains` | Comma-separated list | Empty (current host, root domain and subdomains) | Domains whose links the script changes. A wildcard such as `*.example.com` is allowed. |
| `data-exclude-patterns` | Comma-separated list | See [Link decoration](/link-decoration#default-exclude-patterns) | Link patterns that the script does not change. |
| `data-debug` | `true` or `false` | `false` | `true` writes messages to the browser console. |
| `data-config` | JSON | None | All settings in one attribute. |

Notes on these attributes:

- The script switches on `data-debug` and `data-merge-params` only when the value is exactly `true`.
- The script removes spaces around each list entry and ignores empty entries.
- A value that you set replaces the default value. It is not added to it.

## Settings in `data-config`

The `data-config` attribute holds JSON. Use these keys. Quote the whole attribute with single quotes, because JSON uses double quotes.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| `debug` | Boolean | `false` | Same as `data-debug`. |
| `params` | List of text | `["utm_", "gclid", "fbclid", "msclkid", "ref"]` | Same as `data-params`. |
| `storage` | Text or list | `"localStorage"` | Same as `data-storage`. |
| `ttl` | Number | `30` | Days until the stored data expires. `0` means it never expires. |
| `allowedDomains` | List of text | `[]` | Same as `data-allowed-domains`. |
| `excludePatterns` | List of text | See [Link decoration](/link-decoration#default-exclude-patterns) | Same as `data-exclude-patterns`. |
| `mergeParams` | Boolean | `false` | Same as `data-merge-params`. |

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-config='{"params": ["utm_", "gclid"], "storage": "cookie|localStorage", "ttl": 90, "mergeParams": true}'
></script>
```

The option `ttl` has no data attribute. Set it in `data-config` or in `init()`.

## Order of settings

1. The defaults.
2. The JSON in `data-config`.
3. The individual `data-` attributes. They override the JSON.

If the JSON in `data-config` is not valid, the script ignores it and uses the other settings.

## Fixed values

These values are not configurable:

| Item | Value |
|------|-------|
| Storage name prefix | `pz_` |
| Exclude selector | `[data-pz-ignore], .pz-ignore` |
