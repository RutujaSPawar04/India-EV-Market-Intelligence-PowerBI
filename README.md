# India-EV-Market-Intelligence-PowerBI
Power BI dashboard analyzing India's EV market growth, manufacturer competition, and charging infrastructure gaps (2001-2024)

Overview
India's electric vehicle market has grown from a negligible base in 2001 to over 1.5 million annual registrations by 2023, yet the data behind this growth is fragmented across government databases, manufacturer filings, and infrastructure records. This project consolidates five separate datasets into a single interactive Power BI report that lets stakeholders explore market trends, manufacturer competition, and charging infrastructure coverage in one place.

The report was built to answer a question that matters to anyone operating in India's EV space:
   Which segments are growing, who is winning the market, and are the right states being served by charging infrastructure?

Report Structure
The report contains three pages, each answering a distinct set of business questions.

Page 1 — EV Market Overview:
Covers the overall market trajectory from 2001 to 2024. Shows how EV adoption was flat for nearly two decades before accelerating sharply after 2020, driven by policy support, falling battery costs, and aggressive product launches. Key visuals include a long-term growth trend, vehicle category breakdown, and year-on-year growth percentage by year.

Page 2 — Manufacturer and Market Analysis:
Focuses on the competitive landscape among EV manufacturers from 2015 to 2024. Includes a ranked view of the top ten manufacturers by sales volume, a market share breakdown, and a ranking table that updates dynamically based on the year selected.

Page 3 — EV Adoption vs Charging Infrastructure:
The most strategically interesting page. Compares the number of EV manufacturers present in each state against the number of operational public charging stations. Identifies states where manufacturing activity is high but charging infrastructure has not kept pace.

Dataset

Source: Kaggle — Detailed India EV Market Data 2001 to 2024 (https://www.kaggle.com/datasets/srinrealyf/india-ev-market-data)

File	Description
ev_cat_01-24.csv 
Monthly EV registrations by vehicle category from January 2001 to August 2024

ev_sales_by_makers_and_cat_15-24.csv 
Annual EV sales by manufacturer and vehicle category from 2015 to 2024

OperationalPC.csv 
Count of operational public charging stations by Indian state

EV Maker by Place.csv	
EV manufacturer names and their registered state locations

Vehicle Class - All.csv	
Total vehicle registrations by class for penetration context

All five files are included in this repository. No external data connection is required to open the report.

Technical Implementation

Tools used: Power BI Desktop, Power Query, DAX

Data preparation: The manufacturer sales file was stored in wide format with years as column headers. This was unpivoted in Power Query to produce a single Year column and a single Sales column, which enabled proper relationship building and time-based analysis. A garbage row with Date value of zero was removed from the category sales file before loading.

Data model: The model follows a star schema pattern with three fact tables and four dimension tables. A dedicated date dimension was created using the DAX CALENDAR function and marked as the official date table to enable time intelligence calculations. A separate year dimension table was created from the manufacturer sales data to avoid a many-to-many relationship with the date table.

DAX measures:
  Measure	Logic
  Total EV Sales =	SUMX across all vehicle category columns per row
  Total Maker Sales =	SUM of the EV_Sales column after unpivoting
  Previous Year Sales =	CALCULATE with SAMEPERIODLASTYEAR on the date dimension
  YoY Growth % =	DIVIDE of current minus previous year sales over previous year sales
  Total Charging Stations =	SUM of charging station counts by state
  Market Share % = DIVIDE of maker sales over total sales with ALL removing the maker filter
  Distinct Makers	= DISTINCTCOUNT of manufacturer names
  Maker Rank = RANKX over all makers ranked by total sales descending

Key Findings:
Two-wheelers and three-wheelers account for 96 percent of all EV registrations in India. Passenger cars, despite receiving most of the media attention, represent under 4 percent of the market. This reflects India's actual mobility needs rather than the narrative shaped by premium product launches.

The market crossed one million annual registrations for the first time in 2022, representing 209 percent year-on-year growth. 2020 saw a decline of 25 percent due to COVID-19 related disruptions, followed by one of the sharpest recoveries recorded across any automotive segment globally.

Ola Electric, TVS Motor Company, and Ather Energy collectively account for the majority of two-wheeler EV sales. The market is consolidating rapidly despite having over 1,100 registered manufacturers.

Tamil Nadu stands out as the clearest infrastructure gap in the dataset. It is home to eleven EV manufacturers including two of the top three national players, yet has only 643 operational public charging stations compared to Maharashtra's 3,079. This gap represents both a risk to adoption in the state and an opportunity for charging network operators.

How to Open This Project
Download Power BI Desktop from powerbi.microsoft.com (free, Windows only)
Download the file India_EV_Market_Intelligence.pbix from this repository
Open the file in Power BI Desktop
All data is embedded in the file and will load without any additional setup
Repository Contents
India-EV-Market-Intelligence-PowerBI/
|-- README.md
|-- India_EV_Market_Intelligence.pbix
|-- ev_cat_01-24.csv
|-- ev_sales_by_makers_and_cat_15-24.csv
|-- OperationalPC.csv
|-- EV Maker by Place.csv
|-- Vehicle Class - All.csv

Background:
This project was built as a self-initiated exercise to develop practical Power BI skills using real government and industry data. Every step from raw data inspection through data modeling to DAX measure development was completed independently. The documentation file in this repository contains detailed notes on every decision made during the build, including why specific transformations were applied, how relationships were designed, and what each DAX formula does.
This project was built as a self-initiated exercise to develop practical Power BI skills using real government and industry data. Every step from raw data inspection through data modeling to DAX measure development was completed independently. The documentation file in this repository contains detailed notes on every decision made during the build, including why specific transformations were applied, how relationships were designed, and what each DAX formula does.
