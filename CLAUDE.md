# CLAUDE.md: WellSway Dance Studio website

Guidance for Claude Code when working in this repository. Read `HANDOVER.md` for project history, decisions and the open to-do list.

## What this is

A one-page marketing website for **WellSway Dance Studio**, run by dance teacher **Justyna Wells** in Washingborough, Lincoln (UK). The site's single job is to **turn local visitors into new class attendees**: people should quickly see the weekly classes and prices, then book (mainly via WhatsApp).

- Client: Justyna Wells (dance teacher)
- Built and maintained by: Rob, DesignImp (www.designimp.com), a small web design studio
- Audience: complete beginners (adults), women wanting a fun fitness class (Salsa Fit), and parents of children aged 5+
- Hosting: Vercel (static). Code: GitHub. Pushing to `main` deploys to production.

## Stack

- **Plain static site.** One `index.html` with all CSS and JS inline. No framework, no build step, no package.json.
- Fonts from Google Fonts: Bricolage Grotesque (headings), Plus Jakarta Sans (body), Great Vibes (script accents and logo).
- Images: `justyna.jpg` (her photo, 640×800), `og-image.jpg` (1200×630 social share image).
- `vercel.json`: clean URLs and image cache headers.

Keep it this way unless Rob asks otherwise. Don't introduce React, Tailwind, a bundler or npm dependencies for a one-page site.

## File map

```
index.html     the whole site (HTML + <style> + <script>)
justyna.jpg    hero photo of Justyna
og-image.jpg   Facebook/WhatsApp link preview image (green & gold)
vercel.json    Vercel static config
CLAUDE.md      this file
HANDOVER.md    history, decisions, open items, launch checklist
```

## Page structure (section IDs are used by nav links and JS; don't rename them)

| Order | Section | id / class | Notes |
|---|---|---|---|
| 1 | Sticky header + nav | `header.top`, `#menu` | Links: Classes, Salsa Fit, Kids, Dances, About Justyna, Reviews, Contact, "Book a class" |
| 2 | Hero | `.hero` | Headline "Come and dance with *Justyna*" (script), first-person intro, CTAs (classes, WhatsApp, phone), photo in gold arch, "Next class" chip |
| 3 | Dance-name ribbon | `.ribbon` | Scrolling gold marquee (content duplicated for seamless loop) |
| 4 | Timetable | `#classes`, `.tt`, `.tt-row` | One row per class: day, time, description, price, WhatsApp "Book" button |
| 5 | First class guide | `#first-class` | 4 numbered steps (plain list, no cards) |
| 6 | Salsa Fit spotlight | `#salsa-fit`, `.salsa-spot` | Gold section + dark card with time, price, WhatsApp and call buttons |
| 7 | Parents / kids | `#kids`, `.trust` | DBS, IDTA, first aid, insured |
| 8 | Ten dances | `#dances` | Latin + Ballroom panels, each dance has a 1–5 "energy meter" (`.meter`) |
| 9 | About | `#about` | "My dance *journey*" (script), her story in first person, pull quote, timeline |
| 10 | Reviews | `#reviews` | Two real Google reviews (verbatim), links to Google listing and Facebook |
| 11 | FAQ | `#faq` | `<details>`; first one open on purpose |
| 12 | Contact | `#contact` | Cards: call, email, WhatsApp, Facebook page, Messenger, address + map iframe; enquiry form |
| 13 | Footer | `footer` | Logo, social icons, contact line, DesignImp credit |
| – | Mobile tab bar | `.tabbar` | Shown ≤720px: Classes, WhatsApp, Justyna, Book, Call |
| – | Floating WhatsApp | `.wa-float` | Desktop only |

## JavaScript behaviours (bottom of index.html)

1. **Next class**: reads `.tt-row[data-day][data-start][data-end]` (day 0=Sun…6=Sat), works out the next or ongoing class in **Europe/London** time, adds `.next` to that row (gold edge + "Next up" pill) and fills the hero chip (`#next-label`, `#next-class`). If you add, move or rename a class, update these data attributes.
2. **Form preselect**: elements with `data-pick="…"` set the enquiry form's `<select id="f-class">` to the matching option text.
3. **Copy buttons**: `.copy[data-copy]` copies the phone and email to the clipboard.
4. **Nav highlight**: IntersectionObserver marks the current section's nav link `.on`.
5. **Enquiry form** (`#enquiry`): builds a `mailto:justynawells13@gmail.com` with subject and body pre-filled and opens the visitor's email app. There's no backend. If a form service is added later (e.g. Formspree, Web3Forms, Vercel function + Resend), replace this handler.

## Design system

Colours are CSS custom properties on `:root`. Use the tokens, not new hex values.

| Token | Hex | Use |
|---|---|---|
| `--velvet` | `#0c3b35` | Primary deep emerald (from her velvet dress): header, headings, dark sections |
| `--velvet-2` / `--velvet-3` | `#10493f` / `#16604f` | Emerald variations |
| `--teal` | `#1d8a77` | Secondary accent, small labels |
| `--gold` / `--gold-2` | `#d9a53f` / `#f0cf7c` | Gold accents, buttons, script text |
| `--champ` | `#fbf3df` | Champagne section backgrounds |
| `--paper` | `#f6f8f3` | Main page background |
| `--ink` / `--muted` | `#132420` / `#55665f` | Text |
| `--line` | `#e3e8df` | Borders |
| `--mint` | `#d8efe6` | Soft chips |
| WhatsApp green | `#1fa855` | Only for WhatsApp buttons (`.btn-wa`) |
| Kids accent | `#8a3a70` on `#f8ebf2` | Kids/parents section only |

Buttons: `.btn` + `.btn-gold` (primary), `.btn-velvet` (dark), `.btn-wa` (WhatsApp), `.btn-ghost` (on dark backgrounds).

Breakpoints: `980px` (stack two-column layouts), `720px` (phone: tab bar, single columns).

### Design rules Rob has set (please keep)

- **Script (Great Vibes) accents in two places only**: the hero ("Justyna") and the About heading ("journey"), plus the logo and signature. All other headings stay plain.
- **No small eyebrow labels above most headings.** Only the hero, Salsa Fit ("Every Monday · Ladies only") and parents ("For parents") keep one. No decorative dashes before labels.
- **No decorative feathers, drop caps or badges overlapping her photo.**
- **Avoid the "AI template" look**: don't wrap everything in identical rounded cards; prefer lists, rows and dividers; vary section layouts; no emoji section markers.
- **Font stays "Current"** (Bricolage Grotesque / Plus Jakarta Sans / Great Vibes). Other pairings were tried and rejected.
- **Dances show an energy meter, not music notation** (time signatures and tempo were too technical for beginners).
- **No BBC / Strictly Come Dancing branding**, names, logos or catchphrases.

## Copy and voice

- **British English** (colour, centre, practise as a verb, £).
- Main sections speak **in Justyna's first person** ("I teach…", "Message me…"). Buttons and labels can address the visitor ("Send to Justyna").
- Short, warm, plain sentences. Avoid marketing clichés and em-dash asides.
- Her story in `#about` is **her own words**, lightly edited. Don't rewrite it; only fix typos.
- Reviews are **verbatim real Google reviews**. Never invent, edit or add testimonials.
- Don't add claims (awards, qualifications, prices, times) that aren't in the facts below or confirmed by Rob.

## Source-of-truth business facts

| Item | Value |
|---|---|
| Business | WellSway Dance Studio |
| Teacher | Justyna Wells, IDTA-qualified, DBS checked, first-aid trained, insured |
| Phone / WhatsApp | 07753 612174 (`+447753612174`) |
| Email | justynawells13@gmail.com |
| Venue | 1AE, Community Centre, 10 Fen Rd, Washingborough, Lincoln LN4 1AB |
| Map pin | 53.2243215, -0.4644892 |
| Google listing | "Ballroom and Latin Dance Academy", 5.0 from 3 reviews: https://maps.google.com/?cid=13043871493941128167 |
| Facebook | https://www.facebook.com/profile.php?id=100071256626333 (Messenger: https://m.me/100071256626333) |

**Weekly timetable and prices**

| Day | Time | Class | Price |
|---|---|---|---|
| Monday | 19:15–20:15 | Salsa Fit for Ladies | £10 |
| Tuesday | 19:00–20:00 | Beginners (Ballroom & Latin) | £10 |
| Thursday | 19:00–20:00 | Intermediate / Improvers | £10 |
| Saturday | 9:00am (end time TBC) | Kids Ballroom & Latin, ages 5+ | TBC ("Ask") |

**Dances**: Latin: Cha-cha, Samba, Rumba, Paso Doble, Jive. Ballroom: Waltz, Tango, Viennese Waltz, Foxtrot, Quickstep.

## When you change facts, update every place they appear

The timetable, prices, phone and address are repeated. When one changes, search and update all of them:

- Hero ticks ("£10 per adult class"), hero chip fallback text
- `#classes` rows (text **and** `data-day/start/end/name`)
- `#first-class` step 4 (price), `#salsa-fit` card, `#kids` text
- FAQ answers
- Contact cards, footer
- WhatsApp pre-filled messages (`https://wa.me/447753612174?text=…`, URL-encoded)
- **JSON-LD** in `<head>`: `LocalBusiness` (`openingHoursSpecification`, `hasOfferCatalog` prices, address, geo) and `FAQPage` (must match the visible FAQ text)
- `<meta name="description">`, Open Graph tags, and `og-image.jpg` if the timetable on it changes

## Links and formats

- WhatsApp: `https://wa.me/447753612174?text=<URL-encoded message>`. Each class button has its own pre-filled message naming the class.
- Phone: `tel:+447753612174`. Email: `mailto:justynawells13@gmail.com`.
- External links: `target="_blank" rel="noopener"`.

## Quality bar before committing

- Check at **390px** (phone) and **1280px** (desktop). No horizontal scroll; the mobile tab bar mustn't hide content.
- Keyboard focus visible (`:focus-visible` gold outline). Images need meaningful `alt`.
- Respect `prefers-reduced-motion` (ribbon animation and button transitions already switch off).
- Validate JSON-LD (Google Rich Results Test) after editing structured data.
- Keep the page fast: compress new photos (≤200 KB, ~1600px wide max, WebP or JPG), use `loading="lazy"` below the fold, and set `width`/`height`.

## Deploying

- `main` branch → Vercel production. Other branches get preview URLs.
- No build command; output directory is the repo root.
- Commit messages: short and plain, e.g. `Add class photos to timetable`.
