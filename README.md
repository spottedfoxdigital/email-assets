# Email Assets — Spotted Fox Digital

Public, CDN-served home for **client email-signature assets**: logo files, email-optimized
PNGs, and the HTML signatures that reference them. Images are served through
**jsDelivr** straight from this repo, so signatures pasted into Outlook / Gmail load a
stable `https://` image instead of an attachment or a base64 blob.

## Public on purpose

jsDelivr only serves **public** GitHub repos, so this repo is public by design.
Only commit things that are already public-facing:

- ✅ Client logos / brand marks the client already shows publicly, email-sized PNGs, signature HTML
  (name, title, business phone, address, links — the same details recipients already see).
- ❌ No credentials, API keys, invoices, contracts, client documents, brand-guideline PDFs,
  internal notes, personal cell numbers the person hasn't OK'd, or third-party logos we don't have rights to.

## Structure

```
clients/
  <client>/                 # one kebab-case folder per client
    README.md               # what's here, source notes, outstanding items
    logos/                  # master logo files (full-res PNG, SVG) - not for direct email use
    email/                  # email-optimized PNGs (2x the display size, small file size)
    signatures/             # paste-ready HTML signatures (+ outlook-steps.md, previews/)
      drafts/               # work in progress - not sent to the client yet
```

Current clients: [`incorvaia`](clients/incorvaia/), [`spotted-fox`](clients/spotted-fox/).

File naming: lowercase kebab-case, `<client>-<asset>-<variant>[-<w>x<h>].png`
(e.g. `incorvaia-logo-email-440x86.png`).

## Referencing images (jsDelivr, pinned)

Always use a **pinned** URL (release tag or commit SHA) in signatures, never a branch:

```
https://cdn.jsdelivr.net/gh/spottedfoxdigital/email-assets@<tag-or-sha>/<path>
```

Example:

```
https://cdn.jsdelivr.net/gh/spottedfoxdigital/email-assets@v1.0.0/clients/incorvaia/email/incorvaia-logo-email-440x86.png
```

- Pinned tag/SHA URLs are cached permanently, so a signature never changes underneath the client.
- Don't use `@main` / `@latest` in signatures — those are cached for up to 7 days and can change.
- To update a logo: add the new file (or a new filename), commit, cut a **new tag**
  (`v1.0.1`, `v1.1.0` …), and regenerate the signature with the new URL. Never move or
  delete a tag that's already in someone's signature.
- jsDelivr may take a minute or two to pick up a brand-new tag; verify with
  `curl -I <url>` → `200` + `content-type: image/png` before sending a signature.

## Email image guidelines

- PNG (or JPG for photos) — **no SVG** in email (Outlook/Gmail don't render it).
- Export at 2× the display size and set `width`/`height` attributes to the display size.
- Keep each image small (< 50 KB ideally). Always include `alt` text.
- Signatures stay mostly live text (tables + inline styles); the logo is the only image.

## Releases

| Tag | Contents |
|---|---|
| `v1.0.0` | Initial assets: Incorvaia logos + email logo, Spotted Fox logos + email icon |
