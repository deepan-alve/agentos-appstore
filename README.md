# AgentOS App Store

The remote catalog for AgentOS — a phone-OS-style React Native shell where every "app" is a WebView of a mobile-first website.

The mobile app fetches `catalog.json` from this repo's `main` branch on launch. Edits here propagate to every installed copy of AgentOS the next time it opens the Store screen.

---

## Schema

`catalog.json` is a JSON array of catalog entries:

```json
{
  "id":        "string — stable unique identifier, lowercase, kebab-case",
  "name":      "string — app display name",
  "tagline":   "string — one-line description, ~50 chars max",
  "category":  "reading | productivity | developer | media | misc",
  "url":       "string — mobile-friendly URL the WebView opens",
  "slug":      "string — simple-icons slug for the brand logo (e.g. 'notion')",
  "color":     "string — hex like '#FF6719' (the brand accent color)",
  "tintWhite": "boolean (optional) — render the logo in white instead of brand color (use for black/dark logos against dark backgrounds)"
}
```

The `slug` must match a brand published in [simple-icons](https://simpleicons.org). The mobile app bundles the full simple-icons set (~3000 brands), so most popular services work out of the box.

If `category` is missing or unrecognized, the app treats the entry as `misc`.

## Categories

| Category       | For…                                          |
| -------------- | --------------------------------------------- |
| `reading`      | News, long-form, blogs, publications          |
| `productivity` | Notes, docs, design, project management       |
| `developer`    | Dev tools, code hosts, Q&A, dev communities   |
| `media`        | Audio, video, music, streaming                |
| `misc`         | Anything that doesn't fit above               |

## How to add an app

1. Fork this repo
2. Add an object to `catalog.json`
3. Open a PR — the description should mention why this app belongs and a screenshot of how it looks on mobile
4. Once merged, every AgentOS instance picks it up on next launch

## Validation

The mobile app validates each entry on fetch. Entries missing `id`, `name`, `url`, or `slug` are silently dropped. Catalog source falls back to the bundled (older) copy if the network request fails entirely.

---

## License

MIT. See [LICENSE](./LICENSE).
