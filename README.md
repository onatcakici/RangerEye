# RangerEye — static site

Static build of rangereye.org, mirrored from the live Google App Engine deployment on 2026-07-16, then SEO-hardened for GitHub Pages. Vite/React SPA, no server code.

## Project record

Official publication: [RangerEye: Autonomous Wildfire Detection and Patrol Drone](https://repository.fit.edu/apss_student/46/), Florida Institute of Technology, Northrop Grumman Engineering & Science Student Design Showcase, May 5, 2025.

Authors: Onat Cakici, John Munday, Mitchell Lacle, Manuel Villamor, Otto Dorschner, Yuto Imai, Ishaben Trada, Abdulrahman Almutairi, Abdullah Alaskar.

## How routing works on GitHub Pages

Each route has a real HTML file (`team.html`, `thesis.html`, `ranger.html`, `resources.html`). GitHub Pages serves `/team` from `team.html` with HTTP 200, so every route is crawlable and indexable with its own title, description, canonical, Open Graph tags, and JSON-LD. A small inline script normalizes `/team.html` or `/team/` back to `/team` before the SPA router boots. `404.html` (noindex) catches unknown paths and still boots the SPA. `specs.html` replicates the live server's `/specs -> /ranger` redirect.

## Hosting requirement

All asset paths are root-absolute (/assets/...), so the site must be served from a domain root. Two options:

1. Name the repo `<username>.github.io` and it works at https://<username>.github.io as-is.
2. Use any repo name and attach the custom domain (rangereye.org) in Settings > Pages. Add a CNAME record at your DNS pointing www to `<username>.github.io`, plus A records for the apex (185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153).

A plain project page at `<username>.github.io/<repo>/` will load the HTML but every asset will 404.

## Deploy

Settings > Pages > Source: deploy from branch, `main`, `/ (root)`. Then check "Enforce HTTPS" once the certificate is issued.

## After deploy: SEO checklist

1. Repo settings: add a description ("Autonomous wildfire detection drone. Florida Tech senior design.") and topics (`wildfire-detection`, `autonomous-drone`, `vtol`, `thermal-imaging`, `florida-tech`, `senior-design`, `uav`). Set the website field to https://www.rangereye.org.
2. Google Search Console: verify the domain (DNS TXT record is easiest, or drop the HTML meta tag where index.html has the VERIFICATION_TAGS_PLACEHOLDER comment) and submit https://www.rangereye.org/sitemap.xml.
3. Bing Webmaster Tools: import from Search Console, one click.
4. Confirm https://www.rangereye.org/team returns 200 (not 404) after DNS cutover. That's the signal the per-route files are being served.
5. Optional: request indexing of / and /team in Search Console to speed up the first recrawl.

## Copyright

© 2023-2026 the RangerEye team, Florida Institute of Technology. All rights reserved.
