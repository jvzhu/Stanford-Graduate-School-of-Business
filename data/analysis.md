# Data Analysis & Categorization

This document analyzes the datasets and sources collected in [`sources.md`](sources.md) and provides a categorized summary of data coverage, quality, and notable gaps.

Related issue: [Analyze and categorize collected data (#2)](https://github.com/jvzhu/Stanford-Graduate-School-of-Business/issues/2)

## Scope & Method

- **Input:** the 17 candidate sources catalogued in [`sources.md`](sources.md) under issue [#1](https://github.com/jvzhu/Stanford-Graduate-School-of-Business/issues/1).
- **Method:** desk review of each source's access model, license terms, subject coverage, and documentation; no new raw data was collected.
- **Output:** category-level summaries below, plus a consolidated gap list and recommendations.

## Category Summary

| Category | Sources | Access Profile | Redistributable | Overall Quality |
| --- | --- | --- | --- | --- |
| Institutional repositories & library catalogs | 4 (SDR, GSB Working Papers, SearchWorks, HathiTrust) | Mostly open; some items restricted | Varies per item | Medium–High |
| Academic databases & scholarly search | 5 (Google Scholar, SSRN, JSTOR, NBER, RePEc/IDEAS) | Mixed (open, registration, subscription) | Generally no | Medium |
| Financial & business datasets | 8 (WRDS, CRSP, Compustat, SEC EDGAR, FRED, World Bank, Census, BLS) | 5 open, 3 restricted | Open subset yes; subscription subset no | High |

## Detailed Analysis by Category

### 1. Institutional Repositories & Library Catalogs

**Coverage:** Broad archival and bibliographic coverage of Stanford-affiliated research and historical material. GSB Working Papers provides the most directly relevant subject coverage for business research; SDR and SearchWorks add depth for Stanford-specific holdings; HathiTrust extends coverage to public-domain historical texts.

**Quality:** Metadata quality is high (professionally curated by libraries). Content quality varies: working papers are not peer-reviewed, and archival items may have incomplete or inconsistent metadata.

**Gaps:**

- No structured, machine-readable datasets — these are primarily document/bibliographic sources.
- Per-item license checks are required before any reuse, which limits bulk collection.
- Some SDR items are access-restricted and cannot be mirrored in this repository.

### 2. Academic Databases & Scholarly Search

**Coverage:** Excellent breadth for literature discovery across economics, finance, and management. SSRN and NBER give early access to preprints; RePEc/IDEAS provides open bibliographic metadata; JSTOR covers the peer-reviewed archive.

**Quality:** Bibliographic metadata is generally reliable. Content quality is mixed: SSRN and NBER host non-peer-reviewed working papers, and Google Scholar indexing can include duplicates and low-quality venues.

**Gaps:**

- Full-text access to JSTOR and many publisher-hosted articles requires institutional subscription (follow-up pending in `sources.md`).
- These sources point to replication data rather than hosting it; obtaining the underlying datasets requires per-paper follow-up.
- No bulk-download or API access for most of these services within permitted terms.

### 3. Financial & Business Datasets

**Coverage:** The strongest category for quantitative research.

- *Open subset* (SEC EDGAR, FRED, World Bank, Census, BLS): comprehensive coverage of U.S. securities filings, macroeconomic time series, global development indicators, demographics, and labor statistics. All offer programmatic access (APIs or bulk download).
- *Restricted subset* (WRDS, CRSP, Compustat): gold-standard security prices and firm fundamentals, but access is subscription-gated.

**Quality:** High across the board. Government sources are authoritative, well-documented, and versioned. WRDS/CRSP/Compustat are the academic-finance reference standard.

**Gaps:**

- Institutional access to WRDS/CRSP/Compustat is unconfirmed (open follow-up in `sources.md`); until confirmed, firm-level security prices and fundamentals are a coverage hole.
- Restricted data cannot be redistributed here — only derived aggregates or access instructions can be stored.
- No international firm-level equivalent identified for the open subset (open sources skew U.S.-centric, except World Bank).

## Consolidated Gap List

1. **No primary datasets downloaded yet** — the Primary Datasets table in `sources.md` currently contains only the `_None yet_` placeholder row; the open government sources (SEC EDGAR, FRED, Census, BLS, World Bank) are the recommended starting point since they are freely redistributable.
2. **Subscription access unconfirmed** — WRDS/CRSP/Compustat, JSTOR, and NBER follow-ups remain open, blocking firm-level financial data and full-text article retrieval.
3. **U.S.-centric skew** — apart from World Bank Open Data, open sources cover primarily U.S. data; international firm and market coverage depends on the restricted subset.
4. **No structured research datasets from the bibliographic categories** — repositories and scholarly databases yield documents and citations, not analysis-ready data; replication datasets must be tracked down paper by paper.
5. **License heterogeneity** — several sources ("varies by item/publisher") need per-item verification before any data can be stored under `data/raw/`.

## Recommendations

1. Prioritize downloading baseline datasets from the open, redistributable sources (FRED macro series, SEC EDGAR filings indexes, Census/BLS tables, World Bank indicators) and record them in the Primary Datasets table of `sources.md`.
2. Resolve the restricted-access follow-ups (WRDS/CRSP/Compustat, JSTOR, NBER) to close the firm-level data gap.
3. Add at least one international/non-U.S. open source (e.g., OECD or IMF data) to reduce geographic skew.
4. When using repository or scholarly sources, record per-item license status in `sources.md` before storing any content in `data/raw/`.

## Status

- [x] Review all catalogued sources in `sources.md`
- [x] Categorize sources and summarize coverage per category
- [x] Assess data quality per category
- [x] Document notable gaps and follow-up recommendations
