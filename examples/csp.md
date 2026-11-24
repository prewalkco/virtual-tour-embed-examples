# Content Security Policy for embedded 360° tours

If your site sends a `Content-Security-Policy` header, the browser blocks any iframe whose origin is not listed in `frame-src`. The console then shows *"Refused to frame … because it violates the following Content Security Policy directive"*.

Add the tour's origin to `frame-src`. For Prewalk tours:

```
Content-Security-Policy: frame-src 'self' https://prewalk.co;
```

If you use the recommended Prewalk embed code (iframe plus a small script), also allow the script:

```
Content-Security-Policy: frame-src 'self' https://prewalk.co; script-src 'self' https://prewalk.co;
```

Merge these with your existing directives rather than replacing them; a second `Content-Security-Policy` header makes the policy stricter, not looser.

## Where to set it

- **Nginx:** `add_header Content-Security-Policy "frame-src 'self' https://prewalk.co;" always;`
- **Apache:** `Header set Content-Security-Policy "frame-src 'self' https://prewalk.co;"`
- **Netlify (`_headers`):** `/*` then `  Content-Security-Policy: frame-src 'self' https://prewalk.co;`
- **Vercel (`vercel.json`):** add the header under `headers` for `source: "/(.*)"`.
- **Next.js:** return it from `headers()` in `next.config.js`.

## The other direction

The tour host can also refuse to be framed (with `frame-ancestors` or an allow-list of domains). In Prewalk, owners can allow only specific sites (Pro and above): on any other site the recommended code shows a one-line "This content can't be shown on this site." in place of the iframe, and the iframe-only code gets the browser's own "refused to connect" page. Owners can also turn embedding off; their embeds then show a "not available" card. Details: [`../prewalk/README.md`](../prewalk/README.md#where-an-embed-can-open).
