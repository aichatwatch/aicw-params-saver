---
title: What it captures
description: The default parameters, how the script matches names, and how to change the list.
---

The script reads the query string of the page URL. The query string is the part of the URL after the `?`. It saves each parameter that matches your list.

## Default parameters

| Pattern | What it matches |
|---------|-----------------|
| `utm_` | `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content` and any other name that starts with `utm_` |
| `gclid` | Google Ads click ID |
| `fbclid` | Facebook click ID |
| `msclkid` | Microsoft (Bing) Ads click ID |
| `ref` | A common referral parameter |

## How matching works

Each entry in the list is a prefix. A parameter matches if its name starts with the entry. Matching is case-sensitive.

- `utm_` matches `utm_source` and `utm_anything`.
- `ref` matches `ref`. It also matches `referrer` and `refid`, because those names start with `ref`.

The script saves only parameters that have a value. It ignores a parameter with an empty value.

## Change the list

Use the `data-params` attribute. Separate the entries with commas.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-params="utm_,gclid,campaign_id"
></script>
```

Your list replaces the default list. If you want to keep `fbclid`, `msclkid` and `ref`, write them in your list.

## When the script captures

The script reads the URL when the page loads. It does not read the URL again when a single-page app changes the address. See [SPA support](/spa-support).

By default, the script keeps the parameters of the first visit that had a match. Later visits do not change them. To track more than one visit, see [Attribution modes](/attribution-modes).
