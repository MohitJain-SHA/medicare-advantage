# Senior Healthcare Advisors — Medicare Advantage Funnel

Eligibility-style quiz (3 questions), then a result screen with a "Tap to Call" CTA and a "not ready to call right now" callback form. Self-contained static site — no build step, `index.html` deploys as-is. Same structure, styling, tracking, and LeadConduit posting pattern as the [home healthcare funnel](https://github.com/MohitJain-SHA/senior-healthcare-advisors-home-healthcare).

## Before launch — fill these in

Everything below is a marked placeholder in `index.html`. Nothing on the page pretends to work until these are set.

| What | Where | Behavior until set |
| --- | --- | --- |
| CallGrid tracking number | `CALLGRID_CAMPAIGN_SOURCE_ID` in the script | Visitors see the static number `(954) 697-9692` (`CALLGRID_FALLBACK`) instead of a per-visitor tracking number, so calls aren't attributed by CallGrid |
| LeadConduit flow | `LEADCONDUIT_URL` in the script (`…/flows/<id>/sources/<id>/submit`) | Submitting the callback form shows an error instead of a success message |
| TPMO disclaimer counts | `[NUMBER OF ORGANIZATIONS]` / `[NUMBER OF PRODUCTS]` (three places: article callout, result screen, footer) | Placeholder text is visible on the page |
| License numbers / NPN | `[STATE LICENSE NUMBERS / NPN AS REQUIRED]` in the footer | Placeholder text is visible on the page |
| Footer links | Privacy, Terms, Do Not Sell, Contact (`href="#"`) | Links go nowhere |
| Preview image | `og:image` / `og:url` in `<head>` | No link-preview image |

Also confirm with LeadConduit: `source_sha` is still `senior_healthcare_advisors_web` (copied from the home healthcare funnel) — change it if this flow routes on a different value.

## Compliance notes

Medicare marketing is regulated by CMS. Have compliance review the copy, the consent language, and the disclaimer before running traffic. This page intentionally leaves out the home healthcare funnel's simulated visitor counter, rotating "recent activity" popups, and countdown timer.

## Attribution

Every URL parameter on the landing URL is kept in `sessionStorage` for the visit and mapped into LeadConduit's hidden fields on the callback form:

| URL parameter | LeadConduit field(s) |
| --- | --- |
| `campaign_id` | `campaign_id_ghl_sha` |
| `adgroup_id` or `adset_id` | `ad_group_id_ghl_sha` |
| `ad_id` | `ad_id_ghl_sha`, `sub_id_sha` |
| `medium` or `utm_medium` | `medium_ghl_sha` |
| `term` or `utm_term` | `term_ghl_sha` |
| `gclid` | `gclid_sha`, `google_click_id_ghl_sha`, `google.clid` |
| `msclkid` | `microsoft_click_id_ghl_sha` |
| `fbclid` | `meta_click_id_ghl_sha` |
| `source` / `utm_source` | detected platform → `platform_ghl_sha` (`google`, `bing`, or `facebook` for Meta) |

The `facebook.*` fields are only filled for Meta traffic, so Google and Bing clicks are never labelled as Facebook data. The `device` and `platform` URL parameters from the ad-network templates are not mapped to LeadConduit fields.

## Editing the hero image

Replace the file named `hero-photo.jpg` with a new image of the same name — no code changes needed. (The current image is AI-generated.)
