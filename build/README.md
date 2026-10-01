# Building robbiemed.org

`index.html` and `sitemap.xml` at the repo root are **generated**. Don't edit them by hand.

| File | What it holds |
|---|---|
| `tools.json` | Every section and tool: name, URL, search tags, and descriptions in all six languages (ko, en, fr, zh, ru, ar). |
| `template.html` | The page itself: layout, styles, contact section, interface strings, scripts. |
| `build.mjs` | Fills the template from `tools.json`, writes `index.html` and `sitemap.xml`. No dependencies. |

```bash
node build/build.mjs           # rebuild
node build/build.mjs --check   # fail if index.html is stale
```

## Adding a tool

Add an object to the right category's `tools` array in `tools.json`, in the position you want it listed:

```json
{
  "key": "example",
  "name": "Example",
  "url": "https://example.robbiemed.org",
  "tags": "example extra search words",
  "d": { "ko": "…", "en": "…", "fr": "…", "zh": "…", "ru": "…", "ar": "…" }
}
```

- `key` is lowercase letters and digits, unique.
- `os` is optional and only for things that aren't plain web apps, e.g. `"Windows"` or `"Any (web browser), Android"`.
- Korean is the default language: its text is what ships in the HTML source.

Then run the build and commit `tools.json`, `index.html` and `sitemap.xml` together. The build refuses to run if any tool is missing a language.

`build/` is listed in `.assetsignore`, so Cloudflare doesn't serve it.
