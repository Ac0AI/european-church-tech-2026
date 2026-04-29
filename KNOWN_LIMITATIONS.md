# Known Limitations

This document is the long-form answer to "what are you not telling me?" Every observed-data study has limitations; we'd rather list them ourselves than have someone find them later.

## 1. Federation effect

**The issue.** Some denominations organise their digital presence at a national or regional level rather than at the local-church level. Italian Pentecostal congregations affiliated with the Assemblee di Dio (ADI) typically do not maintain their own websites or social channels — they share the federation's `assembleedidio.org`, the federation's Facebook page, and the federation's YouTube channel. In our coverage rates, those local churches will show as "no website / no Facebook / no YouTube," which is technically true but not the full picture.

**Why we kept it as-is.** We chose not to inflate local-church coverage with federation-level credit because the boundary between "local church operates this account" and "national org operates this account" is fuzzy and subjective. Counting the federation's account as belonging to all 900+ local churches would over-credit each by the same factor.

**How we surface it.** The companion report at https://gospelchannel.com/european-church-tech-2026 has a dedicated case study on Italy's federation model. The data does not get rewritten — the interpretation does.

## 2. CMS detection bias (over-counting WordPress)

**The issue.** Our CMS fingerprinter looks for a combination of HTTP headers, JavaScript signatures, and HTML markers. Some non-WordPress themes use WordPress-derived templates (e.g., themes ported from WP to other CMSes), which can trigger a false positive.

**Estimated impact.** WordPress is over-counted by approximately 3-5 percentage points per country. The actual WordPress dominance is real and large, but the precise number is upper-bounded.

**What we'd accept as a correction.** A reproducible test against [Wappalyzer](https://www.wappalyzer.com/) on a random sample of 100 churches per country, showing different distribution. Open an issue with results.

## 3. Headless and modern-framework under-counting

**The issue.** Static-site generators (Next.js with output: export, Nuxt static, Astro, 11ty), headless CMS setups (Contentful, Sanity, etc.), and JAMstack architectures often leave no server-side fingerprint. Many of these are categorised as "Unknown" in our `detected_platform` column.

**Estimated impact.** Likely a few hundred churches across the 12 primary countries. Modern stacks are still rare in this dataset; their under-counting does not change country rankings, only minor absolute counts.

## 4. Catholic and Orthodox under-coverage

**The issue.** This dataset focuses on evangelical and Protestant churches where individual congregations typically maintain their own digital presence. Catholic dioceses operate websites at the diocese level (one per region, not one per parish). Orthodox parishes often share patriarchate-level digital infrastructure. Mainline Protestant state churches (Church of England, Svenska kyrkan, etc.) are partial — diocesan/regional presences are catalogued but most parish-level pages are not in scope.

**Why.** Measuring a Catholic parish's "own Facebook page" against the diocesan Facebook page would be apples-to-oranges. The dataset is internally consistent because all churches in scope are at the same organisational level.

**What it means for your interpretation.** Country comparisons in this dataset are about *evangelical/Protestant church digital adoption*, not about overall Christian digital presence. Italy's "low" rate means Italian *evangelical* churches have low individual digital presence — Italian Catholicism's digital presence is a different, larger story we do not measure.

## 5. Country coverage imbalance

**The issue.** Each country was populated through different combinations of directory imports, user submissions, and admin curation. The catalog is more complete for some countries than others.

**Coverage notes:**
- **Norway** received a large Pinsebevegelsen directory import in late April 2026; per-church enrichment ran shortly before this dataset was generated. Norway's numbers reflect that recent enrichment.
- **Italy** has 1,002 mapped churches but only ~10% have detected own-websites. The remaining ~90% are ADI-affiliated congregations that share the federation's digital presence (see point 1).
- **Spain** is heavily Pentecostal in our catalog because the largest available directory of Spanish evangelical churches (`Pingst-spanska` import) is Pentecostal-affiliated. Coverage of other Spanish denominations is thinner.
- **France** received a large ADD (Assemblées de Dieu) import; non-ADD churches may be under-represented.

## 6. Time of measurement

**The issue.** Detection signals reflect a single observation window. A church's Facebook page may have been deleted between scrape and dataset publication. A new website launched yesterday is not in this dataset.

**Snapshot date.** All detections are between October 2025 and April 2026. Re-detection is recommended for any time-sensitive use of these signals.

## 7. Definition of "approved"

**The issue.** Only churches with `status = 'approved'` are included. The catalog also contains pending and rejected entries. Approval is a manual quality gate at the catalog level, not a theological or qualitative judgment.

**Implication.** A small bias toward churches that have been verified at least once. Newer additions awaiting approval are not in this dataset.

## 8. We don't measure quality, only presence

A church can have a polished, daily-updated Facebook page, or a Facebook page that hasn't posted since 2019. This dataset reports "has Facebook = true" for both. The same is true for websites, YouTube channels, and livestream URLs.

If you want freshness or activity signals, that's a separate analysis we don't publish in this release.
