# Senior Healthcare Advisors — Medicare Advantage Funnel

Eligibility-style quiz (3 questions), then a result screen with a "Tap to Call" CTA and a "not ready to call right now" callback form. Self-contained static site — no build step, `index.html` deploys as-is. Same structure, styling, tracking, and LeadConduit posting pattern as the [home healthcare funnel](https://github.com/MohitJain-SHA/senior-healthcare-advisors-home-healthcare).

## Before launch — fill these in

Marked placeholders in `index.html`. Nothing on the page pretends to work until these are set.

| What | Where | Behavior until set |
| --- | --- | --- |
| CallGrid tracking number | `CALLGRID_CAMPAIGN_SOURCE_ID` in the script | Visitors see the static number `(954) 697-9692` (`CALLGRID_FALLBACK`) instead of a per-visitor tracking number, so calls aren't attributed by CallGrid |
| LeadConduit flow | `LEADCONDUIT_URL` in the script (`…/flows/<id>/sources/<id>/submit`) | Submitting the callback form shows an error instead of a success message |
| Preview image | `og:image` / `og:url` in `<head>` | No link-preview image |

Also confirm with LeadConduit: `source_sha` is still `senior_healthcare_advisors_web` (copied from the home healthcare funnel) — change it if this flow routes on a different value.

## Compliance notes

This is a good-faith review, not legal advice or a compliance sign-off. Medicare marketing is regulated by CMS (and consent by the TCPA), so have your compliance team or carrier marketing departments review the page before running traffic.

What the page does:

- Labels the page **Advertisement** at the top, since the article format could read as editorial.
- Uses the disclaimer and consent wording from the previous seniorhealthcareadv.com site, with the button name changed to "Get My Free Callback" and a required checkbox added. The TPMO sentence appears in the article, on the result screen, and in the footer, with the counts from that site (5 organizations, 81,602 products). **Update the counts whenever they change.**
- The consent checkbox is unchecked by default. Answering the quiz is explicitly *not* treated as consent.
- Links the Terms of Use, Privacy Policy, and Contact pages on seniorhealthcareadv.com in the footer, and the Privacy Policy next to the form.
- Leaves out the home healthcare funnel's simulated visitor counter, rotating fake "approved" popups, countdown timer, and "never sold" claim.
- Enrollment dates (Oct 15 – Dec 7, Jan 1 – Mar 31, initial enrollment window) are stated factually.

The footer intentionally omits the carrier material ID (`MULTIPLAN_…`) from the previous site: that ID belongs to a specific approved piece of material, so this page needs its own approval and ID before it is used.

Not handled by this page: the CMS call requirements (recording, the verbal TPMO disclaimer at the start of a call, and a documented Scope of Appointment 48 hours before a personal marketing appointment) belong in the call scripts.

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
