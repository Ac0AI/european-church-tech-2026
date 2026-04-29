# European Church Tech 2026 — Open Dataset

Country-level and platform-by-country measurements of digital adoption across **12,624 evangelical and Protestant churches** in 19 European countries. Observed-data methodology — every coverage rate is derived from publicly observable signals about each church's web presence. We did not survey.

**Companion report:** https://gospelchannel.com/european-church-tech-2026

## What's in here

```
data/
├── country_aggregates.csv  # Per-country totals & coverage rates (19 rows)
├── platforms.csv           # CMS / web platform breakdown by country (138 rows)
└── snapshot.json           # Machine-readable metadata + countries + platforms

notebooks/
└── exploratory_analysis.ipynb  # Python load + first analysis (5 minutes)
```

**What is NOT in this release:** per-church rows. Detection at the church level (which church runs WordPress, which one is on Wix, etc.) is the operational asset built by the enrichment pipeline and we keep that internal. Aggregates are released openly; the per-church layer is not. See *Why aggregates only* below.

## What we measured

For each approved church in the catalog, we record whether the following signals are present:

- **Website** — any detected URL (from catalog or Google Places enrichment)
- **CMS / detected platform** — the primary web platform (WordPress, Squarespace, Wix, Webflow, Subsplash, etc.) detected by HTTP fingerprinting
- **Facebook presence** — a Facebook page URL was found via either catalog data or LLM extraction from the church's website
- **YouTube channel** — same, for YouTube channel URL or YouTube channel ID
- **Livestream** — a confirmed livestream URL on the church's profile

We do **not** measure: theological content, denomination quality, congregant experience, sermon style, or anything qualitative. The signals are infrastructure-level only.

## Methodology

Coverage rate per signal = `(number of churches with detected signal) / (total approved churches in country)`. The denominator is consistent across signals — coverage rates are comparable within a country.

Data acquisition pipeline:
1. **Directory imports.** Public church directories (denomination websites, regional listings) ingested for catalog completeness.
2. **Website detection.** Each church's URL is fetched (respecting `robots.txt`) and run through a CMS-fingerprint detector.
3. **Google Places enrichment.** Apify Google Places lookup by church name + city to find missing URLs and verify location.
4. **LLM extraction.** Claude Haiku reads the church's homepage HTML to extract Facebook URL, YouTube URL, and livestream URL when present.

The full report at https://gospelchannel.com/european-church-tech-2026 explains the survey-vs-observed distinction in detail.

## License

- **Data** (`*.csv`, `*.json` under `data/`): [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) — free to use, share, and remix with attribution to *GospelChannel — European Church Tech 2026*.
- **Code & notebooks** (`*.mjs`, `*.py`, `*.ipynb`): [MIT License](LICENSE).

## How to cite

Plain text:
> *European Church Tech 2026: an observed-data dataset on digital adoption across 12,624 European churches.* GospelChannel, 2026. https://gospelchannel.com/european-church-tech-2026

BibTeX:
```bibtex
@dataset{gospelchannel_ect2026,
  title  = {European Church Tech 2026: an observed-data dataset on digital adoption across 12,624 European churches},
  author = {GospelChannel},
  year   = {2026},
  url    = {https://gospelchannel.com/european-church-tech-2026},
  note   = {CC-BY-4.0}
}
```

## Ethics & privacy

- **No personal data.** This dataset contains zero personal identifiers. No email addresses, pastor names, congregant lists, contact phone numbers, or claim tokens. Only church-level observable signals.
- **Public-source only.** All data is derived from publicly accessible URLs that the churches themselves publish. We respect `robots.txt`. We do not bypass authentication.
- **No identifiable churches in this dataset.** Aggregates count churches per country and per platform — no individual church can be identified from the released files. Country totals are coarse enough that no church is uniquely tagged.
- **GDPR.** We are processing public-business contact information at the organisation level only. No natural-person data is included in the dataset.

### Live catalog removal

If you'd like a church removed from the live catalog at gospelchannel.com (which is separate from this dataset), email **hello@gospelchannel.com** with the church name. We process catalog removals within 7 days. After a removal, future versions of this dataset will reflect the lower country count.

## Why aggregates only

We release country and platform-by-country aggregates. We do not release per-church platform detections. Two reasons:

1. **The per-church layer is operational infrastructure.** Detecting a CMS, finding a Facebook URL, and confirming a livestream takes a non-trivial pipeline (catalog ingestion, Apify Google Places lookup, LLM extraction, fingerprint detection). Releasing the per-church output would let third parties skip the pipeline entirely. We're happy to release the *findings*; the *raw enrichment* is the work product that funds the work.
2. **Aggregates are what most uses need.** Journalist citations, academic papers, and benchmark comparisons work fine on country-level numbers. The per-church layer matters for sales targeting and competitive analysis — uses we do not subsidise for free.

If you have a research use that genuinely requires per-church data (e.g., academic study with a clear publication path), email **hello@gospelchannel.com** and we'll discuss data access on a case-by-case basis.

## Verification

Every per-country aggregate is derived by SQL query against the live catalog at gospelchannel.com. The export script that generated this dataset is published in the companion repo — read it to see exactly what we counted. If you doubt a specific aggregate, open an issue with the country and your reasoning.

## Known limitations

A short list — full discussion in [`KNOWN_LIMITATIONS.md`](KNOWN_LIMITATIONS.md):

- **Federation effect.** Where a denomination shares a single national web/social presence (e.g., Italian Assemblee di Dio), local churches will show as "no individual presence" even though they are part of an active digital community.
- **CMS over-counting.** WordPress detection is biased upwards because some non-WP themes leave WP-style markers. Estimated +5pp over-count.
- **Headless under-counting.** Modern Next.js / Nuxt / static-site setups can be hard to fingerprint; some are categorised as "Unknown."
- **Catholic / Orthodox under-coverage.** This dataset focuses on evangelical and Protestant churches where local congregations typically maintain their own digital presence. Catholic dioceses, Orthodox parishes, and large state churches are largely outside the scope by design.
- **Coverage varies by country.** Italy and Spain have lower per-church website detection because directory imports for those countries pulled fewer URLs at source.

## FAQ

See [`FAQ.md`](FAQ.md) for answers to:

- *Did you scrape without consent?*
- *What about Catholic or Orthodox churches?*
- *Italy looks last — is that fair?*
- *Is this a GospelChannel marketing exercise?*
- *How accurate is your CMS detection?*
- *GDPR / privacy?*
- *Can I get the raw HTML you scraped?*

## Mirrors

This dataset is also published on:

- **Kaggle:** https://www.kaggle.com/datasets/gospelchannel/european-church-tech-2026-observed-data

(Zenodo with DOI + Hugging Face mirrors coming.)

## Acknowledgements

Built on data collected at GospelChannel.com — a public catalog of churches where pastors can claim and improve their listing. Released openly so others can replicate, critique, or build on the work.

## Contact

- Issues / corrections / suggestions: GitHub Issues on this repo.
- General: hello@gospelchannel.com
