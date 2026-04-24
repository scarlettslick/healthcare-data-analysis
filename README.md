# The Hidden Math of Medicare: What Hospitals Bill vs. What They Get Paid

## Overview
This project analyzes 2023 CMS Medicare inpatient data to investigate the gap between 
what hospitals bill and what they actually receive. Using Malloy and DuckDB, I queried 
146,000+ records spanning every U.S. state to uncover patterns in hospital billing 
behavior across procedures, states, and individual institutions.

## The Problem
Anyone who has received a hospital bill has probably noticed the numbers don't add up. 
A procedure costs $150,000 on paper, insurance pays $18,000, and somehow that's 
considered settled. This project started with a simple question: is this gap random, 
or is there a systematic pattern to how hospitals inflate their bills? The answer turns 
out to be clearly the latter — and the scale of it is staggering.

## How It Works
All analysis is done in Malloy, a new query language built on DuckDB that compiles to 
SQL. The `.malloynb` notebook file contains the full story arc with queries and 
narrative. The `.malloy` file contains the source definition and all individual queries.

**Data source:** CMS Medicare Inpatient Hospitals by Provider and Service (2023)  
**Tool:** Malloy + DuckDB via VS Code extension  
**Rows:** 146,000+

## Key Findings

**1. Florida and California dominate Medicare volume** at ~442,000 discharges each, 
despite California having a much larger population.

**2. Nevada bills nearly 9x what it gets paid.** Average billed: $157,565. 
Average paid: $17,855. Less than 12 cents on the dollar.

**3. The most extreme procedures show the biggest gaps.** ECMO procedures in Nevada 
are billed at $1.46 million on average but paid only $173,854 — an 88% markdown.

**4. This is a nationwide pattern, not a Nevada quirk.** Every state bills over 
$900,000 for the same ECMO procedure. Washington state gets the best payment ratio 
on this list, collecting $308,494 on a $1.1M bill.

**5. Sepsis is the most common Medicare condition** with 561,795 discharges nationally. 
Hospitals bill $74,730 per case but receive $17,235 — a gap that adds up to tens of 
billions of dollars in aggregate.

**6. Individual hospitals tell the starkest story.** Hackensack Meridian in New Jersey 
bills $542,972 on average. Stanford Health Care handles 11,001 discharges at $469,691 
average billed. Faith Community Hospital in tiny Jacksboro, TX collects the best 
payment ratio of any top-billing hospital.

## What I Learned
The biggest surprise was that the billing gap isn't driven by a few extreme outliers — 
it's completely uniform across states, procedure types, and hospital sizes. I expected 
to find a few bad actors. Instead I found a system where inflated list prices appear to 
be standard practice industry-wide. Malloy made it easy to slice this data in multiple 
directions quickly, though learning the syntax took some adjustment coming from SQL. 
If I were to extend this project I would bring in hospital ownership data (nonprofit vs. 
for-profit) to see whether that explains any of the variation in payment ratios.

## Who Would Care
Healthcare policy analysts, insurance companies, and hospital administrators would find 
this useful for benchmarking billing practices. Journalists covering healthcare costs 
could use this data to identify specific hospitals worth investigating. Patients 
navigating medical bills could use state-level payment ratio data to understand what 
insurers are actually paying versus the sticker price they see on their EOB.

## How to Run
1. Install the [Malloy VS Code extension](https://marketplace.visualstudio.com/items?itemName=malloydata.malloy-vscode)
2. Clone this repo
3. Download the source data from [CMS](https://data.cms.gov/provider-summary-by-type-of-service/medicare-inpatient-hospitals/medicare-inpatient-hospitals-by-provider-and-service) and convert to UTF-8: