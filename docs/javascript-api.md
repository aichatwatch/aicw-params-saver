---
title: JavaScript API
description: Read the saved parameters, clear them, or start the script by hand with init().
---

The script adds a global object named `ParamsSaver` to the page. It has four methods.

## getParams()

Returns all saved parameters as an object. If nothing is saved, it returns an empty object.

```js
ParamsSaver.getParams()
```

Example result:

```js
{ utm_source: "google", utm_medium: "cpc", gclid: "abc123" }
```

## getParam(name)

Returns the value of one saved parameter. If the parameter is not saved, it returns `null`.

```js
ParamsSaver.getParam("utm_source")
```

## clear()

Removes all data that the script stored. This includes items in localStorage, sessionStorage and cookies whose names start with `pz_`. It also resets the list of changed links.

```js
ParamsSaver.clear()
```

`clear()` does not undo links that the script already changed.

## init(config)

Starts the script with your settings. The script also starts by itself when it loads. A call to `init()` starts it again with the new settings.

Every key is optional. The keys are the same as in the `data-config` JSON. See [Configuration](/configuration#settings-in-data-config).

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

`init()` does not read `data-` attributes. Settings that you do not pass use the default values.

### onCapture

`onCapture` is a function that the script calls after it saves parameters. It gets two arguments:

| Argument | Type | Description |
|----------|------|-------------|
| `params` | Object | All saved parameters after this save. |
| `isFirstTouch` | Boolean | `true` if no data was saved before. |

The script does not call `onCapture` if the page URL has no matching parameter. In first-touch mode, it also does not call it when data is already saved.

## Errors

If `init()` fails, the script catches the error. It writes the error to the console only when `debug` is `true`.

## TypeScript

The file `aicw-params-saver.d.ts` has the types `ParamsSaverConfig`, `ParamsSaverAPI` and `ParamData`. See [Installation](/installation#host-the-files-yourself).
