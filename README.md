# Marketing Analytics — Portfolio Project

**Context:** E-commerce brand wants to identify best-performing marketing channels (May–July 2025).  
**Data:** Daily channel-level metrics (impressions, clicks, leads, conversions, spend, revenue).  
**Deliverables:** Power BI report with Overview, Acquisition Funnel, Campaigns, Trends pages.

## How to open
1. Import CSVs from `/data/` into Power BI Desktop.
2. Create relationships: `dim_date.date -> marketing_daily.date`, `dim_channel.channel -> marketing_daily.channel`.
3. Add measures (CTR, CVR, ROAS, CPA) and build visuals.

## Artifacts
- pbix: `/pbix/marketing_report.pbix`
- screenshots: `/images/`
