# Retail Analytics Performance Dashboard

## Executive Summary

The Executive Summary page provides a high-level view of overall retail business performance, designed for senior management and decision-makers to quickly assess financial health and operational efficiency.

This page highlights key KPIs such as Total Sales, Profit, Profit Margin %, Target Achievement %, Budget Utilization %, Total Discount, and Cost metrics, enabling stakeholders to compare actual performance against targets and budgets at a glance.

A rolling 12-month and 6-month sales trend is included to help identify overall business direction while smoothing short-term fluctuations, allowing management to focus on sustained performance rather than isolated monthly changes.

Regional performance insights identify the most profitable region and the fastest-growing region, supporting strategic geographic decisions. Category-level contribution and ranking further help management understand which product categories drive revenue and profitability.

Interactive slicers and bookmark-driven navigation allow users to dynamically filter the analysis by year, month, region, and category, enabling both high-level monitoring and contextual exploration without overwhelming the user.

### Preview
![Executive Summary](Screenshots/01%20Executive%20Summary.png)

## Sales Performance

The Sales Performance page provides a unified view of revenue trends across Monthly, Quarterly, and Yearly time horizons using a single page with bookmark-based navigation.

### Business Objective
Enable stakeholders to monitor sales performance over different time granularities while maintaining a consistent layout and comparable KPIs, without duplicating report pages.

### Key Insights Provided
- Current vs Previous period sales with absolute and percentage growth (MoM / QoQ / YoY)
- Sales trend comparison between Current Year and Last Year
- Top 5 Products and Top 5 Categories by sales contribution
- Target achievement status and variance analysis
- Forecast performance and trend direction indicators

### Time Intelligence & Selection Logic
This page uses **disconnected date tables** for Monthly, Quarterly, and Yearly analysis:
- Monthly view: Month & Year
- Quarterly view: Quarter & Year
- Yearly view: Year

Selection behavior is designed for usability:
- If no period is selected, the latest available period is automatically shown
- If multiple periods are selected, the latest period from the selection is considered
- This ensures stable KPIs and avoids ambiguous results

### Interactivity & Navigation
- Bookmark-based toggles switch between Monthly, Quarterly, and Yearly views while preserving layout consistency
- Slicer panel allows filtering by Year, Month / Quarter, Region, and Category
- Informational tooltips explain period selection logic and filter behavior to guide users

### Technical Highlights
- Disconnected tables used to control time context independently
- Measures dynamically resolve the latest period using MAX logic
- Same KPI measures reused across all views, improving maintainability
- Comparison visuals selectively ignore slicers where required to preserve analytical intent

### Preview
![Sales Performance](Screenshots/02a%20Sales%20Performance%20-%20Monthly.png)
![Sales Performance](Screenshots/02b%20Sales%20Performance%20-%20Quarterly.png)
![Sales Performance](Screenshots/02c%20Sales%20Performance%20-%20Yearly.png)

## Product Movement Overview

The Product Movement Overview page is designed to analyze product-level performance by combining sales contribution, profit margin behavior, and movement velocity to support inventory and assortment decisions.

### Business Objective
Help business and supply chain teams identify fast-moving, slow-moving, and high-impact products, while understanding how different product segments contribute to overall revenue and margin.

### Key Insights Provided
- Top-performing product by total sales and contribution
- High-margin vs low-margin product counts and their respective sales impact
- Overall product count with average profit margin and transaction behavior
- ABC classification (A / B / C segments) based on cumulative sales contribution
- Identification of fast-moving and slow-moving products using transaction activity and recency

### ABC Segmentation Logic
- Products are classified into **A, B, and C segments** using a disconnected ABC segmentation table
- ABC segments are calculated based on cumulative sales contribution
- Separate visuals highlight:
  - Total sales by ABC segment
  - High-margin product sales by ABC segment
  - Low-margin product sales by ABC segment
- Percentage values dynamically recalculate based on visible products and selected filters

### Product Movement Analysis
- Products are categorized as **Fast**, **Medium**, or **Slow** moving using:
  - Transaction count
  - Days since last sale
- Movement category is shown at both:
  - Transaction-level context
  - Overall product behavior level
- This enables quick identification of products that require replenishment, promotion, or rationalization

### Interaction & Filtering Behavior
- Page slicers allow filtering by Year, Month, Region, and Category
- ABC segment selection updates all dependent visuals dynamically
- Due to the use of a disconnected ABC table, traditional drill-through is not applicable
- Instead, a **matrix-based product overview** is used to display detailed information for selected ABC segments, ensuring clarity without breaking filter logic

### Technical Highlights
- Disconnected tables used for ABC segmentation to maintain calculation control
- Cumulative percentage logic implemented for accurate ABC classification
- Matrix visual used as a drill-through alternative for disconnected segmentation
- Measures dynamically recalculate contribution and cumulative values based on filter context

### Preview
![Product Movement](Screenshots/03%20Product%20Movement%20Overview.png)

## Product Deep Dive

The Product Deep Dive page focuses on analyzing an individual product in depth by combining customer behavior, store-level dependency, return risk, profitability concentration, and inventory status.

### Business Objective
Enable stakeholders to evaluate whether a product is healthy, risky, or over-dependent on specific stores, while supporting decisions related to pricing, assortment optimization, inventory planning, and store strategy.

### Key Insights Provided
- Average spend per customer and customer count for the selected product
- New vs existing customer split and repeat purchase rate
- Store-level dependency and return risk analysis
- Profit concentration and volume dependency across stores
- Inventory status indicators including stock availability, restock recency, and risk level

### Store Dependency vs Return Impact
- Bubble chart represents **store-level dependency** for the selected product
- X-axis shows store sales contribution, indicating dependency on individual stores
- Y-axis shows product return rate, highlighting return or quality risk
- This helps identify:
  - High dependency with high return risk (operational concern)
  - High dependency with low return risk (healthy performance)
  - Low impact stores with minimal risk

### Profit Concentration & Volume Dependency
- Analyzes how product profit is distributed across stores
- Bubble size represents sales volume, highlighting volume-driven profit
- Identifies whether profit is:
  - Concentrated in a few stores (risk exposure)
  - Distributed across multiple stores (stable performance)
- Supports decisions on store diversification and dependency reduction

### Inventory Context
- Inventory KPIs provide operational context alongside sales performance:
  - Days since last restock
  - Current stock on hand
  - Stock status and risk level indicators
- This ensures sales insights are evaluated together with supply-side readiness

### Interactivity & Guidance
- Product-level slicers allow focused analysis by Year, Month, Product, and Category
- Informational tooltips explain how to interpret dependency, return risk, profit concentration, and volume behavior
- Designed to support self-service analysis without requiring external explanation

### Technical Highlights
- Dynamic product-level measures respond to slicer selections
- Store-level dependency, return rate, and profit contribution calculated using context-aware ranking measures
- Both scatter charts are controlled using a **Top N store logic**:
  - Displays Top 10 stores by the respective ranking metric
  - If fewer than 10 stores exist, the visual automatically adjusts to the available count
- Top N logic implemented using measure-based visual filters rather than static filters
- Same Top N pattern reused across visuals with different ranking measures for consistency and performance
- Bubble charts used to combine dependency, risk, profit concentration, and volume in a single visual

### Preview
![Product Deep Dive](Screenshots/04%20Product%20Deep%20Dive.png)

## Customer Insight

The Customer Insight page focuses on understanding customer health, value, profitability, and churn risk to support retention strategies, revenue growth, and customer segmentation decisions.

### Business Objective
Provide a consolidated view of customer performance by combining engagement, lifetime value, profitability segmentation, and churn risk indicators.

### Key Metrics Overview
- Active, returning, new, and churned customer counts
- Retention rate to assess customer stickiness
- Average revenue per customer (ARPC) and average order per customer (AOPC)
- Customer Lifetime Value (CLV) at both average and total levels

### Customer Value & Profitability Segmentation
- Customers are segmented based on:
  - **CLV tiers** (Platinum, Gold, Silver)
  - **Profitability segments** (A, B, C)
- Helps identify high-value and high-profit customers who drive long-term revenue
- Enables targeted retention and upsell strategies

### Customer Behavior Analysis
- Purchase gap highlights buying frequency patterns
- Repeat customer rate indicates loyalty strength
- Cross-sell and upsell indices assess expansion potential within the customer base

### Churn Risk Segmentation
- Customers classified into Low, Medium, and High churn risk segments
- Supports early identification of customers requiring retention intervention
- Designed to complement retention and lifecycle management strategies

### Insights Summary
- Consolidated insight panel provides a quick health check of:
  - Customer value
  - Profitability
  - Churn risk exposure
- Enables decision-makers to quickly assess whether immediate action is required

### Interactivity & Logic
- Time-based slicers control the reporting period
- If no period is selected, the latest available period is automatically applied
- If multiple periods are selected, the most recent period from the selection is used
- Ensures consistent and intuitive period-based analysis across the page

### Preview
![Customer Insight](Screenshots/05%20Customer%20Insight.png)

## Store Performance

The Store Performance page provides a comprehensive view of store-level performance by combining sales, profitability, operational efficiency, and risk segmentation into a single, interactive analysis.

### Business Objective
Enable stakeholders to identify top-performing and underperforming stores, compare regional performance, evaluate operational efficiency, and assess store-level risk exposure.

### Key Performance Overview
- Store-level Sales, Cost, Profit, and Profit Margin
- Average sales per store and active store count
- Month-over-Month (MoM) growth tracking
- Best and worst performing stores highlighted for quick comparison

### Store Ranking & Comparison
- Stores are ranked dynamically based on sales performance
- Top and bottom performing stores are highlighted to support performance benchmarking
- Ranking responds to slicer selections without breaking overall context

### Regional Analysis
- Sales and profit distribution across regions
- Identifies:
  - Highest contributing regions
  - Regions with stronger profitability
- Supports geographic expansion and regional optimization decisions

### Operational Metrics
- Store efficiency indicators such as:
  - Average basket size
  - Total transactions
  - Transactions per store
- Weekday vs weekend comparison highlights demand patterns and operational load
- Helps optimize staffing, promotions, and store operations

### Store Segmentation
- Stores are classified into High, Medium, and Low segments based on:
  - Sales contribution
  - Profit contribution
- Risk segmentation identifies stores with:
  - Negative growth
  - Low profitability
  - Low contribution impact
- Enables proactive management of high-risk and underperforming stores

### Interactivity & Navigation
- Bookmark-driven navigation allows switching between:
  - Regional Analysis
  - Operational Metrics
  - Store Segment views
- Slicers enable filtering by Year, Month, Region, and Store
- Informational tooltips guide users on segmentation logic and risk interpretation

### Preview
![Store Performance](Screenshots/06a%20Store%20Perfomance%20-%20Region%20Analysis.png)
![Store Performance](Screenshots/06b%20Store%20Perfomance%20-%20Operational%20Metrics.png)
![Store Performance](Screenshots/06c%20Store%20Perfomance%20-%20Store%20Segment.png)

## Inventory Overview

The Inventory Overview page provides a comprehensive view of inventory availability, movement efficiency, supplier dependency, and inventory risk by combining stock status, movement metrics, and valuation insights into a single, interactive analysis.

### Business Objective
Enable stakeholders to monitor inventory health, identify overstock and slow-moving items, optimize replenishment decisions, and reduce inventory holding and operational risks.

### Key Inventory Overview
- Product stock on hand and total inventory valuation
- Potential sales value from current inventory
- Product reorder level and stock-out visibility
- Identification of slow-moving products
- Inventory carrying cost to assess capital utilization

### Inventory Health & Status
- Product-level inventory status classified as:
  - Over Stock
  - Below Reorder Level
  - Out of Stock
- Highlights supply–demand imbalance across products
- Supports proactive replenishment and stock reduction decisions

### Inventory Movement & Efficiency
- Inventory efficiency evaluated using:
  - Inventory Turnover Ratio (ITR)
  - Days Inventory Outstanding (DIO)
  - Stock Coverage (Days)
- Products classified into High, Medium, and Low movement categories
- Helps assess how effectively inventory is converted into sales

### Supplier Insight
- Suppliers ranked dynamically based on stock contribution
- Top and bottom suppliers highlighted to identify:
  - Supplier concentration risk
  - Dependency on high-volume suppliers
- Supplier-level analysis includes stock count, lead time, and supply frequency

### Risk & Valuation Analysis
- Inventory ageing classified into:
  - Fresh
  - Medium
  - Old
- Risk categorization identifies:
  - High-risk slow-moving or aged inventory
  - Medium-risk inventory requiring monitoring
  - Low-risk healthy inventory
- Product-level risk table supports detailed inspection and corrective action

### Interactivity & Navigation
- Bookmark-driven navigation allows switching between:
  - Supplier Insight
  - Risk & Valuation views
- Slicers enable filtering by Category and Subcategory
- All visuals respond dynamically while maintaining analytical consistency
- Informational tooltips explain inventory metrics and movement logic

### Preview
![Inventory](Screenshots/07a%20Inventory%20Overview%20-%20Supplier%20Insight.png)
![Inventory](Screenshots/07b%20Inventory%20Overview%20-%20Risk%20&%20Valuvation.png)

## Return & Refund Analysis

The Return & Refund Analysis page focuses on understanding the financial and operational impact of product returns by analyzing return behavior across products, customers, and stores.

This page helps identify key return drivers, quantify revenue and profit leakage due to returns, and highlight high-risk entities contributing disproportionately to return volume and value.

### Business Objective
Enable stakeholders to reduce return-related losses by identifying root causes, high-return products, customers, and stores, and by supporting corrective actions in operations, quality control, and customer management.

### Key Return Performance Overview
- Total number of returns and returned quantity
- Return Rate (%) based on transactions
- Total refund amount issued
- Net sales after returns to assess revenue impact
- High-level view of return intensity and financial exposure

### Return Financial Impact
- Return Loss % highlights the proportion of sales value lost due to returns
- Average Return Value identifies high-value refund risks
- Profit Lost Due to Returns quantifies margin erosion
- Provides a clear view of how returns directly affect business profitability

### Return Reason Analysis
- Returns categorized by key reasons such as:
  - Late Delivery
  - Wrong Item
  - Damaged Product
  - Customer Dissatisfaction
- Contribution analysis shows which reasons drive the highest return volume
- Supports root-cause analysis and process improvement initiatives

### Product-Level Return Analysis
- Identifies Top / Bottom products by return quantity using dynamic Top N logic
- Highlights products with:
  - High return rates
  - High return contribution despite lower sales
- Helps prioritize product quality checks, packaging improvements, or delisting decisions

### Customer-Level Return Analysis
- Customers segmented based on return frequency:
  - Low
  - Medium
  - High
  - Extreme return behavior
- Identifies customers with disproportionate return impact
- Supports fraud detection, policy enforcement, and targeted customer communication strategies

### Store-Level Return Analysis
- Stores ranked by return quantity and return contribution
- Highlights operational or logistics issues at specific store locations
- Enables focused investigation into store-level handling, fulfillment, and delivery practices

### Top N & Selection Logic
- Top N analysis dynamically switches between:
  - Top
  - Bottom
  - Top 3 / 5 / 10 entities
- Tie handling ensures consistent and fair ranking results
- If fewer entities exist than the selected Top N, visuals automatically adjust

### Interactivity & Navigation
- Bookmark-driven navigation allows switching between:
  - Product Level
  - Customer Level
  - Store Level analysis
- Slicers enable filtering by relevant dimensions while preserving analytical intent
- Informational tooltips explain return metrics, loss interpretation, and risk implications

### Technical Highlights
- Measure-driven Top N logic implemented using dynamic ranking measures
- Return rate and contribution calculated contextually to avoid misleading aggregation
- Financial impact measures aligned with sales and profit models
- Designed to balance operational detail with executive-level clarity

### Preview
![Return & Refund](Screenshots/08a%20Return%20&%20Refund%20Analysis%20-%20Product%20Level.png)
![Return & Refund](Screenshots/08b%20Return%20&%20Refund%20Analysis%20-%20Customer%20Level.png)
![Return & Refund](Screenshots/08c%20Return%20&%20Refund%20Analysis%20-%20Store%20Level.png)

## Shipping Overview

The Shipping Overview page provides a detailed view of logistics performance by combining shipment volume, delivery efficiency, cost behavior, geographic performance, and shipping risk into a single, interactive analysis.

### Business Objective
Enable stakeholders to evaluate shipping efficiency, identify cost leakages, monitor delivery reliability, and reduce operational risks associated with logistics and fulfillment.

### Key Shipping Overview
- Total shipment volume and overall shipping cost
- Average shipping cost per shipment
- On-time delivery % and late delivery %
- Net visibility into delivery reliability and logistics performance

### Delivery Time Metrics
- Tracks key delivery performance indicators:
  - Average delivery days
  - Fastest and slowest delivery days
  - SLA delay
  - SLA achievement %
- Helps measure customer experience and service-level compliance
- Identifies variability and consistency in delivery timelines

### Shipping Risk & Exceptions
- Highlights operational risk indicators including:
  - Delayed shipments
  - High-risk orders
  - Failure count
  - Damaged shipments
  - Return-related shipping issues
- Supports early identification of logistics bottlenecks and service failures

### Shipping Method Analysis
- Shipment and shipping cost distribution by method:
  - Air
  - Road
  - Sea
- Compares:
  - Volume contribution by method
  - Cost impact by method
  - On-time delivery performance
- Identifies the most reliable and most delay-prone shipping methods

### Geographic Performance Analysis
- Regional comparison of:
  - On-time delivery %
  - Average delivery days
  - Shipping cost
- Highlights:
  - Best-performing regions in delivery efficiency
  - Regions facing higher cost or delay pressure
- Supports logistics optimization and regional planning decisions

### Profitability & Cost Efficiency
- Shipping cost % of sales to assess logistics burden on revenue
- Shipping cost per product to evaluate unit-level efficiency
- High-cost shipping orders highlighted to identify cost outliers
- Excess shipping loss by method helps pinpoint inefficiencies driving margin erosion

### Interactivity & Navigation
- Bookmark-driven navigation allows switching between:
  - Method Level
  - Geographic Level
  - Profitability Level views
- Slicers enable filtering by Year, Month, Region, and Shipping Method
- All visuals respond dynamically while preserving analytical intent
- Insight cards and informational tooltips guide interpretation of shipping metrics and risks

### Preview
![Shipping Overview](Screenshots/09a%20Shipping%20Overview%20-%20Method%20Level.png)
![Shipping Overview](Screenshots/09b%20Shipping%20Overview%20-%20Geographic%20Level.png)
![Shipping Overview](Screenshots/09c%20Shipping%20Overview%20-%20Profitablity%20Level.png)

## Manager Insight Overview

The Manager Insight Overview page delivers an executive-ready narrative summary of business performance by translating analytical outcomes into concise, decision-oriented insights across sales, products, customers, and stores.

This page is designed as a **management briefing layer**, focusing on interpretation rather than exploration.

### Business Objective
Provide leadership with a clear understanding of what happened, why it happened, and what to expect next—using a consistent, latest-month snapshot without requiring manual filtering.

### Time Context & Scope
- All insights are based on the **latest available month**
- No slicers are exposed on this page
- Ensures a stable, comparable executive view without ambiguity

### Sales Summary Insight
- Summarizes overall sales momentum versus the previous period
- Assesses profitability health and execution efficiency
- Compares current performance against last year’s baseline
- Highlights whether performance is improving, stable, or under pressure

### Product Summary Insight
- Identifies the leading and declining products for the month
- Highlights category-level contribution and momentum
- Surfaces inventory-related signals such as overstock conditions
- Connects product performance with returns and quality concerns

### Customer Summary Insight
- Evaluates repeat customer engagement and new customer inflow
- Identifies retention and churn risk signals
- Highlights customer value concentration and profitability balance
- Connects customer dissatisfaction with returns and service experience

### Store Summary Insight
- Assesses overall store performance consistency
- Identifies store-level risk exposure and stability
- Evaluates contribution and profitability health across stores
- Highlights operational and fulfillment challenges impacting stores

### Forward-Looking Perspective
- Provides a directional outlook based on recent performance patterns
- Highlights near-term risks and limited upside scenarios
- Supports leadership discussions and action prioritization

### Interactivity & Navigation
- **Bookmark-driven navigation** used to switch between:
  - Sales Summary
  - Product Summary
  - Customer Summary
  - Store Summary
- Toggle-based navigation ensures:
  - Clean executive layout
  - Zero filter dependency
  - Consistent storytelling experience
- Designed purely for **decision consumption**, not data exploration

### Preview
![Manager Insight](Screenshots/10a%20Manager%20Insight%20Overview%20-%20Sales%20Summary.png)
![Manager Insight](Screenshots/10b%20Manager%20Insight%20Overview%20-%20Product%20Summary.png)
![Manager Insight](Screenshots/10c%20Manager%20Insight%20Overview%20-%20Customer%20Summary.png)
![Manager Insight](Screenshots/10d%20Manager%20Insight%20Overview%20-%20Store%20Summary.png)
