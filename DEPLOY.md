# Deploy guide — mrabbani.github.io

GitHub Pages serves any static site pushed to the `main` branch of a repo named **`<username>.github.io`**. This folder already contains everything that repo needs.

## 1. Create / use the repo

If `mrabbani/mrabbani.github.io` doesn't exist yet, create it on GitHub as a **public** repository (no template, no README — this folder already has one).

## 2. Push these files

From inside the `mrabbani.github.io/` folder:

```bash
git init
git branch -M main
git add .
git commit -m "Initial portfolio"
git remote add origin git@github.com:mrabbani/mrabbani.github.io.git
git push -u origin main
```

If you already cloned the repo, just copy the files into the working tree and commit/push.

## 3. Enable Pages (usually automatic)

For a user site (`<username>.github.io`), Pages is enabled by default on `main` / root.
To verify: **Repo → Settings → Pages** should show "Your site is live at https://mrabbani.github.io/".

If it isn't:
- Set **Source** to `Deploy from a branch`
- Branch: `main`, folder: `/ (root)`
- Save and wait ~30 seconds for the first build.

## 4. (Optional) Custom domain

1. Add your domain (e.g., `mahbub.dev`) to the `CNAME` file at the root of this repo (one line, no protocol).
2. At your DNS provider, add the GitHub Pages records:
   - `A` records for the apex pointing to:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
   - `CNAME` for `www` → `mrabbani.github.io`
3. In **Settings → Pages**, enter the same domain and tick **Enforce HTTPS** once the cert is issued.

## 5. Updating

```bash
# edit index.html …
git add index.html
git commit -m "Update portfolio"
git push
```

GitHub usually deploys within a minute. Check **Actions** tab for build status.

## Sanity checks

- [ ] Visit https://mrabbani.github.io/ and confirm the page loads.
- [ ] Click each nav link — anchors should scroll to the right sections.
- [ ] Try a bogus path (e.g., `/foo`) — the custom 404 should render.
- [ ] Run `curl -I https://mrabbani.github.io/sitemap.xml` — expect HTTP 200.
