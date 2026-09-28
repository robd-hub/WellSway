# Handover: WellSway Dance Studio website

**From:** Claude (Cowork session with Rob, DesignImp)
**Date:** 28 September 2026
**Status:** Design and content agreed; ready to move into GitHub and Vercel. Waiting on Justyna's photos and a domain before public launch.

---

## 1. Where things stand

The site is a finished single-page static website (`index.html`) in green and gold, matching Justyna's teal velvet dress. It's been through several rounds of feedback from Rob and is in a state he's happy with.

**Previews made during the Cowork session** (private claude.ai pages, for reference only; this repo is now the source of truth):

- Main site (latest, v16): https://claude.ai/artifact/5rWCDhX1V7tkHihECZiyaz
- Font lab (four font options compared; "Current" was chosen): https://claude.ai/artifact/WCbBBQULTp6fJnfiwiN6Uj
- Older "Saturday-night ballroom" alternative, not chosen: https://claude.ai/artifact/EaAeaP98tV89GV3r2oHpo9

The preview pages differ slightly from this repo because the preview host can't embed maps or send emails. **This repo's `index.html` is the production version**: it has the real Google Maps iframe and the working mailto enquiry form.

---

## 2. How we got here (decisions and why)

| # | Decision | Reason |
|---|---|---|
| 1 | Started from Rob's navy and gold mockup (`wellsway-mockup.html`) | First concept for Justyna |
| 2 | Tried a "Saturday-night ballroom" theme (mirror ball, spotlights, score paddles) | Rob asked for a Strictly Come Dancing feel. Built without BBC branding. Not chosen. |
| 3 | **Rebuilt in green and gold** from Justyna's photo, with her real timetable, dances and bio | Rob's direction: modern, fun, easy to navigate, attract new attendees |
| 4 | WhatsApp is the main booking route (every class row, hero, floating button, mobile tab bar) | Most UK local-class enquiries come via WhatsApp |
| 5 | Added Messenger and Facebook page links | Rob's request |
| 6 | Added "Coming to your first class" steps, Salsa Fit spotlight and parents' section | Reduce beginner nerves; Salsa Fit targets a different audience; parents need reassurance |
| 7 | Showed prices: £10 for adult classes; kids = "Ask" | Rob confirmed £10 for all adult classes |
| 8 | Showed DBS, IDTA, first aid, insured | Confirmed by Rob |
| 9 | Replaced the 4/4 time signatures and tempos with a 1–5 energy meter | Too technical for beginners |
| 10 | Tested four font pairings | Rob preferred the current one (Bricolage Grotesque / Plus Jakarta Sans / Great Vibes) |
| 11 | "Less AI-looking" pass: script accents only in hero and About, removed most eyebrow labels, turned card grids into a timetable list, numbered list, timeline and trust panel, rewrote copy in Justyna's first person, removed the perks strip | Rob felt parts looked templated |
| 12 | Removed: eyebrow dashes, the Google badge on her photo, both feather decorations, the drop-cap "D" | Rob's requests |
| 13 | Contact section kept as separate cards (call, email, WhatsApp, Facebook page, Messenger, address, map) | Rob preferred this to the combined list |
| 14 | First FAQ item open by default | Shows the list expands; answers the biggest beginner worry. Rob OK'd it. |

---

## 3. Open items (priority order)

### Needed from Justyna / Rob
- [ ] **Photos**: class/action shots (with permission), a junior competition photo, the hall. Biggest remaining improvement. Suggested spots: timetable (small thumbnails or a photo band above it), Salsa Fit section, parents section, About timeline, and opening up the "Ten dances" section.
- [ ] **Domain**: e.g. `wellswaydance.co.uk` (Rob sorting).
- [ ] **Kids' class price** (currently "Ask") and **end time** (currently "9:00am" only). Update the row's `data-end` too.
- [ ] **Confirm the Facebook URL**: currently `profile.php?id=100071256626333`. If she has a vanity URL (facebook.com/…), swap it everywhere, including the `m.me/` Messenger links and JSON-LD `sameAs`.
- [ ] **Energy meter ratings** (1–5 per dance) are Claude's judgement. Ask Justyna to check.
- [ ] Ask Justyna to **rename her Google Business Profile** from "Ballroom and Latin Dance Academy" to "WellSway Dance Studio" and add the website URL. Consistent name, address and phone helps local SEO.

### Technical, once the domain exists
- [ ] Change `og:image` to an **absolute URL** (`https://<domain>/og-image.jpg`). Facebook and WhatsApp ignore relative paths.
- [ ] Add `<link rel="canonical" href="https://<domain>/">` and `og:url`.
- [ ] Add `robots.txt` and `sitemap.xml` (single URL).
- [ ] Put the website URL in JSON-LD (`"url"`).
- [ ] Add the domain in Vercel → Project → Settings → Domains, and set DNS at the registrar.
- [ ] Submit to **Google Search Console**. Check the Rich Results Test for `LocalBusiness` and `FAQPage`.
- [ ] Optional: **Vercel Web Analytics** (one script tag) so Justyna can see visitor numbers.

### Code tidy-up (safe to do any time)
- [x] **Removed unused CSS** left from earlier iterations (72 rules; checked against the HTML and JS, layout unchanged at 390px and 1280px).
- [x] Compressed the share image: now `og-image.jpg` (145 KB, was a 577 KB PNG). Meta tags updated.
- [ ] Convert `justyna.jpg` to WebP with a JPG fallback (`<picture>`) when new photos arrive.

### Nice to have (discussed, not yet requested)
- [ ] A **first-class offer** ("First class free" or "£5 taster"), shown in the hero and timetable. The single most effective conversion idea.
- [ ] A short "Justyna usually replies the same day" line near the contact options.
- [ ] Replace the mailto form with a real form service if Justyna wants enquiries without the visitor's email app opening.

---

## 4. Moving this into GitHub and Vercel

1. **Create the repo**: *local git is already set up on `main` with the first commits; only the GitHub repo, `git remote add` and `git push` remain.* On GitHub, make a new repo (e.g. `wellsway-site`, private or public). In this folder:
   ```bash
   git init
   git add .
   git commit -m "WellSway Dance Studio site: initial handover"
   git branch -M main
   git remote add origin git@github.com:<your-username>/wellsway-site.git
   git push -u origin main
   ```
2. **Connect Vercel**: vercel.com → Add New → Project → import the GitHub repo.
   - Framework preset: **Other**
   - Build command: *(leave empty)*
   - Output directory: **`.`** (root)
   - Deploy. You'll get a `*.vercel.app` URL straight away.
3. **Workflow from then on**: work in Antigravity with Claude Code, commit, push to `main`, and Vercel deploys automatically. Use a branch plus pull request to get a preview URL to show Justyna before merging.
4. **Custom domain**: Vercel → Project → Settings → Domains → add the domain → follow the DNS instructions (A record `76.76.21.21` for the apex, CNAME `cname.vercel-dns.com` for `www`, or use Vercel nameservers). Then complete the "Technical, once the domain exists" list above.

---

## 5. Things to watch out for

- **Facts are repeated** in visible text, WhatsApp messages and JSON-LD. See "When you change facts" in `CLAUDE.md`.
- **The next-class logic** uses UK time and the `data-*` attributes on `.tt-row`. The Saturday class has no end time, so the code assumes 60 minutes.
- **The enquiry form** only works if the visitor has an email app set up (mailto). WhatsApp is the main route by design.
- **The Google Maps iframe** uses the lat/long pin (`53.2243215,-0.4644892`); the "Get directions" links use the Google listing's CID URL.
- **Reviews are real** (Irene Nicholson, Chris Hood; a third, from Aimee Gray, is stars only). Don't edit them. Add new ones only by copying real Google reviews word for word.
- **The og-image** shows the timetable. Regenerate it if class days change.

---

## 6. Contacts

- **Client:** Justyna Wells · 07753 612174 · justynawells13@gmail.com
- **Designer:** Rob, DesignImp · www.designimp.com
