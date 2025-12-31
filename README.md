# Washington-State-EV-Population-Analysis
"Washington State's EV market has matured from a niche Tesla-dominated sector into a rapidly expanding ecosystem where BEVs lead adoption, yet infrastructure and policy eligibility remain critical filters for regional growth."

#### Project Overview & Context
Washington State is a leader in EV adoption, having recently mandated that 100% of new car sales must be electric by 2030. This dataset, provided by the Washington State Department of Licensing (DOL), contains roughly 150,000 records of every Battery Electric Vehicle (BEV) and Plug-in Hybrid (PHEV) currently registered in the state.

#### The Goal
To evaluate the current landscape of electric vehicle adoption in Washington State, identifying market leaders, regional "hotspots," and the impact of range capabilities on policy eligibility.

#### The Objectives
- Market Analysis: Identify the top 10 EV manufacturers and models dominating the state.
- Geospatial Trends: Map EV density to distinguish between urban and rural adoption rates.
- Policy Impact: Analyze the relationship between Electric Range and Clean Alternative Fuel Vehicle (CAFV) eligibility.
- Growth Forecasting: Visualize the surge in registrations from 2011 to the present.

#### Data Transformation & ETL Process
I utilized Power Query (M) to transform the raw Washington DOL dataset into an analysis-ready "Gold" format. The cleaning process followed these critical phases:

#####  Structural Standardization
- Schema Definition: Managed data types by specifically casting Model Year to integers and Postal Code to text to preserve leading zeros.
- Header Promotion: Ensured correct attribute mapping by promoting the first row to headers.
- Naming Conventions: Renamed ambiguous columns to business-friendly terms for easier reporting.

##### Data Quality & Cleansing
- Value Normalization: Used multiple Replaced Value steps to fix typos, standardize manufacturer names (e.g., merging "TESLA INC" into "Tesla"), and handle "Unknown" entries.
- Case Consistency: Applied Capitalize Each Word to the City and Make columns to prevent duplicate entries in visuals caused by casing inconsistencies.
- Handling Nulls: Utilized Filled Down logic to address missing geographic data where appropriate, ensuring a 100% completion rate for mapping visuals.

##### Advanced Transformation & Feature Engineering
- Row Filtering: Filtered the dataset to focus exclusively on Washington State registrations to maintain regional accuracy.
- Index Creation: Added an Index column to facilitate Cumulative (Running Total) calculations and Pareto analysis without a standard date table.
- Sorted Reliability: Implemented Sorted Rows to ensure that "Filled Down" logic and historical trends were applied in the correct chronological order.


##### The "Truncated VIN" Ambiguity
- The Challenge: The dataset utilizes truncated 10-character VINs for privacy. This led to thousands of "duplicate" rows when using VIN as a unique identifier, as many vehicles share the same Year, Make, and Model.
- The Solution: I shifted the data architecture to use the DOL Vehicle ID as the Primary Key. This allowed for 100% accurate vehicle counts while still using the truncated VIN to categorize vehicle "types" for market-segment analysis.

##### Manual Data Entry & "Dirty" Manufacturers
- The Challenge: Inconsistent data entry from different DOL sources resulted in multiple variations of the same brand (e.g., "TESLA INC," "TESLA MOTORS," and "Tesla").
- The Solution: I implemented a series of Replaced Value steps in Power Query and utilized the Capitalize Each Word transformation. This normalized 100% of the manufacturer names, ensuring that market share visuals (like the Pareto chart) were not split across redundant categories.

##### Handling "Zero-Range" BEVs
The Challenge: Several Battery Electric Vehicles (BEVs) were listed with an Electric Range of 0. This skewed the "Average Range" KPI and suggested a lack of technical reliability.
The Solution: Rather than deleting the data, I Implemented Sorted Rows to ensure that "Filled Down" logic and historical trends were applied in the correct chronological order.

##### The "Adoption Inflection" Point
- Finding: While early growth (2011–2017) was linear, the market entered a Polynomial (curved) growth phase starting in 2020.
- Data Point: Cumulative registrations jumped by 48% between 2022 and 2024 alone.
- Why it matters: This suggests Washington is moving past the "Early Adopter" phase and into the "Early Majority" stage of the technology adoption lifecycle.

##### Tesla’s Dominance vs. Rising Competition
- Finding: Tesla remains the undisputed market leader with a 51% market share (driven primarily by the Model Y and Model 3). However, its absolute dominance is beginning to "thinned out" as legacy automakers enter the field.
- Data Point: Competitive makes now account for 64% of new registrations, a 20% increase from three years ago.
- Pareto Insight: The top 3 manufacturers (Tesla, Chevrolet, and Nissan) account for roughly 80% of the total EV population, confirming a highly concentrated market.

##### Geographic "Hotspots" & Urban Concentration
- Finding: EV adoption is not uniform. It is heavily concentrated in the Greater Seattle Area (King County), which accounts for over 50% of all state registrations.
- Data Point: The density of EVs per 1,000 residents is highest in ZIP codes with robust charging infrastructure, while rural counties like [Insert Rural County Name] show adoption rates below 1%.
- Why it matters: This indicates that "Range Anxiety" and infrastructure gaps remain the primary barriers to adoption outside of major urban hubs.

##### Policy Impact: The "CAFV Eligibility" Gap
- Finding: Government incentives are a major driver of choice. 70% of current EVs on the road are eligible for the Clean Alternative Fuel Vehicle (CAFV) tax exemptions.
- Data Point: There is a "Policy Gap" where 30% of vehicles (mostly older models or short-range PHEVs) do not meet the 35+ mile electric-only range requirement for state tax breaks.
- Why it matters: This suggests that as range technology improves, more consumers are "buying into" the eligible bracket to save on transaction costs.

##### Technology Shift: BEV vs. PHEV
- Finding: Washingtonians overwhelmingly prefer pure Battery Electric Vehicles (BEVs) over Plug-in Hybrids (PHEVs).
- Data Point: BEVs make up 80% of total registrations, while PHEVs hold only 20%.
- Why it matters: This preference for BEVs shows a strong consumer confidence in battery range and a desire to completely move away from gasoline, rather than using a hybrid "bridge."


#### Conclusion
This analysis confirms that Washington State is no longer in the "experimental" phase of electric vehicle adoption. We have moved into a mass-market transition, characterized by high adoption velocity and a diversifying competitive landscape. While Tesla remains the dominant player, the growth of legacy automakers and the direct impact of CAFV policy eligibility are the new primary drivers of market composition.

