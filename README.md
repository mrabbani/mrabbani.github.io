# mrabbani.github.io

Personal portfolio of **Md. Mahbub Rabbani** — CTO at [weLabs](https://welabs.dev), Dokan Plugins Tech Lead at [weDevs](https://wedevs.com).

Live site: **https://mrabbani.github.io/**

## Structure

| File | Purpose |
|---|---|
| `index.html` | Single-file portfolio (HTML + inline CSS/JS, no dependencies) |
| `404.html` | Custom not-found page |
| `.nojekyll` | Skip Jekyll processing on GitHub Pages |
| `robots.txt` | Search engine rules |
| `sitemap.xml` | Sitemap for crawlers |
| `CNAME` | Custom domain (empty — fill in if/when you point a domain) |

## Local preview

```bash
# Python
python3 -m http.server 8080

# or Node
npx serve .
```

Open <http://localhost:8080>.

## Deploy

See [`DEPLOY.md`](./DEPLOY.md).

## Stack

- Plain HTML5, modern CSS (custom properties, color-mix), tiny vanilla JS
- Zero external assets — no fonts, frameworks, or CDNs

## License

Source code: MIT. Content (résumé, project descriptions): © Md. Mahbub Rabbani.
