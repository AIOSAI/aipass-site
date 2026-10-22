# aipass-site

**The AIPass website**: the static site at <https://aipass.ai> for
[AIPass](https://github.com/AIOSAI/AIPass). It says what AIPass does for a
developer, how to install it, what BAUD is, and where the docs live.

Plain HTML and CSS. **No build step, no framework, no JavaScript, nothing to
install.** Every font and image the pages load is in this repo, so there are no
CDN, font or script calls to outside hosts.

---

## Quick Start

```bash
# Clone it
gh repo clone AIOSAI/aipass-site
# (plain git works too: the remote is https://github.com/AIOSAI/aipass-site.git)
cd aipass-site

# Serve it, so the links between pages resolve as they do live
python3 -m http.server 8000          # then visit http://localhost:8000
```

Edit a page, save, reload the browser. That is the whole loop.

---

## What's in here

```
index.html           # Home: the promise, what it does, your machine on any device, BAUD, FAQ, install
install.html         # Requirements, the two install commands, what install changes, containers, uninstall
baud.html            # BAUD, the phone face: four screenshots, what it needs, pairing, how to get it
docs.html            # A curated index of links into the real docs on GitHub; nothing is copied
css/index.css        # The one stylesheet: theme tokens, layout, every component
fonts/               # Inter (variable woff2), JetBrains Mono (variable ttf)
images/              # AIPass wordmark, banner, fingerprint, favicon set; baud/ holds the BAUD screenshots
logo-preview.html    # Branding scratch page, not linked from the site
CNAME                # aipass.ai
src/aipass_site/     # The AIPass agent that maintains this repo
LICENSE              # MIT
```

Each page carries its own title, description, canonical link and Open Graph
tags. The header and footer are the same block copied into all four pages; the
only difference is `aria-current="page"` on the current page's nav link. A
change to either block goes into all four files.

---

## The design

Paper and a screen. The site is light grey-green paper; it turns dark only
where a BAUD screenshot is shown (the Home hero, the BAUD strip, the BAUD
gallery), so dark always means "this is the phone's screen". Headings sit in a
left rail on wide screens and above their text on phones.

All colors, faces and sizes are custom properties in the `:root` block of
`css/index.css`; no rule below it uses a literal color. The main ones:

| Token | Value | Role |
|-------|-------|------|
| `--paper` | `#e9ede8` | Page ground |
| `--ink` | `#16201b` | Text, rules, the primary button |
| `--ink-soft` | `#47554d` | Secondary text |
| `--screen` | `#0c110e` | The dark bands, sampled from BAUD |
| `--signal` | `#1c6b42` | Links and focus on paper |
| `--phosphor` | `#5bd68e` | Links, focus and buttons on the dark bands |

Inter sets all text; JetBrains Mono sets only commands. The one motion is the
FAQ's plus turning into a cross, and `prefers-reduced-motion` turns it off.

---

## Deploying

The live site is **<https://aipass.ai>**, served by **GitHub Pages from the
`main` branch** of `AIOSAI/aipass-site`. The `CNAME` file at the repo root
holds the custom domain (`aipass.ai`); a push to `main` is a deploy. There is
no build workflow (no `.github/workflows/`, `netlify.toml` or `vercel.json`)
because Pages serves the files as they are. The Pages source branch is a
GitHub repository setting, not a file in this tree.

---

## Loose ends

- **Unused brand alternates** sit in `images/`: `aipass-combo.svg`,
  `aipass-wordmark-traced.svg` and `aipass-fingerprint-256.png`. No page links
  to them; `logo-preview.html` shows some of them and also points at image
  files on a local disk, so it renders only partly from a clone.
- **`LICENSE` carries only the Evil Martians copyright** from the LaunchKit
  template the site began from. There is no separate AIPass copyright notice.

---

## Agent workspace

`src/aipass_site/` holds **AIPASS_SITE**, the resident AIPass agent for this
repo. See [`src/aipass_site/aipass_site/README.md`](src/aipass_site/aipass_site/README.md)
for what it does and how to talk to it.

---

## License and attribution

MIT, see [`LICENSE`](LICENSE).

The site began from **[LaunchKit](https://launchkit.evilmartians.io)**, the
open-source landing page template by **[Evil Martians](https://evilmartians.com)**.
The `LICENSE` file is LaunchKit's MIT license, `Copyright (c) 2025 Evil
Martians`, kept as that license requires. The markup, stylesheet, copy and
images that ship now are AIPass's own; the vendored Inter and JetBrains Mono
fonts carry their own open licenses.

---

*Last Updated: 2026-10-21*
