![1e654488-8a28-47e1-ad88-83036c4ba40f](https://github.com/user-attachments/assets/8a4ea79f-b333-442a-b457-05b72a67183f)


# 🔭 Features:
IThis project sets out to create an ETL and data dashboard that can:
- Analyse and reconcile affiliate network data against internal metrics to identify tracking discrepancies, revenue leakage, and commission inaccuracies.
- Conduct performance and commission audits, ensuring correct CPA rates, sub-ID tracking, and overall partner integrity.
- Build models and insights to uncover revenue opportunities, optimise conversion paths, and recommend strategic upsells or product/technical fixes.
- Develop and maintain reporting and dashboards covering key operational metrics such as decline rates, tracking-error volume, and post-transaction conversion.
- Partner with Product, Engineering, and Data teams to diagnose tracking issues, build automated alerting and improve data quality
- Support Commercial teams with data-driven business cases and predictive models to identify opportunities for affiliate growth and/or leakage recovery





# 🔩 Technologies:
- Event-level analytics platforms (e.g., Snowplow, GA360/BigQuery, Adobe Analytics)
- Excel/Sheets
- SQL SnowFlake
- Python
- Power Bi
- JPype
- JSON
- Pandas



# ♟️ The Process:
Began by gathering three data sources: Affiliate Network Data, Internal Product/Transaction Data, and Tracking Metadata.

Resulting sheets include:

1) Affiliate Network Clickstream (event‑level)  <br>
click_id / timestamp / affiliate_id / publisher_name / sub_id / device_type / country / landing_page / commission_rate / network_session_id
    >Required to track click‑to‑conversion drop‑off, invalid clicks, partner quality, sub‑ID consistency.
    <br>
    

2) Affiliate Network Conversions (network‑reported)  <br>
conversion_id / click_id (foreign key) / order_value / commission_amount / currency / conversion_status (approved, pending, declined) / decline_reason / attribution_model / transaction_timestamp <br>
    >Required to detect revenue leakage, over‑ or under‑payment, incorrect CPA rates, missing sub‑IDs.
    <br>
    
3) Internal Orders (source of truth)  <br>
order_id / user_id / order_value / payment_status / fraud_flag / product_category / order_timestamp / utm_source, utm_medium, utm_campaign / session_id <br>
    >Anchoring for reconciling network vs. internal revenue, identifying untracked affiliate orders, validating decline reasons, building conversion paths.
    <br>


4) Tracking Metadata (Snowplow‑style event data)  <br>
page_view_id / session_id / user_id / event_type (page_view, click, purchase, etc.) / affiliate_click_context (JSON) / device, browser, geo / referrer / sub_id <br>
    >Which allows for rebuilding journeys, detecting broken tracking, validating partner integrity, identify missing or malformed parameters.
    <br>
    

In response to the gathered data, we are wanting to understand general questions surrounding integrity/performance audits, like: 
- How many affiliate conversions are missing from internal data? 
- Which partners have the highest decline rates and why?
- Where is revenue leakage occurring?
- Which sub‑IDs are underperforming or mis‑tracking?
- What is the true CPA vs. what the network is charging?
- Which partners drive high‑value vs. low‑value customers?
<br>

To create a data model which can audit the data, we require a modeled data set to flag for our determined auditing needs:
(Note for WIP: essentially I extract these initial 4 data sheets, then use sql to validate the data, then anywhere the data does not validate I want it to return those invalidations to which a new sheet is created for my report)
<br>
Acheived through SQL logic parameters
<br>
Sub‑ID mismatch
>CASE WHEN sub_id_click != sub_id_conversion OR sub_id_click != sub_id_internal THEN 'subid_mismatch' END
<br>
Missing order
>CASE WHEN conversion_id IS NOT NULL AND order_id IS NULL THEN 'missing_order' END
<br>
Invalid CPA
>CASE WHEN commission_amount != order_value_network * cpa_rate THEN 'invalid_cpa' END
<br>

5) Resulting Table  <br>
click_id / network_order_value / internal_order_value /	discrepancy_flag / reason <br>

<br>
Of which will follow a dashboard tracking these decline rates, revenue leakages, sub-ID performances, conversion funnels, along with a short written report to draw attention to our findings.


# 🎬 Preview:


# 👁️‍🗨️ Insights:
-
-
-
-
-

# 🗳️ Lessons and Improvements:
- 
-
-
-
-
