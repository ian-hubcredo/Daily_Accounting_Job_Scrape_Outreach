# HR Agency Jobs Scrape Workflow

## Overview

This is a **daily automated pipeline targeting accounting and bookkeeping firms** that are hiring. It scrapes job postings from LinkedIn (two scrapers) and Indeed, uses AI to verify each company's domain and classify their industry, splits leads into bookkeeper vs accountant tracks, finds decision-makers via Apollo, verifies emails through Reoon, logs to separate Google Sheets, and pushes to Instantly and Aimfox for outreach. Nearly identical to the FlexScale Flow but with different credentials and configuration.

## How It Works

```
Schedule (24h) -> Scrape LinkedIn + Indeed -> Filter Accounting Jobs -> AI Verify Domains -> Split Bookkeeper/Accountant -> Apollo Search + Enrich -> Email Verify -> Sheets -> Instantly + Aimfox
```

### Workflow Diagram

```mermaid
flowchart TD
    A["Schedule\nEvery 24 hours"] --> B["LinkedIn + Indeed\nScrape accounting jobs"]
    B --> C["AI Agent - GPT-4.1-mini\nVerify domain + industry"]
    C --> D{"Bookkeeper\nor Accountant?"}
    D -- "Bookkeeper" --> E["Apollo Search + Enrich"]
    D -- "Accountant" --> F["Apollo Search + Enrich"]
    E --> G["Reoon Email Verify"]
    F --> H["Reoon Email Verify"]
    G --> I["Bookkeepers Sheet"]
    H --> J["Accountancy Sheet"]
    I --> K["Instantly + Aimfox"]
    J --> L["Instantly + Aimfox"]

    style A fill:#1B3A4B,color:#fff
    style C fill:#3D5A80,color:#fff
    style D fill:#4A6D7C,color:#fff
    style G fill:#2C5F7C,color:#fff
    style I fill:#274C36,color:#fff
    style J fill:#274C36,color:#fff
```

## Integrations

- **Apify** - LinkedIn and Indeed job scraping
- **OpenAI (GPT-4.1-mini)** - Domain verification and industry classification
- **Tavily** - Web search for domain lookup
- **Apollo.io** - People search and bulk enrichment
- **Reoon** - Bulk email verification
- **Google Sheets** - Separate bookkeeper and accountant sheets
- **Instantly** - Email outreach
- **Aimfox** - LinkedIn outreach

## Setup

1. Import `HR_Agency_Jobs_Scrape_Workflow.json` into your n8n instance.
2. Update all credentials.
3. Activate the workflow to run every 24 hours.
