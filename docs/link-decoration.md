---
title: Link decoration
description: Which links the script changes, how to allow other domains, and how to exclude links.
---

Link decoration means that the script adds the saved parameters to the `href` of a link. The script looks at every `a` element that has an `href`.

## Rules for each link

For each link, the script does these checks in order. If a check fails, the script does not change the link.

1. The link has an `href`.
2. The `href` does not start with `mailto:`, `tel:`, `javascript:`, `data:`, `blob:`, `file:`, `ftp:`, `sms:`, `whatsapp:`, `skype:`, `facetime:` or `#`.
3. The link has no `data-pz-ignore` attribute and no `pz-ignore` class.
4. The `href` does not match an exclude pattern.
5. The domain of the link is allowed.

When a link passes, the script adds each saved parameter that the link does not already have. It never changes a parameter that is in the link. It keeps the hash fragment (the part after `#`) and the other query parameters.

## Default allowed domains

If you do not set `data-allowed-domains`, the script changes links to:

- the current host,
- the root domain of the current host,
- all subdomains of the root domain.

For example, on `app.example.com`:

| Link to | Changed |
|---------|---------|
| `example.com` | Yes |
| `app.example.com` | Yes |
| `other.example.com` | Yes |
| `different.com` | No |

The script finds the root domain from the last two parts of the host name. For these two-part endings it uses the last three parts: `co.uk`, `com.au`, `co.nz`, `com.br`, `co.jp`, `org.uk` and `net.au`. For `localhost` and IP addresses, the root domain is the host itself.

## Allow other domains

Set `data-allowed-domains` to a comma-separated list. Each entry is one of these:

- A plain domain, for example `partner.com`. It matches only that exact host.
- A wildcard, for example `*.example.com`. It matches `example.com` and all its subdomains.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-allowed-domains="example.com,*.example.com,partner.com"
></script>
```

<Warning>
If you set `data-allowed-domains`, the list replaces the default rule. Add your own domain to the list. If you do not, links to your own site are not changed.
</Warning>

If the storage setting includes `cookie`, the first entry in this list is also the cookie domain. See [Storage and privacy](/storage-and-privacy).

## Default exclude patterns

The script does not change a link when its `href` matches one of these patterns.

| Type | Patterns |
|------|----------|
| Programs | `*.exe`, `*.msi`, `*.dmg`, `*.pkg` |
| Archives | `*.zip`, `*.rar`, `*.7z`, `*.tar*` |
| Documents | `*.pdf` |
| Protocols | `mailto:*`, `tel:*`, `javascript:*` |
| Pages | `*logout*`, `*signout*`, `*unsubscribe*` |

A pattern can use `*` for any characters and `?` for one character. Matching is not case-sensitive. A pattern must match the whole `href` text.

Set `data-exclude-patterns` to use your own list.

```html
<script
  src="https://cdn.jsdelivr.net/gh/aichatwatch/aicw-params-saver@latest/dist/aicw-params-saver.min.js"
  data-exclude-patterns="*.pdf,*logout*,*admin*,*.zip"
></script>
```

<Warning>
Your list replaces the default list. If you want to keep a default pattern, write it in your list.
</Warning>

## Exclude one link

Add the `data-pz-ignore` attribute or the `pz-ignore` class to the link.

```html
<a href="/logout" data-pz-ignore>Logout</a>
```

```html
<a href="/admin" class="pz-ignore">Admin</a>
```

## Other notes

- The script changes a link only one time. After a single-page app changes the address, or after `clear()`, it can change the link again.
- If the script has no saved parameters, it changes no link.
- The script does not change a link when the new `href` is the same as the old one.
