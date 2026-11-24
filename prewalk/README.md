# Embedding Prewalk tours, projects and portfolios

A reference for the embed codes [Prewalk](https://prewalk.co) gives you. It covers the three embeds and their addresses, the code and `embed.js`, the URL options and sizing, full screen and VR, who can open an embed and where, what each plan shows, and privacy.

**Last verified: 24 November 2026.** For the step-by-step walkthrough with screenshots, see [Embed a tour on your website](https://prewalk.co/blog/embed-on-your-website). Plans are on the [pricing page](https://prewalk.co/pricing); more answers are in the [FAQ](https://prewalk.co/faq).

Copy-paste page: [`embeds.html`](embeds.html).

## The three embeds

| Embed | Address | Where to get the code |
| --- | --- | --- |
| Tour | `https://prewalk.co/embed/TOUR_ID` | Studio → open the tour → **Share** → **Embed on your website** → **Copy code** |
| Project | Public: `https://prewalk.co/embed/@HANDLE/projects/PROJECT_SLUG`<br>Link-only or password-protected: `https://prewalk.co/embed/p/PROJECT_ID` | Studio → open the project → **Share** → **Embed on your website** |
| Portfolio (your profile) | `https://prewalk.co/embed/@HANDLE` | **Settings → Branding → Embed your portfolio**, or the first panel of any tour's or project's **Share** tab |

The portfolio shows your public tours and projects. A tour that belongs to a public project appears inside that project's card, not as a card of its own. Whatever you publish later appears there by itself.

## The code

The **recommended** code is the iframe plus `embed.js`:

```html
<iframe src="https://prewalk.co/embed/TOUR_ID" title="Apartment 3B" width="100%" height="560" style="border:0;width:100%;max-width:100%" loading="lazy" allow="autoplay; fullscreen; gyroscope; accelerometer; xr-spatial-tracking"></iframe>
<script src="https://prewalk.co/embed.js" async></script>
```

On the Free plan, the code ends with a visible link:

```html
<p style="margin:6px 0 0;font:13px/1.4 system-ui,sans-serif"><a href="https://prewalk.co" target="_blank" rel="noopener">Powered by Prewalk</a></p>
```

What `embed.js` does:

- **Height:** it grows portfolio and project embeds to fit their content, so they never scroll inside. The height in the code is the minimum.
- **Full-screen layer:** it opens a portfolio card in a full-screen layer over your page. **Esc** or **×** closes it, and the visitor never leaves your site.
- **Allowed sites:** on a site that is not allowed, it puts a one-line note in place of the iframe (see [Where an embed can open](#where-an-embed-can-open)).
- **Privacy:** it sets no cookies and stores nothing.
- **One script per page:** it takes care of every Prewalk iframe on the page, including iframes without their own script tag.

The **fixed-height** code is the iframe alone. Use it for site builders that strip scripts; the embed keeps the height you chose (200–4000 px).

## URL options

Add them to the embed address like any query string, e.g. `https://prewalk.co/embed/@HANDLE?layout=carousel&header=0`. The builder on the Share tab and in Branding writes them for you.

| Option | Embeds | Values | Default |
| --- | --- | --- | --- |
| `theme` | all | `auto` (follows the visitor's light or dark setting), `light`, `dark` | `auto` |
| `accent` | all, Pro and above | a hex colour without `#`, e.g. `accent=0a7cff`; ignored on Free | your colour from Branding |
| `credits=0` | tour, project | hides the credits | shown |
| `twofinger=1` | tour, project | on phones one finger scrolls your page and two fingers move the tour | off |
| `header=0` | portfolio | hides the profile header (avatar, name, buttons) | shown |
| `layout` | portfolio | `grid`, `carousel` | `grid` |
| `limit` | portfolio | items shown before **Show more**, 1–48 | `12` |
| `type` | portfolio | `all`, `tours`, `projects` | `all` |
| `category` | portfolio | `real-estate`, `hospitality`, `architecture`, `interior`, `venues`, `other` | every category |
| `tag` | portfolio | one tag | every tag |
| `project` | portfolio | a public project's slug: only that project's public tours | everything |

## Size

- **Width:** every Prewalk embed is 100% wide.
- **Tour height:** a tour embed keeps the height from the code. For a shape that follows the column, put the iframe in a wrapper with `aspect-ratio`, as in [`../examples/responsive.html`](../examples/responsive.html). The player fills the wrapper.
- **Portfolio and project height:** with `embed.js` they grow to fit their content, so set the code's height to the smallest height you want. Without the script they keep the code's height and scroll inside.

## Full screen and VR

Every Prewalk embed code carries `allow="autoplay; fullscreen; gyroscope; accelerometer; xr-spatial-tracking"`. Keep it when you paste the code:

- **`fullscreen`:** the player's full-screen button works inside your page, on every plan.
- **`xr-spatial-tracking`:** the VR button works inside the iframe. The button appears only in browsers that support WebXR immersive VR, such as the Meta Quest browser; desktop and phone browsers show no VR button.
- **`gyroscope; accelerometer`:** phones can look around by moving the device.
- **`autoplay`:** the tour's sound autoplay setting gets its chance; the browser may still wait for a tap.

Prewalk's code has no `allowfullscreen` attribute: the `allow` list already grants full screen, and the old attribute next to it only logs a console warning.

In full screen the brand stays in the top left corner: the «prewalk.co» badge on Free, and your logo (or your name, without a logo) on Pro and above.

## Who can open an embed

| Visibility | Can it be embedded? | Shown in the portfolio embed? |
| --- | --- | --- |
| Public | Yes | Yes |
| Link-only | Yes, with its embed code | No |
| Password-protected (Pro and above) | Yes. The password is asked inside the embed. | No |

- **Tour password:** the password is checked by prewalk.co and nothing is stored: no cookie, no storage. Reloading the page asks again.
- **Project password:** one password opens the project and every tour in it. The tours do not ask again.

## Where an embed can open

**Allowed sites** (Settings → Branding, Pro and above). List up to 20 host names, one per line:

- `example.com`, or `*.example.com` for its subdomains (this does not cover `example.com` itself).
- Only `https` pages on those hosts can show your embeds.
- An empty list means everywhere.
- Prewalk's own pages can always show them.

On any other site:

- With the recommended code, `embed.js` puts the line *This content can't be shown on this site.* in place of the iframe, in the visitor's language.
- With the iframe-only code, the browser refuses the frame and shows its own error page.
- The protection itself is the `frame-ancestors` header of the embed, so it holds even without the script.

**Allow embedding** (Settings → Branding, every plan). When it is off:

- Every embed of your profile, projects and tours on another site shows a plain *not available* card instead of your content.
- Prewalk's own pages keep the player.
- Tour links (`https://prewalk.co/t/…`) keep working when opened directly.

## What each plan shows

| | Free | Pro and above | Enterprise on its own domain (white-label) |
| --- | --- | --- | --- |
| Prewalk badge | «prewalk.co» at the top left: first in the tour's bar, over the corner of a project's cover, above the portfolio header. It links to prewalk.co in a new tab. | None | None |
| «Powered by Prewalk» line under the code | Yes | No | No |
| Your logo and accent colour (Settings → Branding) | No | Yes | Yes |
| **Get in touch** in the embed (contact form, optional WhatsApp and phone) | No | When turned on | When turned on |
| Prewalk name and «Open on prewalk.co» | Yes | Yes | No; the embed and its links stay on your domain |
| **Report** link | Yes | Yes | Yes |

## Privacy

- **No cookies or storage:** embeds set no cookies and use no localStorage or sessionStorage.
- **No third parties:** an embed loads only from `prewalk.co` and `cdn.prewalk.co`.
- **View counting:** views are counted on Prewalk's server without cookies. A tour embed counts a view at the visitor's first interaction (drag, tap or button), not when your page loads.
- **Reporting:** every embed has a **Report** link.

If your site sends a Content Security Policy, allow `https://prewalk.co` in `frame-src` (and in `script-src` for `embed.js`), as in [`../examples/csp.md`](../examples/csp.md).

## Troubleshooting

| You see | Why | Fix |
| --- | --- | --- |
| *This content can't be shown on this site.* | The owner's allowed sites do not include this page's host, or the page is not `https` | Add the host in Settings → Branding → Allowed sites |
| A *not available* card | **Allow embedding** is off, or the tour or project no longer exists | Turn **Allow embedding** on in Settings → Branding |
| The browser's own "refused to connect" page | The iframe-only code on a site that is not allowed | Add the site to the allowed sites |
| A blocked frame and "Refused to frame" in the console | Your site's Content Security Policy | Allow `https://prewalk.co` in `frame-src` ([`../examples/csp.md`](../examples/csp.md)) |
| A portfolio or project embed scrolls inside | `embed.js` is missing (some builders remove scripts) | Use the recommended code, or give the fixed-height code more height |
| The full-screen button does nothing | The `allow` attribute was removed | Paste the code unchanged |
