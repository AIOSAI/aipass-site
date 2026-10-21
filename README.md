# aipass-site

**The AIPass landing page** — the static marketing site for
[AIPass](https://github.com/AIOSAI/AIPass), a persistent agent workspace.

Plain HTML, CSS, and JavaScript. **No build step, no framework, nothing to
install** — there is no `package.json`, no bundler config, and no `Makefile` in
this repo. Open `index.html` and you are looking at the site.

---

## Quick Start

```bash
# Clone it
gh repo clone AIOSAI/aipass-site
# (plain git works too: the remote is https://github.com/AIOSAI/aipass-site.git)
cd aipass-site

# Just open the file
xdg-open index.html                  # macOS: open index.html

# Or serve it, if you want real paths and no file:// quirks
python3 -m http.server 8000          # then visit http://localhost:8000
```

Edit `index.html`, save, reload the browser. That is the whole loop.

---

## What's in here

```
index.html           # the landing page — 327 lines, the whole site
logo-preview.html    # branding scratch page: wordmark + fingerprint SVGs side by side
css/
  index.css          # 818 lines — design tokens, components, both themes
  tablet.css         # 62 lines
  mobile.css         # 108 lines
  pricing.css        # 74 lines — unused, see Loose Ends
js/
  main.js            # 20 lines — mobile nav toggle, nothing else
  pricing.js         # 38 lines — unused, see Loose Ends
fonts/               # Inter (variable woff2 + italic), JetBrains Mono (variable ttf)
images/              # AIPass wordmark, fingerprint, favicon set + unused template assets
vendor/              # Font Awesome 6.7.2 (css + webfonts), vendored — no CDN
src/aipass_site/     # the AIPass agent that maintains this repo
LICENSE              # MIT — Evil Martians, from the upstream template
```

`index.html` loads `index.css`, `tablet.css`, `mobile.css`, and `main.js`.
Nothing else is wired in.

---

## The page

One page, six sections, in order:

1. **Hero** — "AI agents that remember, collaborate, and never start from zero,"
   with the two-line install snippet (clone → `./aipass install`)
2. **What you get** — three cards: Persistent Memory, Agent Coordination,
   Your CLI / Your Subscription
3. **How it works** — three steps: Clone and install → Say hi → Scale up
4. **Bring your own project** — the pitch for any codebase, beside a code block
   showing the directory tree `aipass init` creates
5. **FAQ** — five accordion items: CLI providers, platforms, "do I need all 18
   agents", how it differs from CrewAI/LangChain, and is it free
6. **CTA** — the install snippet again, plus GitHub and r/AIPass buttons

Outbound links point to `github.com/AIOSAI/AIPass`, `pypi.org/project/aipass/`,
`reddit.com/r/AIPass`, X, Bluesky, Hacker News, and dev.to.

No "Lorem ipsum" or placeholder copy remains in `index.html`.

---

## Theming

Colors are CSS custom properties in `css/index.css` — 55 `--color-*`
declarations in total.

- `:root` (line 25) holds the **light** palette — the default, 36 declarations.
- `.theme-dark` (line 150) overrides it for the **dark** palette, 19 declarations.
- `index.html` ships with `<html lang="en" class="theme-dark">`, so the live
  page is dark. Remove that class to get the light theme.

To reskin, edit the `--color-*` values in those two blocks. The upstream
template's palette tool still works for generating a matched light/dark pair:
<https://codepen.io/romanshamin/full/QwWgNLN>

---

## Deploying

Static files, so any static host works — Netlify, Vercel, GitHub Pages,
Firebase, Cloudflare Pages, or a plain web server. Upload the repo contents;
there is nothing to compile.

The live site is **<https://aipass.ai>**, served by **GitHub Pages from the
`main` branch** of `AIOSAI/aipass-site`. The `CNAME` file at the repo root
holds the custom domain (`aipass.ai`); a push to `main` is a deploy. There is
no build workflow — no `.github/workflows/`, `netlify.toml`, or `vercel.json` —
because Pages serves the files as they are. The Pages source branch is a
GitHub repository setting, not a file in this tree.

---

## Loose ends

Honest inventory, none of it fixed:

- **`css/pricing.css` and `js/pricing.js` are orphans.** No HTML file in the
  repo references either one — there is no pricing page. Both are template
  leftovers.
- **Unused image assets ship with the repo:** `demo.gif` (4.0 MB),
  `placeholder-feature.png`, `placeholder-feature-4-3.png`,
  `placeholder-feature-16-9.png`, `placeholder-main-ui.png`, `logo-1/2/3.png`,
  `Logo-Template.svg`, `aipass-banner.png`, `aipass-fingerprint-256.png`,
  `aipass-wordmark-traced.svg`, and `images/favicon/favicon.png`. Nothing links
  to them. The first six are upstream template assets; the AIPass-branded ones
  appear to be alternates kept from the branding pass.
- **`.gitignore.txt`** is a stray second ignore file — a Node/Vite-flavoured
  list that git does not read. The real one is `.gitignore`.
- **`LICENSE` carries only the Evil Martians copyright** (see below). There is
  no separate AIPass copyright notice in the repo, though the page footer
  displays "© 2026 AIPass".

---

## Agent workspace

`src/aipass_site/` holds **AIPASS_SITE**, the resident AIPass agent for this
repo. See [`src/aipass_site/aipass_site/README.md`](src/aipass_site/aipass_site/README.md)
for what it does and how to talk to it.

---

## License and attribution

MIT — see [`LICENSE`](LICENSE).

This site is built on **[LaunchKit](https://launchkit.evilmartians.io)**, the
open-source landing page template by
**[Evil Martians](https://evilmartians.com)**. The `LICENSE` file in this repo
is LaunchKit's MIT license, `Copyright (c) 2025 Evil Martians`, retained as that
license requires. The page footer credits LaunchKit as well.

The AIPass copy, branding, and page structure in `index.html` are original work;
the CSS framework, fonts, and layout system come from the template.

---

*Last Updated: 2026-10-21*
