---
title: Troubleshooting
description: Check that links change, find out why a link does not change, and fix common problems.
---

## Check which links change

You can watch the links that you hover over. Use the browser console.

<Steps>
  <Step title="Open the developer console">
    In your browser, press `Cmd+Shift+I` on Mac or `Ctrl+Shift+I` on Windows and Linux. Open the Console tab.
  </Step>
  <Step title="Run the hover check">
    Paste this code and press Enter. It writes the address of each link that you hover over.

    ```js
    window.addEventListener("mouseover", event => {
      const link = event.target.closest("a");
      if (link && link.href) {
        console.log("Hovered Link:", link.href);
      }
    });
    ```
  </Step>
  <Step title="Open your site with a parameter">
    In the same browser window, open a page of your site that has the script. Add a parameter to the URL, for example `?utm_campaign=github-aicw-params-saver`.
  </Step>
  <Step title="Move the mouse over other links">
    Look at the console. The internal links now have `utm_campaign=github-aicw-params-saver`.
  </Step>
</Steps>


## See what is stored

Run this in the console to see the saved parameters.

```js
ParamsSaver.getParams()
```

If the result is an empty object, the script has saved nothing. Run the next check.

## Turn on debug messages

Add `data-debug="true"` to the script tag. Reload the page. The console shows messages that start with `[ParamsSaver`. They tell you what the script captured, which links it changed and why it skipped a link.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-debug="true"
></script>
```

## Common problems

<AccordionGroup>
  <Accordion title="No link changes">
    - Check that the URL has a parameter that matches your list. The default list is in [What it captures](/what-it-captures).
    - Check that the parameter has a value. The script ignores empty values.
    - Check that the script is on the page. Look in the Network tab for `aicw-params-saver.min.js`.
  </Accordion>
  <Accordion title="Old parameters stay, new ones do not appear">
    This is first-touch mode. The script keeps the first source. To keep all sources, set `data-merge-params="true"`. To start again, run `ParamsSaver.clear()`. See [Attribution modes](/attribution-modes).
  </Accordion>
  <Accordion title="Links to my own site do not change">
    If you set `data-allowed-domains`, add your own domain to the list. Also check that the link does not match an exclude pattern and has no `pz-ignore` class. See [Link decoration](/link-decoration).
  </Accordion>
  <Accordion title="A link to a PDF or a ZIP file does not change">
    The default exclude patterns skip these files. This is normal. See [Link decoration](/link-decoration#default-exclude-patterns).
  </Accordion>
  <Accordion title="Parameters are gone after a while">
    The stored data expires after 30 days by default. Set `ttl` to change it. See [Storage and privacy](/storage-and-privacy#how-long-data-stays).
  </Accordion>
  <Accordion title="The data does not carry over to another subdomain">
    localStorage works for one host only. Use `data-storage="cookie|localStorage"` and set the first entry of `data-allowed-domains` to a domain that starts with a dot. See [Storage and privacy](/storage-and-privacy#share-data-between-subdomains).
  </Accordion>
  <Accordion title="The data attributes have no effect">
    Check that the attribute names are spelled as in [Configuration](/configuration). Check that `data-config` holds valid JSON. The script ignores invalid JSON without an error message.
  </Accordion>
</AccordionGroup>

## Report a bug

To report a bug or ask a question about the tool, open an issue on [GitHub](https://github.com/aichatwatch/aicw-params-saver/issues). For other contact, use the [AI Chat Watch contact page](https://aichatwatch.com/quote).
