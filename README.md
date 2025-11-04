
#Sephora Skincare Analytics Dashboard  
[![Excel Project](https://img.shields.io/badge/View%20Excel%20Model-download-blue?style=flat-square)](data/Muhamamad_Sephora_WORKING.xlsx)

> Analysis of Sephora skincare data: exploring product pricing, sentiment, and brand performance across 1.1M+ records.  
> Built entirely in Excel.

> Dataset: Kaggle (Sephora Product + Reviews Dataset)
> License: MIT License
> Author: Curtrianna Muhammad

---

## Overview

**Objective:**  
Clean and analyze Sephora’s skincare dataset to uncover pricing, popularity, and quality trends across brands and categories.

**Tools & Techniques:**  
- Excel **Power Query** for data cleaning and transformation  
- **Power Pivot** for relational data modeling  
- **DAX** for KPIs, ratios, and segmentation  
- Interactive dashboards for **Product Segmentation**, **Consumer Behavior**, and **Profit & Pricing Trends**

**Dataset size:** 1,115,905 rows


---

##  Key Insights
* Revenue performance trails target by ~59%, largely due to limited discount depth in high-value categories.
* Skincare and Fragrance dominate sales, balancing premium and accessible items.
* Customer sentiment remains strong (4.2 avg.), especially among Men’s and Hair products.
* Online-Only and Exclusive products drive brand differentiation and engagement.
* Mini/Travel sizes and midrange SKUs show highest versatility and accessibility.

---

## Column Dictionary 
The tables were imported from the original Kaggle dataset and fully cleaned in Power Query.
Columns were renamed, reformatted, and standardized for relational joins with Products and Calendar.

### Products

| **Column Name**        | **Type**           | **Example Value**                                                         | **Description**                                                             | **Analytical / Dashboard Use**                            |
| ---------------------- | ------------------ | ------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------- |
| **ProductID**          | Text               | `P473671`                                                                 | Unique product identifier from Sephora.                                     | Primary key for joining with `Reviews` table.             |
| **ProductName**        | Text               | `Fragrance Discovery Set`                                                 | Full descriptive product name.                                              | Used as label across visuals and filters.                 |
| **BrandID**            | Whole Number       | `6342`                                                                    | Brand’s unique numeric ID from Sephora.                                     | Links to brand-level aggregations.                        |
| **BrandName**          | Text               | `19-69`                                                                   | Full brand name.                                                            | Enables brand segmentation and filtering.                 |
| **FirstCategory**      | Text               | `Fragrance`                                                               | Top-level product category.                                                 | Used for high-level KPI grouping.                         |
| **SecondCategory**     | Text               | `Women`                                                                   | Secondary classification (gender or product type group).                    | Enables segmentation by audience type.                    |
| **ThirdCategory**      | Text               | `Perfume`                                                                 | Sub-category or specific product segment.                                   | Used for deeper market segmentation.                      |
| **ProductSize**        | Text               | `3.4 oz / 100 mL`                                                         | Reported size of product.                                                   | Used in volume conversion and pricing normalization.      |
| **ProductType**        | Text               | `Size + Concentration + Formulation`                                      | Categorical tag describing data grouping method.                            | Used for consistency in unit standardization.             |
| **ProductValue**       | Text               | `3.4 oz / 100 mL Eau de Parfum Spray`                                     | Combined string of size and formulation.                                    | Used for descriptive labeling and deduplication.          |
| **ProductDescription** | Text               | `[Capri Eau de Parfum]`                                                   | Marketing description text (trimmed from original dataset).                 | Supports qualitative product review mapping.              |
| **Ingredients**        | Text/List          | `['Alcohol Denat.', 'Parfum (Fragrance)', 'Ethylhexyl Methoxycinnamate']` | Cleaned list of ingredients.                                                | Enables filtering by chemical components or formula type. |
| **RetailPrice**        | Currency           | `195.00`                                                                  | Standard retail price in USD.                                               | Used as baseline for price comparison.                    |
| **SalePrice**          | Currency           | `82.00`                                                                   | Current sale or promotional price (if available).                           | Used to calculate discount metrics.                       |
| **DiscountAmount**     | Currency           | `113.00`                                                                  | Retail – Sale Price.                                                        | Used for discount analytics and KPI visualizations.       |
| **PriceTier**          | Text               | `Premium`                                                                 | Categorization of product based on price thresholds.                        | Enables comparisons across budget/mid/premium segments.   |
| **MarketValue**        | Currency           | `200.00`                                                                  | Estimated benchmark value of similar items in market.                       | Used for pricing gap and value perception measures.       |
| **PerceivedValueGap**  | Currency           | `-5.00`                                                                   | Difference between Retail Price and Market Value.                           | Used to assess overpricing or underpricing trends.        |
| **VariantCount**       | Whole Number       | `2`                                                                       | Number of product variations (e.g., sizes or colors).                       | Indicates SKU diversity and product flexibility.          |
| **VariantMaxPrice**    | Currency           | `85.00`                                                                   | Highest price among product variations.                                     | Used to calculate price range.                            |
| **VariantMinPrice**    | Currency           | `30.00`                                                                   | Lowest price among product variations.                                      | Used to calculate price range.                            |
| **PriceRange**         | Currency           | `55.00`                                                                   | Difference between Variant Max – Min Price.                                 | Reflects breadth of product pricing.                      |
| **FeatureTags**        | Text/List          | `['Unisex / Genderless Scent', 'Layerable Scent', 'Warm & Spicy']`        | Marketing and attribute tags.                                               | Enables keyword clustering and consumer feature analysis. |
| **LimitedEdition?**    | Boolean            | `FALSE`                                                                   | Indicates if product is limited edition.                                    | Used to track exclusivity.                                |
| **New?**               | Boolean            | `FALSE`                                                                   | Indicates if product is recently released.                                  | Used for product lifecycle tracking.                      |
| **SephoraExclusive?**  | Boolean            | `FALSE`                                                                   | Marks whether the item is exclusive to Sephora.                             | Used to segment Sephora-only listings.                    |
| **OnlineOnly?**        | Boolean            | `TRUE`                                                                    | True if product is available only online.                                   | Used for channel performance comparison.                  |
| **OutOfStock?**        | Boolean            | `FALSE`                                                                   | Indicates if product is currently unavailable.                              | Used for stock availability insights.                     |
| **LovesCount**         | Whole Number       | `6 320`                                                                   | Number of users who “hearted” the product.                                  | Used as engagement metric.                                |
| **ReviewCount**        | Whole Number       | `11`                                                                      | Total number of reviews associated with the product.                        | Used for review volume analysis.                          |
| **AvgRating**          | Whole Number (1–5) | `4`                                                                       | Average consumer rating.                                                    | Used to measure customer satisfaction.                    |
| **ProductSizeVolume**  | Decimal            | `4`                                                                       | Converted product size in oz or equivalent.                                 | Used in volume-based price metrics.                       |
| **ProductValueVolume** | Decimal            | `100`                                                                     | Converted volume in mL or equivalent.                                       | Used for per-unit value comparisons.                      |
| **FinalVolumeML**      | Decimal            | `100`                                                                     | Standardized volume (in mL) after conversion.                               | Ensures consistent unit analysis.                         |
| **FinalSizeCategory**  | Text               | `Large`                                                                   | Grouped label for size classification (`Travel/Mini`, `Standard`, `Large`). | Used for dashboard filtering and KPI segmentation.        |


### Reviews

| **Column Name**    | **Type**           | **Example Value**                                    | **Description**                                                     | **Analytical / Dashboard Use**                                   |
| ------------------ | ------------------ | ---------------------------------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **ProductID**      | Text               | `P420652`                                            | Unique identifier linking each review to its corresponding product. | Foreign key for joining with `Products` table.                   |
| **ProductName**    | Text               | `Lip Sleeping Mask Intense Hydration with Vitamin C` | Full product name for reference or redundancy checks.               | Label for pivot tables and visuals.                              |
| **BrandName**      | Text               | `LANEIGE`                                            | Name of the brand or manufacturer.                                  | Enables brand-level grouping and KPI summaries.                  |
| **RetailPrice**    | Currency           | `24.00`                                              | Product’s listed retail price at time of review.                    | Used for cross-referencing price segmentation and review trends. |
| **ReviewCount**    | Whole Number       | `28`                                                 | Count of reviews submitted for the product.                         | Used in engagement metrics and ratio calculations.               |
| **AvgRating**      | Whole Number (1–5) | `5`                                                  | Reviewer’s star rating.                                             | Core input for sentiment and satisfaction KPIs.                  |
| **IsRecommended?** | Boolean            | `TRUE`                                               | Indicates if the reviewer recommends the product.                   | Used for calculating % Recommended by brand/category.            |
| **IsHelpful?**     | Boolean            | `TRUE`                                               | Whether the review was marked as helpful by other users.            | Enables % Helpful Reviews and engagement analysis.               |
| **FeedbackCount**  | Whole Number       | `8`                                                  | Total number of feedback responses (positive + negative).           | Quantifies engagement and credibility of reviews.                |
| **NegReviewCount** | Whole Number       | `2`                                                  | Number of users who rated the review as “Not Helpful.”              | Used to calculate helpfulness ratio and reviewer bias.           |
| **PosReviewCount** | Whole Number       | `6`                                                  | Number of users who rated the review as “Helpful.”                  | Used for helpfulness and trust scoring.                          |
| **WriterID**       | Text               | `42802569154`                                        | Unique anonymous ID for each reviewer.                              | Allows tracking repeat reviewers and unique writer analysis.     |
| **SubmissionTime** | Date (MM/DD/YYYY)  | `3/19/2023`                                          | Date the review was posted.                                         | Enables time-series analysis via `Calendar` relationship.        |
| **Title**          | Text               | `Great!`                                             | Short summary headline of the review.                               | Used for qualitative keyword extraction and quick summaries.     |
| **Text**           | Text (Long)        | `The scent isn’t my favourite but it works great!`   | Full written text of the review.                                    | Core for NLP or qualitative sentiment analysis.                  |
| **SkinType**       | Text               | `Combination`                                        | Self-reported skin type of reviewer.                                | Used for consumer profile segmentation.                          |
| **SkinTone**       | Text               | `LightMedium`                                        | Reviewer’s skin tone.                                               | Helps assess product inclusivity and user diversity.             |
| **HairColor**      | Text               | `Brown`                                              | Reviewer’s reported hair color.                                     | Secondary demographic descriptor for segmentation.               |
| **EyeColor**       | Text               | `Blue`                                               | Reviewer’s reported eye color.                                      | Optional demographic attribute for audience profiling.           |



---

## Power Query Data Preparation Summary
The Sephora dataset was transformed through a structured Power Query workflow to ensure consistency, readability, and relational integrity across all linked tables.
Below summarizes the major cleaning, transformation, and normalization tasks applied throughout the model.

### Products Table Transformations
* Renamed columns to consistent PascalCase with no spaces for model clarity.
* Added derived fields: PriceTier, DiscountAmount, PerceivedValueGap, and FinalSizeCategory.
* Standardized product volume by parsing and converting ounces → milliliters using numeric token extraction (GetNumberBeforeToken, ParseVolumeML).
* Capitalized all brand, category, and descriptive names using Text.Proper.
* Filtered duplicates, nulls, and non-relevant records (e.g., “null” or empty price entries).
* Reordered columns by logical grouping: identifiers → attributes → pricing → flags → derived measures.
* Added logical flags (LimitedEdition?, OnlineOnly?, SephoraExclusive?, OutOfStock?) as Boolean (TRUE/FALSE).
* Mapped and normalized size tiers through lookup from MapSizing query for coherent product segmentation.

### Reviews Table Transformations
* Renamed columns from snake_case to readable PascalCase.
* Capitalized categorical text fields (SkinType, SkinTone, HairColor, EyeColor) using Text.Proper.
* Converted Boolean flags (IsRecommended?, IsHelpful?) from numeric (1/0) to logical TRUE/FALSE.
* Removed duplicates and rows with missing or invalid ProductID links.
* Replaced nulls with blanks or zeros based on data type.
* Trimmed and reordered columns for alignment with the Products table (ensuring relational consistency).
* Standardized date fields (SubmissionTime) and casted to Date type for calendar relationships.

### Demographics Normalization 

#### RawDemographics
* Unpivoted demographic columns (SkinType, SkinTone, HairColor, EyeColor) into Attribute–Value format.
* Trimmed, capitalized, and de-duplicated values using Text.Proper.
* Removed blanks and inconsistent entries (null, empty text).
* Sorted by Attribute and Value alphabetically.

#### NewDemographics
* Filtered out ambiguous entries such as "Notsurest".
* Maintained clean, usable demographic categories for model mapping.

#### MapDemographics
* Created mapping structure with Attribute, Value, NewValue, and Status columns.
* Assigned "Kept" or "Removed" flags for control tracking of standardized demographic values.
* Sorted by attribute for easy join reference.

### Product Size Normalization 

#### RawSizing
* Extracted distinct combinations of ProductSize and ProductValue.
* Calculated equivalent FinalVolumeML through unit conversion.
* Derived FinalSizeCategory labels: Travel/Mini, Standard, Large, XL.

#### MapSizing
* Standardized attribute naming and created mapping table with
* Attribute (e.g., ProductSize)
* Value (FinalVolumeML)
* NewValue (size category label).
* Used as a lookup table for consistent size-tier alignment in the main Products query.

### Text Analysis Query
* Isolated Title and Text fields from Reviews for NLP preprocessing.
* Added custom Boolean field HasValueMention using:
  > = Table.AddColumn(Source, "HasValueMention", each Text.Contains([Text], "value"), type logical)
* Casted logical columns and prepared data for downstream sentiment and keyword extraction.

### Supporting Queries
* Calendar: Generated clean Date table with year, month, and quarter breakdowns for time intelligence.
* Helper Queries: Parameterized transformations to automate folder imports and apply consistent schema.

### Final Integration Notes
* Ensured referential integrity between Products, Reviews, and Calendar via consistent ProductID and SubmissionTime relationships.
* Normalized all text capitalization and removed inconsistent casing from category, tone, and color attributes.
* Verified all numeric columns are typed as Decimal or Whole Number, avoiding “Any” data types.
* Organized queries into logical folders:
* Main Tables: Products, Reviews, Calendar
* Lookup & Mapping: RawDemographics, MapDemographics, RawSizing, MapSizing
* Text Processing: TextAnalysis

  
---


##  Key DAX Measures

```DAX
// Revenue KPIs
Revenue := SUM(Products[SalePrice])
Revenue Goal := 300000
Revenue Goal Attainment % := DIVIDE([Revenue], [Revenue Goal])
Revenue Gap ($) := [Revenue] - [Revenue Goal]

// Product Composition
% Premium Products := 
    DIVIDE(CALCULATE([Total Products], Products[Price Tier] = "Premium"), [Total Products])

Revenue Contribution by Tier % :=
VAR _total = CALCULATE([Revenue], ALL(Products[Price Tier]))
RETURN DIVIDE([Revenue], _total)

// Sentiment
% Products Mostly Positive :=
VAR T =
  ADDCOLUMNS(
    VALUES(Products[ProductID]),
    "Pos", CALCULATE(SUM('Reviews 1'[PosReviewCount])),
    "Neg", CALCULATE(SUM('Reviews 1'[NegReviewCount]))
  )
VAR T_Valid = FILTER(T, [Pos] + [Neg] > 0)
RETURN DIVIDE(COUNTROWS(FILTER(T_Valid, [Pos] > [Neg])), COUNTROWS(T_Valid))

