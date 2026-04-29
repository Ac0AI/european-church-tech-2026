# FAQ

## Did you scrape without consent?

All data is from publicly accessible URLs that the churches themselves publish on the open web. We respect `robots.txt`. We do not bypass authentication, paywalls, or rate limits. We do not scrape personal accounts, member directories, or anything behind a login.

The dataset itself contains no personal information — only church-level observable signals (URL, social presence, platform). There is no scraped HTML, no member data, no email addresses.

If a church wants to be removed from the catalog or the dataset, see the removal process in the README — typical turnaround is under 7 days.

## What about Catholic or Orthodox churches?

This dataset focuses on **evangelical and Protestant churches** where individual congregations typically maintain their own websites and social channels. Catholic dioceses and Orthodox parishes generally share regional or patriarchate-level digital infrastructure, which would not be comparable at the same level.

Country comparisons are therefore about *evangelical/Protestant* digital adoption, not about all Christian presence in a country. We're explicit about this in the report and in `KNOWN_LIMITATIONS.md`.

## Italy ranks last on individual website rate. Is that fair?

Italian Pentecostalism is structured federally. Most local Assemblee di Dio congregations share the national federation's website, Facebook page, and YouTube channel. The numbers in this dataset are accurate as a measurement of *individual* church-level digital presence — they would be misleading if read as "Italian Pentecostalism is digitally absent."

We explicitly wrote a case study on this, run as Section 4 of the report at https://gospelchannel.com/european-church-tech-2026. The federation finding is itself the interesting result — not a bug in the data.

## How is this not a GospelChannel marketing exercise?

GospelChannel is the catalog the data was scraped from — that's true and we say so up front. The reasons we're publishing the dataset openly:

1. Anyone can replicate or critique the findings against the raw data.
2. Researchers and journalists can build their own analyses without going through us.
3. Future church-tech reports become easier to write because the underlying observational data exists.

If we wanted to gate the data behind GospelChannel branding, we wouldn't be releasing it under CC-BY-4.0 with no signup wall.

The companion report does link back to the live catalog at the end (the "Find your church" CTA) — that is the only marketing touchpoint, and it's not in the dataset itself.

## How accurate is your CMS detection?

Detection uses HTTP-header, JS-signature, and HTML-marker fingerprinting against a library of known platforms. Estimated accuracy:

- **WordPress:** over-counted by 3-5pp due to false positives from WP-derived themes on other CMSes.
- **Squarespace, Wix, Webflow:** high accuracy (these platforms leave clear signatures).
- **Subsplash, Faithlife, Tithe.ly:** high accuracy where present.
- **Modern frameworks (Next.js, Nuxt, Gatsby, Framer):** detected when client-side hydration markers are present; pure static exports may be missed.
- **Headless CMSes (Contentful, Sanity, etc.):** under-detected; many show as "Unknown."

Reproducibility: every row has a `slug` you can use to look up the live profile and re-detect with [Wappalyzer](https://www.wappalyzer.com/) or any equivalent tool. Disagreements welcome — open a GitHub issue.

## GDPR / privacy?

The dataset contains zero personal data. No email addresses, pastor names, member lists, donation records, prayer requests, or contact phone numbers. The data is at the church (organisation) level only — public business contact information.

GDPR applies to natural persons. Church organisations as legal entities have public-business presences, which are not GDPR-restricted at the organisation level. We process no personal data in this dataset.

If you spot any row that you believe contains personal information, open an issue and we'll remove it within 24 hours.

## Can I get the per-church data — which specific churches run what?

No. The per-church platform detection is the operational asset built by our enrichment pipeline. We release aggregates openly because they're what journalists and researchers need; we do not release the per-church layer because it is the work product that justifies the pipeline investment.

If you have a research use that genuinely requires per-church data (e.g., a study with a clear publication path), email **hello@gospelchannel.com** and we'll discuss case-by-case access.

## Can I get the raw HTML you scraped?

No. The raw HTML belongs to the churches that published it — we do not re-distribute it. If you want to do your own analysis on church website HTML, re-fetch it yourself from the public URLs.

## Why are some countries missing or under-represented?

Catalog inclusion comes from a mix of directory imports, user-submitted listings, and admin curation. Some countries have stronger directory infrastructure than others. Country coverage is not exhaustive — for example, France's catalog is heavily ADD-affiliated because that's the largest available French directory; non-ADD French evangelical churches may be under-represented.

`KNOWN_LIMITATIONS.md` has the per-country notes.

## How can I cite this?

```
European Church Tech 2026: an observed-data dataset on digital adoption
across 12,624 European churches. GospelChannel, 2026.
https://gospelchannel.com/european-church-tech-2026
```

BibTeX is in the README.

## Found something wrong?

Open a GitHub issue with:
- The slug of the church (or the country aggregate)
- What you think the correct value is
- Any source (URL, screenshot) that supports your finding

We process issues weekly and re-release the dataset when there are material corrections.

## Found a bug in the methodology?

Same channel — open an issue with a reproducible counter-example. If your point holds, we'll update `KNOWN_LIMITATIONS.md` and credit you in the next release.

## Why CC-BY-4.0 specifically?

CC-BY-4.0 lets anyone use the data for any purpose (including commercial) as long as they credit *European Church Tech 2026 (GospelChannel, 2026)*. It's the standard open-data licence used by Wikidata, Our World in Data, and most government open-data portals. We chose it because it removes friction for researchers and journalists while keeping a clear paper trail back to the source.
