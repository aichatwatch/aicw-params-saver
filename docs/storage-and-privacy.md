---
title: Storage and privacy
description: What the script stores, where it stores it, how long it keeps the data, and what it sends.
---

This page describes what the code does. It is not legal advice. Ask a qualified person if you need to know what the law requires for your site.

## What the script stores

The script stores one item. The name of the item is `pz_params`. The item holds:

- the captured parameters, as name and value pairs,
- the time of the first capture,
- the time when the item expires.

The script stores no other data about the visitor.

## Where it stores the data

The setting `data-storage` selects the storage. The default is `localStorage`.

| Value | Where the data goes |
|-------|---------------------|
| `localStorage` | Browser localStorage. Data stays until it expires or the visitor clears it. This is the default. |
| `sessionStorage` | Browser sessionStorage. The browser removes the data when the tab closes. |
| `cookie` | A cookie. The script sets the path to `/` and `SameSite=Lax`. |

By default the script uses no cookies.

## Use more than one store

Separate stores with a pipe character. The list is a priority list.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-storage="cookie|localStorage"
></script>
```

- The script writes to the first store that works.
- The script reads from the first store that has data.
- If a store is not available, the script goes to the next one.

A cookie can hold less than 4000 characters of data. If the data is larger, the script does not write the cookie.

## Share data between subdomains

A cookie can work on more than one subdomain. Set the first entry of `data-allowed-domains` to a domain that starts with a dot. The script uses this entry as the cookie domain.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-storage="cookie|localStorage"
  data-allowed-domains=".example.com,partner.com"
></script>
```

## How long data stays

The default expiry is 30 days. A value of `0` means the data never expires. The script sets the expiry each time it writes the data.

There is no data attribute for the expiry. Set `ttl` in the JSON of `data-config` or in `init()`. The value is in days.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-config='{"ttl": 90}'
></script>
```

## What the script sends

The script makes no network request. All data stays in the browser. The script only changes link addresses on the page. If a visitor clicks a changed link, the browser sends the parameters to the site of that link.

## Delete the data

Call `ParamsSaver.clear()`. It removes every item whose name starts with `pz_` from localStorage, sessionStorage and cookies. See [JavaScript API](/javascript-api).

## Consent

The script does not show a consent banner. It does not check consent. If your site needs consent before it stores data, load the script after the visitor agrees. The default settings use no cookies. If you set `cookie`, think about how your rules treat cookies.
