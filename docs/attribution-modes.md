---
title: Attribution modes
description: Keep the first source only, or keep a list of all sources with data-merge-params.
---

The script has two modes. The setting `data-merge-params` selects the mode.

## First-touch mode

This is the default. The setting is `data-merge-params="false"`.

The script saves the parameters of the first visit that has a match. After that, it ignores new parameters. It keeps the saved values until they expire. The default expiry is 30 days. See [Storage and privacy](/storage-and-privacy#how-long-data-stays).

```text
Visit 1: ?utm_source=google    -> stored: "google"
Visit 2: ?utm_source=facebook  -> stored: "google" (unchanged)
Visit 3: ?utm_source=medium    -> stored: "google" (unchanged)
```

In this mode, a later visit does not add even a parameter that is new. For example, if the first visit had only `utm_source`, a later `gclid` is not saved.

## Attribution journey mode

Set `data-merge-params="true"`. The script then keeps all the sources of a visitor.

For each parameter, the script joins the values with a pipe character (`|`). It adds a value only if the value is not in the list yet. The order stays the same.

```text
Visit 1: ?utm_source=google    -> stored: "google"
Visit 2: ?utm_source=facebook  -> stored: "google|facebook"
Visit 3: ?utm_source=medium    -> stored: "google|facebook|medium"
Visit 4: ?utm_source=medium    -> stored: "google|facebook|medium"
```

A parameter that is new is added with its value. The saved time of the first capture does not change.

Add the setting to the script tag.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-merge-params="true"
></script>
```

<Note>
In this mode, the script adds the joined value to your links, for example `utm_source=google|facebook`. Your analytics tool must accept such a value.
</Note>

## Know when data is saved

You can run your own code when the script saves data. Pass an `onCapture` function to `init()`. It receives the saved parameters and a flag that is `true` for the first save. See [JavaScript API](/javascript-api#onCapture).
