# Bored Panda Group — email signatures

A static site. No build step, no server, no dependencies.

```
index.html              the generator people use
boredpanda-sig-2x.png   logos, referenced by index.html
spike-sig-2x.png
studios-sig-2x.png
```

## Deploying

1. Push these four files to the root of a repository.
2. Repo **Settings → Pages → Source: Deploy from a branch**, branch `main`,
   folder `/ (root)`.
3. Wait a minute, then open the published URL.

The published site is public even if the repository is private — which is
required here, since mail clients must be able to fetch the logos without
signing in. Pages from a private repo needs a paid GitHub plan; a public repo
works on any plan.

## Why there is no URL to configure

`index.html` resolves logo paths against its own location at runtime. Deploy it
anywhere and the signatures it generates point at the right place. Move the
site and newly generated signatures follow automatically.

## Changing a logo

**Add a new file, don't overwrite an existing one.** Mail clients and image
proxies cache aggressively, so overwriting can show old and new versions to
different people for a long time — including in emails sent months ago, because
images are fetched when a message is opened, not when it was sent.

Add `name-sig-v2-2x.png`, update the `COMPANIES` list in `index.html`, keep the
old file in place.

## Editing the templates

Everything lives in `index.html`. The `COMPANIES` array near the top of the
script holds each company's logo file, display size, and whether it carries the
"part of Bored Panda Group" line. The `build()` function immediately below is
the signature markup itself.

Two rules if you edit it:

- **Inline styles only.** No `<style>` block, no classes, no media queries.
  Gmail strips them.
- **Never set a background colour.** That is what makes the signature survive
  dark mode. The logos carry their own light edge instead.

Logo display sizes are 163×34, 129×40 and 79×44. They differ on purpose — the
three marks have very different proportions, and matching them by height would
make Spike unreadable and boredpanda.com overbearing.

## Adding a company

Add an entry to `COMPANIES`. A company without a logo yet uses `wordmark`
instead of `img`, and gets its name typeset at the weight a logo would carry —
see Panda Ventures. Swapping in a real logo later needs no layout change.

## Known limitation

The Gmail mobile app only supports plain-text signatures. The generator
provides a plain version for that; there is no way to use the HTML one there.
