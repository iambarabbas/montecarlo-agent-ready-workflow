# MEMORY.md

## True Legacy Homes - Current State (Feb 2026)

### SEO Score: 6.5/10
- **San Diego:** Strong (#1 local, 329 reviews)
- **Orange County:** Moderate (110 reviews, not ranking organically)
- **Los Angeles:** Critical (1 review, invisible in search)

### Key SEO Priority
LA reviews are the #1 unlock. Target 30+ reviews in 4 weeks.

### Content Gap
OC location page has 2x the content of SD/LA. Those pages need expansion.

### Active Cron Jobs
- Estate Sales: Fri 9:30am PT (job: `6bd7abf4-b77d-4b65-a9d2-e9ff9a2261ef`)
- SD Blog: Mon 8am PT
- OC Blog: Wed 8am PT  
- LA Blog: Fri 8am PT

### WordPress Critical
- Sales posts use `/wp-json/wp/v2/sales` (NOT `/posts`)
- Avia Builder requires full template structure
- All images must be uploaded (100-400 per sale)
- Working template saved: `/memory/estate-sale-avia-template.txt`

### Image Extraction Critical
- **NEVER** use static HTML/curl to get images (only gets ~16)
- **ALWAYS** use Playwright script: `node scripts/extract-estatesales-images.js <saleId>`
- This scrolls the page to load ALL images (typically 100-300 per sale)
- CDN format: `https://picturescdn.estatesales.net/{saleId}/1-2/{guid}.jpg` (thumbnails)
- ⚠️ **MUST use `/1-2/` NOT `/1-1/`** — `/1-1/` returns 403 Forbidden, `/1-2/` is public

### Static Site Sale Pages (TLH GitHub Pages)
- **Location:** `/upcoming-sales/` directory
- **Main listing:** `/upcoming-sales/index.html`
- **Individual sales:** `/upcoming-sales/{city}-{street}/index.html`
- **Template:** `/scripts/generate-sale-page.py` (includes social links in sidebar)

**Weekly Update Process:**
1. Extract images via Playwright script (get sale IDs from estatesales.net)
2. Create new sale page directories with index.html (generated from template)
3. Update `/upcoming-sales/index.html`:
   - **This Weekend section:** Add new sales at top with "2-Day Sale" badge
   - **Past Sales section:** Move previous week's sales here with "Ended" badge + grayscale styling
4. Commit and push to TrueLegacyHomes/website

**Social Media Links (Mar 2026):**
- Main `/upcoming-sales/` page: Facebook & Instagram in footer
- Individual sale pages: "Follow Our Sales" section in sidebar (after Get Directions button)
- Template updated: `scripts/generate-sale-page.py` includes social links automatically

**Image URL Fix:** Always replace `/1-1/` with `/1-2/` in extracted image URLs before using

### Key Files
- `tlh-seo-audit-2026-02-14.md` — Full SEO audit
- `tlh-seo-4-week-roadmap.md` — 4-week action plan
- `memory/estate-sales-workflow.md` — Weekly workflow docs
- `memory/estate-sales-image-extraction.md` — **Playwright image extraction** (ALWAYS use this)
- `memory/tlh-site-go-live.md` — **Site go-live plan** (Cloudflare Pages, redirects, DNS)
- `scripts/extract-estatesales-images.js` — Extracts ALL images via headless browser
- `scripts/generate-sale-page.py` — Generates sale HTML from template + images
- `tlh-rebuild/` — Markdown + Tailwind site rebuild (COMPLETE - 25+ pages, 155 blog posts)
- `tlh-rebuild/_redirects` — 324 redirect rules for go-live (WP URLs → new URLs)

### TLH GitHub (Feb 2026)
- **Organization:** https://github.com/TrueLegacyHomes
- **Website repo:** https://github.com/TrueLegacyHomes/website
- **Platform Suite repo:** https://github.com/TrueLegacyHomes/platform-suite
- **Staging URL:** https://staging.website-252.pages.dev/
- **Production URL:** https://website-252.pages.dev/
- **OLD repo (DO NOT USE):** iambarabbas/tlh-markdown-demo
- **Local folder:** `/Users/admin/.openclaw/workspace/tlh-rebuild/`
- **Git remote:** `origin` (TrueLegacyHomes/website)
- **Pages:** 25+ service/location pages + 155 blog posts

⚠️ **CRITICAL WORKFLOW (Mar 2026):**
1. **ALL work happens on `staging` branch** - NEVER push directly to main
2. Only merge to main when Brett says **"Push to production"**
3. After any HTML class changes, ALWAYS rebuild Tailwind: `~/tailwindcss3 -i ./src/input.css -o ./css/tailwind.min.css --minify`
4. All TLH website work MUST push to TrueLegacyHomes org, NOT iambarabbas!

### TLH AI Infrastructure (Feb 2026)
- **Cowork Plugins:** https://github.com/TrueLegacyHomes/tlh-cowork-plugins (14 skills, private)
- **Starter Template:** https://github.com/TrueLegacyHomes/tlh-starter-template (Next.js scaffold)
- **Docs Site:** https://truelegacyhomes.github.io/tlh-docs/ (25 pages, VitePress)
- **Install skills:** `/plugin marketplace add TrueLegacyHomes/tlh-cowork-plugins`
- **Tech Stack:** Next.js + Supabase + Vercel + Tailwind + shadcn/ui
- **Brand Colors:** Teal #38b5ad, Dark #1e293b, Warm #fef3e2
- **Source doc:** "IT Person Onboarding Guide" (9 phases)
- **Status:** Phases 1-2, 4A, 4B complete. Phase 3 blocked (needs API creds from Paul)

### Enterprise MCP Server (Mar 2026)
- **Live URL:** https://enterprise-mcp.brett-35e.workers.dev
- **GitHub:** https://github.com/TrueLegacyHomes/enterprise-mcp (private)
- **Local:** ~/Desktop/enterprise-mcp/
- **Stack:** Cloudflare Workers + Durable Objects + D1 SQLite
- **Auth:** Microsoft 365 SSO via Cloudflare Zero Trust
- **Note:** Use `new_sqlite_classes` migration (required for free plan)

### Target Audience (ALL PAGES)
**55+ women** navigating life transitions (downsizing, parent's estate, relocating). 
- Lead with empathy before logistics
- Human faces > product shots
- Phone calls preferred over forms
- Reduce information overload
- Acknowledge the emotional weight

### Static Site Cron Job (TODO)
Automate weekly estate sale page updates:
- Extract images from new sales
- Create sale detail pages
- Update main /upcoming-sales/ listing (new → This Weekend, old → Past Sales)
- Push to GitHub
- Coordinate with WordPress + Mailchimp workflow (Fri 9:30am)

### TLH Sub-Agent (TODO)
Brett wants dedicated TLH agent for website/SEO/design work:
- Auto-route TLH messages from Clark → TLH agent
- Invisible to user (just message Clark, TLH agent handles)
- Needs: brand context, SEO roadmap, 55+ women audience profile, WP credentials

### SITE TRANSFER - Ready to Resume
**Trigger phrase:** "site transfer"

**Current state (Feb 26):**
- Site cleaned: 474MB → ~40MB deployable
- 98 article posts kept, 62 sales posts removed
- 87 blog images compressed (30MB) - need to go on R2
- HTML/CSS/root images (~10MB) - goes on Cloudflare Pages

**Next steps when triggered:**
1. Brett creates R2 bucket: `tlh-blog-images`
2. Get R2 public URL (custom domain or R2.dev)
3. Update blog HTML paths to R2 URLs
4. Upload 87 images to R2 via wrangler
5. Deploy Pages (~10MB)

**Key files:**
- `scripts/upload-blog-image.sh` - Future image uploads
- `docs/R2-SETUP.md` - Full R2 instructions
- `memory/2026-02-26.md` - Detailed session notes

---

## Clear Sky Speech Therapy (Feb 2026)

### Overview
- **Owner:** Megan Williamson, MA, CCC-SLP
- **Location:** Kamas, Utah (Summit County)
- **Phone:** 435-248-2135
- **Service Area:** Park City, Heber City, Midway, Summit County, Wasatch County (Utah only)

### Website
- **Custom Domain:** https://clearskyspeechutah.com (HTTPS pending provisioning)
- **GitHub Pages:** https://iambarabbas.github.io/clear-sky-speech/
- **GitHub:** https://github.com/iambarabbas/clear-sky-speech
- **Stack:** HTML + Tailwind CSS, GitHub Pages
- **DNS:** GoDaddy (A records → GitHub IPs, CNAME www → iambarabbas.github.io)

### Brand Colors
- Dark teal: #2D4A5E
- Coral accent: #E8A68C

### Key Features
- Click-to-call (no contact forms)
- Private pay only
- Reading therapy service page (big SEO opportunity)
- 5 Utah location pages for local SEO
- AI-generated images via DALL-E + Brett's hero/logo

### Source Files
- ~/Desktop/speech/ (logo, icon, hero, resume)

---

## Wheeless Fitness (Mar 2026)

### Overview
- Personal training / fitness coaching website
- **Live:** https://iambarabbas.github.io/wheeless-fitness-rebuild/
- **GitHub:** https://github.com/iambarabbas/wheeless-fitness-rebuild

### Brand Colors
- Primary blue: #4A7C8C
- Dark: #1e293b

---

## Barabbas Road Church (Feb 2026)

### Overview
- Reformed, gospel-centered church in San Diego
- Tagline: "Hear the Truth. Live the Truth. Defend the Truth."
- Address: 7340 Miramar Rd, San Diego, CA 92126
- Service: Sundays @ 10am

### Brand Colors
- Dark charcoal: #272727
- Gold accent: #C0A365
- Teal accent: #279AB3

### Audit (Completed)
- **Live:** https://iambarabbas.github.io/barabbas-audit/
- **Local:** /barabbas-audit/index.html
- WordPress 4.3 (2015!) - major security risk
- Missing schema markup, no H1 on homepage
- Score: Technical 45/100, SEO 62/100

### Redesign (In Progress)
- **Live:** https://iambarabbas.github.io/barabbas-rebuild/
- **Local:** /barabbas-rebuild/index.html
- Modern responsive design with actual brand colors
- Photos from current site: logo, hero, baptism, pastor, missions
- Full schema markup for local SEO
- Status: Draft ready, Brett will come back to it

---

## Brett (USER.md)
- Works in marketing
- Timezone: PST
- Current focus: TLH content marketing automation + SEO

## GitHub Routing ⚠️ IMPORTANT
- **TrueLegacyHomes** org → ALL TLH projects (website, platform-suite, future TLH repos)
  - Push command: `git push tlh main`
  - Staging: https://truelegacyhomes.github.io/website/
  - NEVER push TLH stuff to iambarabbas!
- **iambarabbas** → everything else (Clear Sky, Barabbas Church, personal projects)

---

## Clark (Me)
- 🐘 Elephants never forget
- Help Brett with TLH marketing automation
- Run estate sales workflow every Friday 9:30am
