# Smart Mobility and Traffic Flow Optimization in Austin Using IoT Bluetooth Sensors

## Project Overview
This project analyzes Austin's smart mobility sensor data to understand congestion patterns, segment performance, and travel-time reliability across the city's transportation network. Using matched travel data and 15-minute aggregated segment summaries, we examined delay trends, identified peak-time bottlenecks, predicted high-risk delays, and measured recovery times to free-flow speeds.

**Team A04**: Sambisha Godi (Project Manager), Li-Hsin Chang, Margaret Croghan, Steven Marathias, Tanish Puneeth

## 📊 Project Highlights
- **Data Size**: ~25.4 GB total (ITMF: 14GB, TMSR: 11.4GB)
- **Records**: ~165 million data points
- **Key Findings**: Urban segments are consistently slowest, short segments are disproportionately affected by congestion, critical corridors experience extended recovery times
- **Visualization**: Interactive Tableau dashboards for real-time insights
- **Technologies**: BigQuery, Python, SQL, Tableau, Google Colab

## 🎯 Problem Statement
Urban congestion remains a pressing challenge for modern cities, impacting travel reliability, economic productivity, and quality of life. This project aims to:
- Identify roadway segments with highest traffic density and slowest average speeds
- Compare travel times across different hours and days to detect congestion trends
- Examine origin-destination movement patterns and asymmetric routes
- Evaluate segment length vs. average speed relationships to identify bottlenecks

## 📁 Dataset Details

### **1. Bluetooth Travel Sensors – Individual Traffic Match Files (ITMF)**
- **Source**: [City of Austin Data Portal](https://data.austintexas.gov/)
- **Size**: ~14.0 GB | Rows: ~103M | Columns: 11
- **Content**: Individual Bluetooth device detections with timestamps and location details
- **License**: Public Domain

### **2. Bluetooth Travel Sensors – Traffic Match Summary Records (TMSR)**
- **Source**: [City of Austin Data Portal](https://data.austintexas.gov/)
- **Size**: ~11.4 GB | Rows: ~61.9M | Columns: 16
- **Content**: Aggregated summaries of travel times and average speeds in 15-minute intervals
- **License**: Public Domain

## 🔧 How Data Is Collected (AWAM System)
Austin uses the **Anonymous Wireless Address Matching (AWAM)** system for privacy-safe traffic monitoring:

1. **Sensors**: AWAM field devices detect anonymous Bluetooth signals from passing vehicles (phones, infotainment systems, GPS devices)
2. **Anonymization**: All raw signals are anonymized immediately—no personal identities are ever stored
3. **Tracking**: As vehicles pass sensors, the system records time and location
4. **Calculation**: When the same anonymous signal is detected at another sensor, AWAM calculates:
   - Travel time between points
   - Speed
   - Time of day, day of week, and station pairing
5. **Processing**: AWAM Host Software processes millions of detections into ITMF and TMSR datasets

## 📊 Key Insights

### **1. Citywide Traffic Patterns**
- **Peak Congestion**: 5-7 PM weekdays show slowest average speeds
- **Densest Areas**: Loop 360 and downtown Lamar-5th/6th/Lavaca corridors
- **Slowest Segments**: RM 620 bottlenecks and downtown Congress Avenue

### **2. Temporal Analysis**
- **Busiest Days**: Tuesday-Thursday (slowest speeds, longest travel times)
- **Peak Hours**: 5-7 PM show highest congestion citywide
- **Recovery Times**: Most segments recover in <15 minutes, but chronic bottlenecks take 12-18 hours

### **3. Origin-Destination Insights**
- **Top Origins**: Lamar Blvd intersections dominate (Lamar & Oltorf, Barton Springs, Blue Bonnet)
- **Top Destinations**: Lamar & Oltorf is busiest endpoint
- **Asymmetric Routes**: Several corridors show 4-5x slower travel in one direction

### **4. Segment-Level Engineering**
- **Short Segments**: Consistently slower across all area types (Urban: 17 mph vs 22 mph)
- **Long Recovery**: Chronic bottlenecks on US-290, Loop 1, and TX-71 corridors
- **Area Types**: Urban segments show biggest speed disparity between short/long segments

## 🛠️ Technical Implementation

### **Data Cleaning & Preparation**
- Filtered invalid matches and unrealistic travel times
- Standardized origin/destination identifiers
- Removed duplicates and ensured proper timestamp formatting
- Handled negative travel times and extreme outliers
- Created 15-minute time buckets for consistent aggregation

### **SQL & BigQuery Operations**
- Created ER diagram with SENSOR, DETECTION, and MATCHED_TRAVEL tables
- Performed complex joins between ITMF and TMSR datasets
- Implemented window functions for peak detection and recovery analysis
- Used approximate quantiles for outlier detection

### **Visualization**
- **Tableau Dashboard 1**: Congestion Patterns and Segment Performance
- **Tableau Dashboard 2**: Origin-Destination Analysis and Travel Time Distributions

## 📈 Tableau Dashboards

### **Dashboard 1: Congestion Patterns & Segment Performance**
[![Tableau Dashboard 1](https://img.shields.io/badge/Tableau-Dashboard_1-blue)](https://public.tableau.com/app/profile/maggie.croghan/viz/Team4-FinalDashboard1/CongestionPatternsandSegmentPerformanceDashboard?publish=yes)

**Features**:
- Hourly congestion index
- Top 10 slowest segments
- Speed by time of day
- Day-of-week comparisons

### **Dashboard 2: OD Analysis & Travel Time Reliability**
[![Tableau Dashboard 2](https://img.shields.io/badge/Tableau-Dashboard_2-green)](https://public.tableau.com/views/dashboard2_17652280043810/Dashboard2?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

**Features**:
- Top origin-destination pairs
- Travel time distributions
- Speed by time of day
- Travel time reliability metrics

## 📁 Project Structures
