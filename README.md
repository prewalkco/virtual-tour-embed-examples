# virtual-tour-embed-examples

Copy-paste patterns for embedding a **360° virtual tour** on any website: responsive sizing, lazy loading, click-to-load, fullscreen and VR permissions, Content Security Policy, and notes for WordPress, Webflow, Framer, Squarespace and Wix.

Written and maintained by **[Prewalk](https://prewalk.co)**, 360° virtual tour software for real estate and architecture. The patterns use a plain `<iframe>`, so they work with any viewer, and they are tested with [Prewalk](https://prewalk.co) tours. Don't have a tour yet? [Create one free at prewalk.co](https://prewalk.co): upload 360° photos or renders and get an embed code in minutes.

## Contents

| File | Pattern |
| --- | --- |
| [`examples/responsive.html`](examples/responsive.html) | Responsive iframe with `aspect-ratio`, taller on phones |
| [`examples/click-to-load.html`](examples/click-to-load.html) | Poster image that loads the tour only when clicked (fast pages, good Core Web Vitals) |
| [`examples/Tour360.jsx`](examples/Tour360.jsx) | Small React component with the same behaviour |
| [`examples/csp.md`](examples/csp.md) | Content Security Policy for sites that embed tours |
| [`prewalk/`](prewalk/README.md) | Prewalk reference: tour, project and portfolio embed codes, URL options, allowed sites, passwords, what each plan shows, privacy |

## The minimum that works

```html
<!-- YOUR_TOUR_EMBED_URL: on prewalk.co open the tour → Share → Embed on your website -->
<div class="tour">
  <iframe
    src="YOUR_TOUR_EMBED_URL"
    title="Apartment 3B: 360° virtual tour"
    loading="lazy"
    allow="fullscreen; xr-spatial-tracking; gyroscope; accelerometer"
    allowfullscreen></iframe>
</div>

<style>
  .tour { aspect-ratio: 16 / 9; }
  .tour iframe { width: 100%; height: 100%; border: 0; display: block; }
  @media (max-width: 600px) { .tour { aspect-ratio: 4 / 5; } } /* taller on phones */
</style>
```

Why each attribute is there:

- **`title`**: screen readers announce it; describe the property, not "iframe".
- **`loading="lazy"`**: the tour does not load until it is near the viewport.
- **`allow="fullscreen"` + `allowfullscreen`**: without them the fullscreen button does nothing.
- **`xr-spatial-tracking`**: needed for the VR button (WebXR) to work inside an iframe, for example on Meta Quest.
- **`gyroscope; accelerometer`**: lets phones look around by moving the device, where the viewer supports it.
- **`aspect-ratio`** instead of a fixed height: the tour scales with the column and never collapses to 0 px.

## Common gotchas

| Symptom | Cause | Fix |
| --- | --- | --- |
| Tour is a thin strip or invisible | Iframe has no height | Give the wrapper an `aspect-ratio` or explicit height |
| Fullscreen button does nothing | Missing `allow="fullscreen"` / `allowfullscreen` | Add both |
| VR button missing inside the iframe | Missing `xr-spatial-tracking` | Add it to `allow` |
| Page scroll gets stuck on the tour on phones | Viewer captures one-finger drags | Use a two-finger navigation option if your viewer has one, or the click-to-load pattern |
| "Refused to frame" in the console | Your CSP or the tour's embed settings block it | See [`examples/csp.md`](examples/csp.md); check the tour's allowed domains |
| Page is slow on mobile | Several tours load at once | Use `loading="lazy"` or click-to-load |

## Website builders

- **WordPress (Gutenberg):** add a *Custom HTML* block and paste the embed code. Some security plugins strip `<script>`; use the iframe-only code there.
- **Webflow:** add an *Embed* element, paste the code, and set the wrapper width to 100%.
- **Framer:** use the *Embed* component with *HTML* mode and paste the code.
- **Squarespace:** add a *Code* block (not a Text block) and paste the code.
- **Wix:** use *Embed code → Embed HTML*, choose *Code*, then resize the element; Wix places iframes in a fixed box.

## Prewalk notes

- Full reference: [`prewalk/`](prewalk/README.md) (embed addresses, options, allowed sites, passwords, plans, privacy; last verified 25 November 2026).
- In the Prewalk studio, open a tour's **Share** tab and click **Copy code** under **Embed on your website**.
- The **recommended** code is an iframe plus a small script from prewalk.co: portfolio and project embeds grow to fit their content, and portfolio items open full screen on your site. The **fixed-height** code is the iframe alone, for builders that strip scripts.
- Embed options include theme (match visitor, light or dark), credits, two-finger navigation on phones and, on Pro and above, an accent color.
- Owners can turn embedding off (their embeds then show a "not available" card) and, on Pro and above, allow only specific sites.
- Step-by-step guide: [Embed a tour on your website](https://prewalk.co/blog/embed-on-your-website). Developer write-up: [iframe vs script, sizing and the gotchas](https://dev.to/prewalk/embedding-a-360-virtual-tour-on-any-website-iframe-vs-script-sizing-and-the-gotchas-436a).

## About

Maintained by [Prewalk](https://prewalk.co), 360° virtual tour software for real estate and architecture. Prewalk turns 360° photos and 3D renders into tours buyers walk room by room from one link, in the browser on phones, computers and Meta Quest.

MIT licensed. Pull requests with patterns for other builders are welcome.
