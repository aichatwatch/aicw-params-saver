---
title: SPA support
description: How the script changes links that a single-page app adds or moves after the page loads.
---

A single-page application (SPA) loads one HTML page. It then changes the content and the address with JavaScript. The script needs no setting for this.

## What the script watches

| Event | What the script does |
|-------|----------------------|
| New elements are added to the page | If the new elements include links, the script changes them after 100 ms. |
| The app calls `history.pushState` or `history.replaceState` | After 50 ms, the script resets its list of changed links and changes all links again. |
| The visitor uses the back or forward button of the browser (the `popstate` event) | The script does the same as for `pushState`. |

The script watches the `body` element and all elements inside it.

## What the script does not do

After an address change, the script does not read the URL again. It does not capture new parameters. It captures parameters only when the page loads.

If your app opens a new URL with new `utm_` parameters without a page load, the script does not save them.

## Notes

- The script calls the original `pushState` and `replaceState` first. Your app works as before.
- If the browser has no `MutationObserver`, the script skips link watching. The history hooks still work.
