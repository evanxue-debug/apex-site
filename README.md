# website/

The public pages Apple requires for an auto-renewing subscription app: a privacy
policy and terms of use. Plain static HTML and one stylesheet — no build step, no
dependencies, no JavaScript.

```
index.html     landing page linking to both
privacy.html   privacy policy
terms.html     terms of use, including the health/medical disclaimer
style.css      shared styles, dark by default, light via prefers-color-scheme
.nojekyll      tells GitHub Pages to serve the files verbatim
```

All placeholders are filled in: the legal entity is **Zeyuan Xue (individual
developer)**, support is **evanxue@rplbb.com**, and the terms are governed by
**Singapore** law (§11).

## Published at

<https://evanxue-debug.github.io/apex-site>

| Page | URL |
|---|---|
| Privacy | `https://evanxue-debug.github.io/apex-site/privacy.html` |
| Terms | `https://evanxue-debug.github.io/apex-site/terms.html` |

The `.html` suffixes are deliberate — GitHub Pages serves files as-is and does
not rewrite extensionless URLs.

## Deploying to GitHub Pages

Push the *contents* of this folder to the root of the `apex-site` repository:

```bash
cd /tmp && rm -rf apex-site
git clone https://github.com/evanxue-debug/apex-site.git
cp -R /Users/alpha/Documents/apex/website/. apex-site/
cd apex-site && git add -A && git commit -m "Publish Apex legal pages" && git push
```

Then in that repo: **Settings → Pages → Source: Deploy from a branch → `main` /
`(root)`**. The site is live a minute or two later.

Verify both URLs load in a browser before you submit — App Review checks them.

## If the URL ever changes

The app reads it from **one** place, `src/config/links.ts`:

```ts
export const SITE_ORIGIN = 'https://evanxue-debug.github.io/apex-site';
```

Change that line and the paywall and Settings screens follow.
`src/config/__tests__/links.test.ts` pins the resulting URLs, so update the
expectations there too.

## Where the URLs are used

| Page | Where it appears |
|---|---|
| Privacy | Paywall footer, Settings → About, App Store Connect app record |
| Terms | Paywall footer, Settings → About, App Store Connect subscription metadata |

App Store Connect asks for the privacy policy URL on the app record, and for a
terms (EULA) URL on the subscription group. Both must resolve publicly *before*
you submit, or review will reject the build.
