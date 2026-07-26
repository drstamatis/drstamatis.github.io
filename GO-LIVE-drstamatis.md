# Go-live checklist — drstamatis.com (canonical)

**Canonical site:** `drstamatis.com` → served by GitHub Pages.
**Redirect:** `caitlinstamatis.com` → 301 to `drstamatis.com`.
Both domains registered + DNS managed at **Cloudflare**. The `CNAME` file in this repo already contains `drstamatis.com`.

Do these in order.

## 1. Push the site to GitHub
Your folder is a git repo:
```
git add -A
git commit -m "Rebrand + GEO; canonical drstamatis.com"
git push
```
If there's no remote yet, create a public repo and follow the original `DEPLOY.md`.

## 2. Cloudflare DNS for drstamatis.com (the live site → GitHub Pages)
In the `drstamatis.com` zone, add these. **Set Proxy status to "DNS only" (grey cloud), not proxied** — GitHub needs this to issue the HTTPS certificate; leaving it orange causes cert failures / redirect loops.
```
A      @      185.199.108.153     DNS only
A      @      185.199.109.153     DNS only
A      @      185.199.110.153     DNS only
A      @      185.199.111.153     DNS only
CNAME  www    <your-github-username>.github.io   DNS only
```
(Optional IPv6, also DNS only: AAAA @ 2606:50c0:8000::153 / 8001::153 / 8002::153 / 8003::153)

## 3. Enable GitHub Pages + HTTPS
Repo → **Settings → Pages** → Custom domain = `drstamatis.com` → wait for the green DNS check → tick **Enforce HTTPS**. (DNS can take minutes to a few hours.)

## 4. Redirect caitlinstamatis.com → drstamatis.com (Cloudflare)
Cloudflare has no simple "forward" toggle — you use a Redirect Rule. In the **`caitlinstamatis.com`** zone:
1. Add a placeholder **proxied** record so the rule engine can run:
   ```
   A  @    192.0.2.1   Proxied (orange cloud)
   A  www  192.0.2.1   Proxied (orange cloud)
   ```
2. **Rules → Redirect Rules → Create rule:**
   - **If** — "All incoming requests" (or Hostname contains `caitlinstamatis.com`)
   - **Then** — Type: **Dynamic**, Expression: `concat("https://drstamatis.com", http.request.uri.path)`
   - **Status code:** 301
   - **Preserve query string:** on
This sends `caitlinstamatis.com/anything` → `drstamatis.com/anything` permanently.

## 5. Get indexed (this is what turns the GEO work into citations)
- **Google Search Console** → add `drstamatis.com` → verify with a Cloudflare **TXT** record (GSC gives the value: `TXT  @  google-site-verification=…`) → submit `https://drstamatis.com/sitemap.xml`.
- **Bing Webmaster Tools** → add site (import from GSC) → submit the same sitemap. *(Bing matters because ChatGPT Search pulls from it.)*

## 6. (Later) Substack on writing.drstamatis.com
When you set up the newsletter:
- Substack → Settings → custom domain → enter `writing.drstamatis.com` → pay the one-time $50 → it gives you a target value.
- Cloudflare → add `CNAME  writing  <substack-target>  DNS only (grey cloud)`.
- Point the site's "Writing" nav link to `https://writing.drstamatis.com`.

## 7. Verify it's all live
- Load `https://drstamatis.com/robots.txt`, `/sitemap.xml`, `/llms.txt` — confirm they serve.
- Visit `caitlinstamatis.com` — it should flip to `drstamatis.com`.
- Run the home, About, and Services URLs through Google's **Rich Results Test** (search.google.com/test/rich-results) — expect valid **Person**, **ProfessionalService**, and **FAQPage**.
- A week or two after indexing, ask ChatGPT/Perplexity "Who is Caitlin Stamatis?" and see if the site is cited.

## Already done in the files
Rebrand to Caitlin Stamatis, PhD; Person + ProfessionalService + FAQPage + BlogPosting schema (entity-graph linked via `@id`); `sameAs` to LinkedIn, Google Scholar, ResearchGate, OSF; `workLocation`; canonical + OpenGraph + Twitter + author meta on every page; homepage identity sentence; Services FAQ with licensure (NY, NJ, 40+ PSYPACT states); fixed footer LinkedIn link; linked the on-domain essay + byline/date; static citation counters; robots.txt / sitemap.xml / llms.txt / CNAME.

## Still worth doing later (P1/P2)
Create a free **ORCID** and add it to the schema `sameAs`; publish new evergreen essays natively (or a Substack on `writing.drstamatis.com`); a dedicated **/speaking** page; a **Psychology Today** profile linking back; `ScholarlyArticle`/DOIs on the publications list.
