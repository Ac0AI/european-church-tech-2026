# Backlash response bank

Copy-paste-ready replies for the most likely Reddit / HackerNews / Twitter pile-ons. Each is calibrated to be **one short paragraph, no defensiveness, link to evidence**. Stay polite, never escalate, never delete comments.

**Posting rhythm:** reply within 4-12 hours of a comment landing (long enough not to look like AI, short enough to feel attentive). Don't reply to obvious trolls — they want engagement, withhold it.

---

## "You scraped without consent / this is unethical"

> All data is from publicly accessible URLs the churches themselves publish. We respect robots.txt, no auth bypassed, no rate-limit games. The dataset has zero personal data — only church-level boolean signals and the detected web platform. Any church that wants out can email hello@gospelchannel.com or open an issue here. Removal in under 7 days.

## "What about Catholic / Orthodox / mainline Protestant churches?"

> The dataset is scoped to evangelical and Protestant churches where local congregations typically maintain their own digital presence. Catholic dioceses operate at the diocese level, Orthodox parishes share patriarchate infrastructure — measuring those at the local-parish level would be apples-to-oranges. We say so explicitly in KNOWN_LIMITATIONS.md. Country comparisons here are about evangelical/Protestant adoption, not all-Christian presence.

## "Italy ranks last and that's unfair / Italian-shaming"

> The Italy ranking is a measurement of *individual local-church* digital presence, not a verdict on Italian Christianity. We wrote a dedicated case study explaining the federation model — Italian Pentecostal congregations share assembleedidio.org and the federation's social channels rather than maintaining their own. The data shows the structure, the report explains what the structure means. Linked here: https://gospelchannel.com/european-church-tech-2026

## "This is just GospelChannel marketing dressed as research"

> Two things make that hard to argue: (1) we're publishing the underlying data openly under CC-BY-4.0, no signup wall, so anyone can replicate or critique us. (2) The dataset works completely independent of GospelChannel.com — every signal can be re-verified by going to the church's URL directly. The only marketing touch is a CTA at the bottom of the report. Everything else is open.

## "Your CMS detection is wrong / WordPress detection is broken"

> WordPress detection has a known +3-5pp over-count from theme false-positives — we documented that in KNOWN_LIMITATIONS.md. If you've found a specific bad detection, open an issue with the slug + your finding and we'll fix the row. Headless / Next.js setups are also under-counted; if you're aware of specific churches running modern stacks, we'd love the slugs.

## "How do I know your data is real?"

> Country aggregates were derived by SQL queries against the live catalog at gospelchannel.com — the export script that built this dataset is in the repo, anyone can read what we counted. If a specific country aggregate looks off, open an issue and we'll walk through the underlying query. For per-church verification (which we don't release), email hello@gospelchannel.com — case-by-case access for genuine research uses.

## "Where is the per-church data?"

> Aggregates only. The per-church platform detection is the operational layer our enrichment pipeline builds — releasing it openly would let third parties skip the pipeline entirely (the data is the moat). Aggregates cover what journalists and researchers usually need. For research uses that genuinely need per-church data, email hello@gospelchannel.com.

## "GDPR? You're processing personal data"

> Zero personal data in the dataset. No email addresses, no pastor names, no contact phone numbers. Church-level observable signals only. Churches as legal entities have public-business presences, which sit outside GDPR's natural-person scope. Spot a row that contains personal info? Open an issue and we'll remove it within 24 hours.

## "Why can't I download the raw HTML you scraped?"

> Because that HTML belongs to the churches that published it. We don't redistribute their source content. Our dataset is derived signals — boolean flags and a platform string. If you want the source, re-fetch it yourself from the URLs in churches.csv.

## "You're missing X church / X country / X denomination"

> Catalog inclusion is mostly directory imports + user submissions + admin curation, so coverage isn't exhaustive — KNOWN_LIMITATIONS.md has the per-country notes. If you have a specific church or directory you'd like us to include, open an issue or email hello@gospelchannel.com. We re-release the dataset when material additions land.

## "AI-generated slop / used Claude to write this"

> The methodology is hand-built infrastructure: scraping pipeline, CMS fingerprinting, LLM-assisted extraction for hard-to-find URLs (we do use Claude Haiku for URL extraction, that's documented in the methodology). The data itself is observed, not generated. The report and dataset descriptions were drafted with editing assistance, but every number is derived from the SQL queries you can see in the export script.

## "You're conflating denominations / your taxonomy is wrong"

> The released dataset deliberately doesn't include a denomination breakdown for exactly this reason — denomination labels in our catalog are biased toward the directories we imported (e.g., heavy Pentecostal in Spain because the largest available Spanish directory is Pentecostal). Country aggregates are denomination-agnostic. If you want denomination data we have it but won't release it without flagging the import bias.

## "You should have released the worship-music data / Spotify / sermon analysis"

> Possibly later. This release is the methodology-clean tech-detection layer. Adding worship music data needs a separate cleanup pass on Spotify ID matching and licensing. We'd rather ship a small, defensible dataset now than a sprawling one with murky boundaries.

## "Your composite score is arbitrary"

> Composite is equal-weighted across 5 signals: website, CMS, Facebook, YouTube, livestream. We could weight it differently and Italy / France would shift positions. The raw per-signal numbers in country_aggregates.csv are weighting-free if you'd rather work from those. The rationale for equal weighting: no defensible reason to weight Facebook over YouTube, etc., at the country-comparison level.

---

## When NOT to reply

- **Pure rage / no specific point.** Ignore. Replying validates.
- **Bad-faith framing of the methodology** ("you're trying to make X look bad"). Don't engage with motive-attribution. Either restate the methodology, or don't reply.
- **Theological flame-bait** ("real Christians don't need Facebook"). Out of scope. Skip.
- **Off-topic Reddit drama.** Skip.

## When to escalate (post-update)

If a comment surfaces a real factual error in the data or methodology:
1. Acknowledge the comment within 12 hours: "good catch, looking into this."
2. Verify in the database.
3. If correct, fix the row, cut a new dataset release with a note in the release log.
4. Reply again with: "fixed in v2026-04-29-r2, thanks."

This builds credibility faster than any pre-emptive defense.

## Tone calibration

- Polite, factual, brief. Never sarcastic.
- Always link to evidence (KNOWN_LIMITATIONS.md, FAQ.md, specific URLs) — let the documentation do the work.
- Use "we" not "I" — this is a team-shaped piece of work, not a personality.
- If wrong, say so plainly. "You're right, fixed in r2." That kind of admission earns more credibility than 10 perfect responses.
