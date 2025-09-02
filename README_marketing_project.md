# Marketing Analytics Portfolio Project (Dummy Data)

This project demonstrates a complete marketing analytics workflow in **Power BI**, using synthetic data covering 2025-05-01 to 2025-07-31 across these channels:

- Google Ads
- Facebook Ads
- LinkedIn Ads
- Email
- Organic Search
- Referral

## Files
- `marketing_daily.csv` — daily channel-level metrics (impressions, clicks, leads, conversions, spend, revenue).
- `dim_channel.csv` — channel metadata (paid vs non-paid).
- `dim_date.csv` — calendar table for modeling.
- `stages.csv` — helper table for building a Funnel visual via a SWITCH measure.

## Suggested Power BI Measures (DAX)

```DAX
-- Date table (if you don't use the provided CSV)
Date = CALENDARAUTO()

Total Impressions = SUM(marketing_daily[impressions])
Total Clicks = SUM(marketing_daily[clicks])
Total Leads = SUM(marketing_daily[leads])
Total Conversions = SUM(marketing_daily[conversions])
Total Spend = SUM(marketing_daily[spend])
Total Revenue = SUM(marketing_daily[revenue])

CTR = DIVIDE([Total Clicks], [Total Impressions])
CVR = DIVIDE([Total Conversions], [Total Clicks])
Lead Rate = DIVIDE([Total Leads], [Total Clicks])
CPC = DIVIDE([Total Spend], [Total Clicks])
CPA = DIVIDE([Total Spend], [Total Conversions])  -- aka CAC for acquisition
ROAS = DIVIDE([Total Revenue], [Total Spend])
CPM = DIVIDE([Total Spend], DIVIDE([Total Impressions], 1000))

-- Funnel helper (requires 'stages' table)
Funnel Value =
    SWITCH(
        SELECTEDVALUE(stages[stage]),
        "Impressions", [Total Impressions],
        "Clicks", [Total Clicks],
        "Leads", [Total Leads],
        "Conversions", [Total Conversions]
    )
```

## Suggested Report Pages
1. **Overview** — KPIs (Spend, Revenue, Conversions, ROAS, CPA), date & channel slicers, line chart of Revenue vs Spend, bar chart of Conversions by Channel.
2. **Acquisition Funnel** — Funnel visual using `stages[stage]` and `[Funnel Value]`, plus CTR/CVR cards.
3. **Campaigns** — Table or bar chart by `campaign` showing Spend, Conversions, CPA, ROAS.
4. **Trends** — Monthly/weekly trend lines for Spend, Clicks, Conversions, Revenue.

## How to Use
1. Open Power BI Desktop → **Get Data** → **Text/CSV** → import all CSVs.
2. Mark `dim_date[date]` as **Date** type and relate to `marketing_daily[date]`.
3. Relate `dim_channel[channel]` to `marketing_daily[channel]`.
4. Create DAX measures above and build visuals.
5. Export screenshots and write a short case study in your GitHub README.

## Notes
- Data are synthetic and for portfolio demonstration only.
- You can fork this and extend: add budgets, multi-touch attribution, or cohorts.
