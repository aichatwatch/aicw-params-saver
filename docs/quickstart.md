---
title: Quickstart
description: Add one script tag to your pages and check that the links change.
---

This page shows the shortest way to use the script.

## Add the script

Add this tag to every page of your site. Put it in the page HTML.

```html
<script src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"></script>
```

With no other settings, the script does these things:

- It captures `utm_` parameters, `gclid`, `fbclid`, `msclkid` and `ref`.
- It stores them in localStorage. It does not use cookies.
- It adds them to all internal links on the page.

<Tip>
For a production site, pin the script to a release tag. See [Installation](/installation#pin-a-release-tag).
</Tip>

## Check that it works

<Steps>
  <Step title="Open your site with a parameter">
    Open a page of your site and add a parameter to the URL, for example `?utm_campaign=test`.
  </Step>
  <Step title="Look at an internal link">
    Move the mouse over an internal link. Read the address in the status bar of the browser. The link now has `utm_campaign=test`.
  </Step>
  <Step title="Click the link">
    Click the link. The next page has the same parameter in its URL. If the script is on that page too, the links on that page have it as well.
  </Step>
</Steps>

If the link does not change, read [Troubleshooting](/troubleshooting).

## Next steps

- To change which parameters the script captures, see [What it captures](/what-it-captures).
- To change which links the script changes, see [Link decoration](/link-decoration).
- To see all settings, see [Configuration](/configuration).
