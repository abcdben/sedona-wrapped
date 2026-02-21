# Sedona Conference Citation Collector

Collects citations to The Sedona Conference from CourtListener's case law database and RECAP Archive (federal court filings).

## Quick Start

### 1. Get a CourtListener API Token (free)

1. Sign up at https://www.courtlistener.com/sign-in/
2. Get your token at https://www.courtlistener.com/help/api/rest/

### 2. Set Your Token

```bash
export COURTLISTENER_API_TOKEN="your-token-here"
```

Or pass it directly when running:
```bash
python sedona_citation_collector.py --token YOUR_TOKEN
```

### 3. Run Collection

```bash
# Quick test (50 results per query)
python sedona_citation_collector.py --test

# Standard run (100 results per query)
python sedona_citation_collector.py

# Full collection (all results - may take a while)
python sedona_citation_collector.py --full

# Include additional specific searches (Sedona Principles, Cooperation Proclamation, etc.)
python sedona_citation_collector.py --full --include-specific
```

## Output Files

Results are saved to `./sedona_data/`:

| File | Description |
|------|-------------|
| `sedona_opinions.json` | Judicial opinions citing Sedona (federal + state) |
| `sedona_recap_documents.json` | Court filings from RECAP (motions, briefs, etc.) |
| `sedona_citations_combined.csv` | Combined dataset for analysis |
| `summary_stats.json` | Aggregate statistics |

## Data Fields

### Opinions
- `case_name`, `court`, `court_id`, `date_filed`
- `citation` (parallel citations)
- `snippet` (context around the Sedona mention)
- `jurisdiction` (federal/state)
- `court_level` (supreme/appellate/district/bankruptcy/etc.)

### RECAP Filings
- `case_name`, `court`, `court_id`, `date_filed`
- `description` (document type/title)
- `snippet` (context around the Sedona mention)
- `docket_number`, `pacer_doc_id`

## Search Queries

Default searches:
- `"Sedona Conference"`
- `"Sedona Conf"`

With `--include-specific`:
- `"Sedona Principles"`
- `"Sedona Cooperation Proclamation"`
- `"Sedona Commentary"`

## Coverage

| Source | Opinions | Filings (briefs, motions) |
|--------|----------|---------------------------|
| Federal | ✅ | ✅ (RECAP Archive) |
| State | ✅ | ❌ (no centralized source) |

## Next Steps: Building the Dashboard

Once you have the data, the visualization can include:

1. **Volume metrics**: Total citations, opinions vs. filings
2. **Trend lines**: Citations by year (inflection points around rule changes, major cases)
3. **Geographic breakdown**: By circuit, by state
4. **Court level analysis**: SCOTUS → Circuit → District → Bankruptcy
5. **Document type breakdown**: What types of filings cite Sedona most?
6. **Which commentaries get cited**: Principles vs. Cooperation Proclamation vs. specific commentaries
7. **Citation context classification**: (future enhancement - LLM-assisted categorization of how Sedona was used)

## Known Limitations

- CourtListener is comprehensive but not exhaustive—Westlaw/Lexis may have additional citations
- RECAP only covers federal filings that have been contributed to the archive
- State court filings are not available (no centralized source exists)
- Citation context (approved vs. distinguished) would require additional classification
