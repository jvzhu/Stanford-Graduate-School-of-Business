# Data Sources

This document tracks candidate and confirmed data sources for the project, including bibliographic metadata, access and license terms, links to raw data, and notes on data quality and coverage.

Related issue: [Collect data from sources (#1)](https://github.com/jvzhu/Stanford-Graduate-School-of-Business/issues/1)

## How to Add a Source

For each source, record the following fields:

- **Title** — name of the dataset, archive, or publication
- **Author/Publisher** — creator or maintaining institution
- **Year** — publication or last-updated year
- **URL/DOI** — persistent link or digital object identifier
- **Access** — open, registration required, subscription, or restricted
- **License/Usage Terms** — license name or summary of usage restrictions
- **Data link** — direct link to raw data, if available
- **Quality/Coverage notes** — initial assessment of data quality and coverage

## Candidate Sources

### Institutional Repositories & Library Catalogs

| Title | Author/Publisher | Year | URL/DOI | Access | License/Usage Terms |
| --- | --- | --- | --- | --- | --- |
| Stanford Digital Repository (SDR) | Stanford University Libraries | Ongoing | <https://sdr.stanford.edu/> | Open (some items restricted) | Varies by item; check each record |
| Stanford GSB Working Papers | Stanford Graduate School of Business | Ongoing | <https://www.gsb.stanford.edu/faculty-research/working-papers> | Open | Author-retained copyright; cite as working paper |
| SearchWorks (Stanford Library Catalog) | Stanford University Libraries | Ongoing | <https://searchworks.stanford.edu/> | Open catalog; items may require affiliation | Varies by item |
| HathiTrust Digital Library | HathiTrust | Ongoing | <https://www.hathitrust.org/> | Open (public domain items); member access for others | Public domain / varies |

### Academic Databases & Scholarly Search

| Title | Author/Publisher | Year | URL/DOI | Access | License/Usage Terms |
| --- | --- | --- | --- | --- | --- |
| Google Scholar | Google | Ongoing | <https://scholar.google.com/> | Open search; article access varies | Varies by publisher |
| SSRN (Social Science Research Network) | Elsevier | Ongoing | <https://www.ssrn.com/> | Free with registration | Author-retained copyright; preprints |
| JSTOR | ITHAKA | Ongoing | <https://www.jstor.org/> | Subscription (institutional) | Subscription terms; limited free reading |
| NBER Working Papers | National Bureau of Economic Research | Ongoing | <https://www.nber.org/papers> | Subscription; free for many affiliations | NBER terms of use |
| RePEc / IDEAS | RePEc | Ongoing | <https://ideas.repec.org/> | Open | Varies by hosting archive |

### Financial & Business Datasets

| Title | Author/Publisher | Year | URL/DOI | Access | License/Usage Terms |
| --- | --- | --- | --- | --- | --- |
| WRDS (Wharton Research Data Services) | University of Pennsylvania | Ongoing | <https://wrds-www.wharton.upenn.edu/> | Restricted (institutional subscription) | Subscription agreement; no redistribution |
| CRSP (Center for Research in Security Prices) | University of Chicago | Ongoing | <https://www.crsp.org/> | Restricted (subscription, via WRDS) | Subscription agreement; no redistribution |
| Compustat | S&P Global | Ongoing | <https://www.spglobal.com/marketintelligence/en/> | Restricted (subscription, via WRDS) | Subscription agreement; no redistribution |
| SEC EDGAR | U.S. Securities and Exchange Commission | Ongoing | <https://www.sec.gov/cgi-bin/browse-edgar> | Open | Public domain (U.S. government work) |
| FRED (Federal Reserve Economic Data) | Federal Reserve Bank of St. Louis | Ongoing | <https://fred.stlouisfed.org/> | Open (API key for programmatic access) | FRED terms of use; most series freely usable with attribution |
| World Bank Open Data | World Bank | Ongoing | <https://data.worldbank.org/> | Open | CC BY 4.0 |
| U.S. Census Bureau Data | U.S. Census Bureau | Ongoing | <https://data.census.gov/> | Open | Public domain (U.S. government work) |
| Bureau of Labor Statistics | U.S. Department of Labor | Ongoing | <https://www.bls.gov/data/> | Open | Public domain (U.S. government work) |

## Primary Datasets

Links to downloaded or linked primary datasets. Raw data files should be stored under `data/raw/` (or linked here if too large or restricted).

| Dataset | Source | Location/Link | Retrieved | Notes |
| --- | --- | --- | --- | --- |
| _None yet_ | — | — | — | Pending selection of primary datasets from candidate sources above |

## Data Quality & Coverage Notes

Initial assessment of the candidate sources:

- **Open government data (SEC EDGAR, FRED, Census, BLS)** — high reliability, well-documented, and freely redistributable; good starting point for baseline datasets.
- **Subscription datasets (WRDS, CRSP, Compustat)** — the gold standard for financial research data, but access requires institutional subscription and data cannot be redistributed in this repository; store only derived aggregates or link to access instructions.
- **Working paper archives (SSRN, NBER, GSB Working Papers)** — useful for bibliographic entries and replication data pointers; quality varies since many papers are not yet peer-reviewed.
- **Library catalogs and repositories (SDR, SearchWorks, HathiTrust)** — broad coverage for archival/historical material; per-item license checks required before reuse.

## Restricted Access Follow-ups

Sources requiring outreach or institutional credentials:

- [ ] WRDS/CRSP/Compustat — confirm institutional access and permitted usage
- [ ] JSTOR — confirm institutional access for full-text retrieval
- [ ] NBER — verify affiliation-based free access

## Status

- [x] Compile list of candidate sources
- [x] Verify access and license terms (initial pass; per-item verification ongoing)
- [ ] Download or link primary datasets
- [x] Create sources.md with bibliographic entries
- [x] Add initial notes on data quality and coverage
