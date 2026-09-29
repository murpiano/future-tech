![Future Tech](docs/screenshot.jpg)

# Future Tech

A multi-page tech news and resources site: a home page, news, podcasts, resources, a blog and a
contact form. Plain HTML, SCSS and vanilla JavaScript, no framework or build tool beyond Sass.

This is a markup training project, built from a video tutorial from December 2025 to February
2026 to practice layout, responsive design and a small component system in plain JavaScript. The
text and images are the tutorial's placeholder content.

## What you can do

Browse six pages from the header nav: home, news, podcasts, resources, a blog and contacts. Open
the collapsible FAQ-style sections, switch between tabs on pages that have them, play the embedded
videos, and use the contact form's country-code select and masked phone input.

## How it works

### A small component system, no framework

`scripts/BaseComponent.js` is a tiny base class other components extend. It wraps a component's
state in a `Proxy`: assigning to a state property calls the component's own `updateUI()`
automatically, so a component like `Tabs` only has to change `this.state.something` and not call
a render method by hand. Each component reads its root element and its parts from
`data-js-*` attributes (`Header.js`, `Tabs.js`, `Select.js`, `ExpandableContent.js`,
`InputMask.js`, `VideoPlayer.js`), never from classes meant for styling.

### One entry point

`scripts/main.js` is the only script the pages load. It constructs one instance of each
component collection (`new TabsCollection()`, `new SelectCollection()`, and so on), and every
collection finds its own root elements on the page, so a page with no tabs just skips that part
silently.

### Styles

`styles/` holds plain SCSS compiled with the `sass` CLI, no PostCSS or bundler.

## Run locally

```bash
git clone https://github.com/murpiano/future-tech.git
cd future-tech
npm install
npm run sass-watch   # compiles styles/ on save

# then open index.html, news.html, etc. directly, or serve the folder:
npx serve .
```

There is no build step, no tests and no CI. The pages are static HTML, so they run from the
file system or any static server.

## Where things live

```text
scripts/    one file per component (Header, Tabs, Select, VideoPlayer, …) plus main.js
styles/     SCSS source, compiled next to it by sass-watch
images/, icons/, fonts/, videos/   static assets
*.html      one file per page: index, news, podcasts, resources, blog, contacts
```

## Rough edges

- No bundler or minifier: every page loads its scripts and compiled CSS directly, unbundled.
- The contact form has no submit handler; the mask and the country select work, but there is
  nowhere to send the data.
- All article, podcast and resource content is the tutorial's placeholder text and stock images.

---

<sub>[Bogdan Trotsenko](https://github.com/murpiano) · [murpiano](https://github.com/murpiano) · [Telegram](https://t.me/murpiano)</sub>
