# 📚 Data Dictionary - E-Commerce Customer Journey & Conversion Analysis
## Complete Field Reference Guide

---

## Dataset Overview

**Focus**: E-Commerce customer behavior and conversion funnel  
**Total Records**: 100,000+ customer interactions  
**Key Dimensions**: Customer journey stages, products, channels, orders  
**Time Period**: 12+ months historical data  
**Grain**: One row per customer session / order event

---

## CUSTOMER JOURNEY FACT TABLE

### Session/Visit Events

#### **Session_ID**
- **Type**: Text (Unique)
- **Definition**: Unique identifier per website session
- **Pattern**: AUTO-GENERATED
- **Cardinality**: 100,000+ unique sessions
- **Usage**: Track individual customer visits
- **Business Rule**: Non-null, unique per session

---

#### **Customer_ID**
- **Type**: Integer
- **Definition**: Unique customer identifier
- **Range**: 1 - 45,000 unique customers
- **Relationship**: Links to customer dimension
- **Repeat Visits**: 65% customers have 2+ sessions
- **Purpose**: Customer segmentation, LTV tracking
- **Data Quality**: Some anonymous/guest customers

---

#### **Session_Date**
- **Type**: Date
- **Range**: Last 12 months
- **Format**: YYYY-MM-DD
- **Pattern**: Business operational dates (includes weekends)
- **Seasonality**: Peak during holiday months (Nov-Dec)
- **Usage**: Time-based analysis, trend identification

---

#### **Session_Time**
- **Type**: DateTime
- **Definition**: Exact time of session start
- **Granularity**: Hour and minute level
- **Peak Hours**: 
  - 10AM-12PM: 22% of traffic
  - 6PM-8PM: 28% of traffic (Peak)
  - 1AM-5AM: 5% of traffic (Low)
- **Purpose**: Traffic pattern analysis, performance scheduling

---

#### **Device_Type**
- **Type**: Category
- **Values**:
  - Desktop: 45% of sessions
  - Mobile: 50% of sessions
  - Tablet: 5% of sessions
- **Conversion Impact**:
  - Desktop: 8.2% conversion
  - Mobile: 5.1% conversion
  - Tablet: 6.8% conversion
- **Mobile Issue**: Lower conversion due to checkout friction
- **Business Rule**: Must be standardized value

---

#### **Traffic_Source**
- **Type**: Category
- **Values**:
  - Direct: 25% (bookmark/remembers)
  - Organic_Search: 35% (Google, Bing)
  - Paid_Ads: 25% (Google Ads, Facebook)
  - Social_Media: 10% (Facebook, Instagram, TikTok)
  - Referral: 5% (Other websites)
- **Conversion by Source**:
  - Direct: 4.2% (highest quality)
  - Organic: 3.8% (high intent)
  - Paid: 2.1% (broad audience)
  - Social: 1.5% (brand awareness)
  - Referral: 3.2% (partnership)
- **Cost by Source**:
  - Direct: $0 (no cost)
  - Organic: $0 (low cost)
  - Paid: $0.80 per click
  - Social: $0.45 per click
  - Referral: $0 (partner)

---

### FUNNEL STAGE TRACKING

#### **Stage_Name**
- **Type**: Category (Ordered)
- **Values** (in sequence):
  1. **Awareness**: Lands on website
  2. **Interest**: Browses product listing
  3. **Consideration**: Views specific products
  4. **Add_to_Cart**: Adds item to shopping cart
  5. **Checkout_Start**: Begins checkout process
  6. **Purchase**: Completes transaction
  7. **Post_Purchase**: Return/review/repeat

- **Progression**: Sequential, no skipping
- **Duration**: Average 8 minutes per stage
- **Dropout**: 50% drop-off by Checkout

---

#### **Pages_Viewed**
- **Type**: Integer
- **Range**: 1 - 50 pages per session
- **Mean**: 3.2 pages
- **Distribution**:
  - 1-2 pages: 35% (quick exit)
  - 3-5 pages: 40% (moderate engagement)
  - 6-10 pages: 20% (high engagement)
  - 10+ pages: 5% (power users)
- **Correlation**: More pages = higher conversion
  - 1-2 pages: 1% conversion
  - 3-5 pages: 5% conversion
  - 6-10 pages: 12% conversion
  - 10+ pages: 20% conversion
- **Insight**: Engagement strongly predicts purchase

---

#### **Time_on_Site (Minutes)**
- **Type**: Integer/Decimal
- **Range**: 0.5 - 120 minutes
- **Mean**: 6.2 minutes
- **By Conversion**:
  - Bounce (<0.5 min): 90% don't convert
  - Brief (0.5-2 min): 2% convert
  - Normal (2-8 min): 6% convert
  - Extended (8+ min): 15% convert
- **Mobile Effect**: Mobile users spend 30% less time
- **Quality Metric**: Time + pages = engagement score

---

### CONVERSION EVENT DETAILS

#### **Added_to_Cart**
- **Type**: Boolean
- **Values**: Yes / No
- **Distribution**: 21.5% of sessions add to cart
- **Critical Metric**: First major funnel stage
- **Predictive**: Cart addition 80% predictive of purchase
- **Cart Value**: 
  - Average items: 1.8 items
  - Average cart value: $89
  - Range: $10 - $500

---

#### **Checkout_Started**
- **Type**: Boolean
- **Values**: Yes / No
- **Distribution**: 40% of cart sessions start checkout (60% abandon!)
- **Critical Issue**: MAJOR DROP-OFF POINT
- **Problem Areas**:
  - Mobile checkout: Only 30% complete
  - Payment friction: Limited options
  - Shipping costs: Surprise at checkout
  - Account requirements: Forced login
  - Trust signals: Missing security badges

---

#### **Purchase_Completed**
- **Type**: Boolean
- **Values**: Yes / No
- **Distribution**: 7.3% overall conversion rate
- **By Segment**:
  - First-time: 2.1% conversion
  - Returning: 28% conversion
  - High-engagement: 22% conversion
  - Low-engagement: 1% conversion

---

#### **Order_Value**
- **Type**: Currency
- **Range**: $10 - $5,000
- **Mean**: $99.80
- **Median**: $75.00
- **By Segment**:
  - New customers: $65 avg
  - Returning: $145 avg
  - High-tier: $250+ avg
- **Distribution**: Right-skewed (few high-value orders)

---

#### **Items_Purchased**
- **Type**: Integer
- **Range**: 1 - 20 items per order
- **Mean**: 1.8 items
- **Bundle Opportunity**: 
  - Single items: 60% of orders
  - 2+ items: 40% of orders
  - Bundle buyers: 12% higher LTV
- **Cross-sell Potential**: +$15 per bundle

---

#### **Payment_Method**
- **Type**: Category
- **Values**:
  - Credit Card: 65% (most common)
  - Debit Card: 20%
  - Digital Wallet: 10% (Apple Pay, PayPal)
  - Other: 5%
- **Completion Rate**:
  - Credit Card: 87%
  - Debit: 85%
  - Digital Wallet: 92% (highest!)
  - Other: 60%
- **Insight**: Limited payment options limiting sales

---

#### **Discount_Applied**
- **Type**: Boolean / Currency
- **Values**: Yes/No or discount amount
- **Prevalence**: 35% of orders have discount
- **Impact**:
  - No discount: $110 AOV, 85% completion
  - 10% discount: $98 AOV, 92% completion
  - 20% discount: $85 AOV, 95% completion
- **Trade-off**: Higher conversion vs lower margin

---

### PRODUCT DETAILS

#### **Product_ID**
- **Type**: Integer
- **Definition**: Unique product identifier
- **Cardinality**: 500+ products
- **Relationship**: Links to product dimension
- **Usage**: Product-level performance tracking

---

#### **Product_Category**
- **Type**: Category
- **Values**:
  - Electronics: 35% of sales
  - Clothing: 25% of sales
  - Home & Garden: 20% of sales
  - Sports: 12% of sales
  - Other: 8% of sales
- **Conversion by Category**:
  - Electronics: 8.5% (high intent)
  - Clothing: 6.2%
  - Home & Garden: 5.8%
  - Sports: 7.1%
  - Other: 4.2%

---

#### **Product_Name**
- **Type**: Text
- **Length**: 30-100 characters
- **Format**: Standardized naming
- **Example**: "Samsung 55 inch 4K Smart TV"
- **Quality**: Complete product descriptions

---

#### **Product_Price**
- **Type**: Currency
- **Range**: $5 - $2,000
- **Price Sensitivity**:
  - <$50: 12% conversion
  - $50-$100: 8% conversion (sweet spot)
  - $100-$500: 5% conversion
  - $500+: 2% conversion
- **Perception**: Higher prices need more social proof

---

#### **Product_Stock**
- **Type**: Integer
- **Definition**: Inventory available
- **Impact**: Out of stock loses sales
- **Reorder**: Stock-outs should trigger reorder
- **Visibility**: Show inventory to reduce friction

---

#### **Product_Rating**
- **Type**: Decimal (1.0 - 5.0)
- **Scale**: 1-5 stars
- **Distribution**:
  - 4.5+: 25% of products (bestsellers)
  - 4.0-4.5: 40% of products (good)
  - 3.0-4.0: 25% of products (average)
  - <3.0: 10% of products (poor)
- **Conversion Impact**:
  - 4.5+ stars: 12% conversion
  - 4.0-4.5: 8% conversion
  - 3.0-4.0: 4% conversion
  - <3.0: 1% conversion
- **Trust Signal**: High ratings critical

---

#### **Review_Count**
- **Type**: Integer
- **Range**: 0 - 5,000 reviews
- **Conversion Effect**:
  - 0 reviews: 3% conversion
  - 1-10 reviews: 5% conversion
  - 10-50 reviews: 9% conversion
  - 50+ reviews: 14% conversion
- **Social Proof**: More reviews = higher conversion

---

### CUSTOMER ATTRIBUTES

#### **Customer_Status**
- **Type**: Category
- **Values**:
  - New: 40% of customers (first purchase)
  - Returning: 45% of customers (2-5 purchases)
  - Loyal: 15% of customers (6+ purchases)
- **Conversion by Status**:
  - New: 2.1%
  - Returning: 18%
  - Loyal: 35%
- **LTV by Status**:
  - New: $50
  - Returning: $240
  - Loyal: $650

---

#### **Customer_Age_Group**
- **Type**: Category
- **Values**:
  - 18-25: 20% (low spenders)
  - 26-35: 35% (high spenders)
  - 36-50: 30% (loyal)
  - 50+: 15% (premium)
- **Conversion by Age**:
  - 18-25: 5.2%
  - 26-35: 8.1% (highest)
  - 36-50: 7.8%
  - 50+: 6.5%

---

#### **Customer_Location**
- **Type**: Text (Country / State)
- **Values**: 50+ countries, US states
- **Shipping Complexity**: International slower
- **Tax Impact**: State sales tax affects AOV
- **Regional Performance**: Varies by region

---

#### **Email_Subscriber**
- **Type**: Boolean
- **Values**: Yes / No
- **Distribution**: 65% subscribed
- **Impact**: Subscribers 2x more likely to convert
- **Retention**: Email key to customer retention

---

## AGGREGATE METRICS TABLES

### Funnel Metrics Table

**Row**: Each funnel stage  
**Columns**:
- Stage_Name
- Total_Sessions_Entering
- Sessions_Progressing
- Conversion_Rate
- Drop_Off_Rate

**Example**:
```
Stage: Add_to_Cart
Entering: 21,450 sessions
Progressing: 8,580 (40%)
Conversion: 40%
Drop-off: 60%
```

---

### Product Performance Table

**Row**: Each product  
**Columns**:
- Product_ID
- Product_Name
- Total_Views
- Add_to_Cart_Rate
- Purchase_Count
- Revenue
- Profit_Margin
- Inventory_Status

---

### Channel Performance Table

**Row**: Each traffic source  
**Columns**:
- Channel
- Sessions
- Revenue
- Conversion_Rate
- CPA (Cost Per Acquisition)
- ROAS (Return on Ad Spend)

---

## DATA QUALITY STANDARDS

### Validation Rules

| Field | Rule | Severity |
|-------|------|----------|
| Customer_ID | Non-null | CRITICAL |
| Session_Date | Valid date | CRITICAL |
| Purchase_Completed | Yes/No | CRITICAL |
| Order_Value | > $0 if purchased | HIGH |
| Payment_Method | Valid value | HIGH |
| Pages_Viewed | ≥ 1 | MEDIUM |
| Device_Type | Standardized | MEDIUM |

---

### Data Quality Summary

✅ **Completeness**: 98.5%  
✅ **Accuracy**: 99.2%  
✅ **Consistency**: 97.8%  
✅ **Timeliness**: Updated daily (12 hours latency)

---

## TRANSFORMATION LOGIC

### Binning Examples

**Conversion Likelihood**:
```
High (>10% chance):
  ├─ 6+ pages viewed
  ├─ 8+ minutes on site
  ├─ Returning customer
  └─ Product rating 4.5+

Medium (5-10% chance):
  ├─ 3-5 pages viewed
  ├─ 2-8 minutes on site
  ├─ First-time buyer
  └─ Product rating 3.5-4.5

Low (<5% chance):
  ├─ 1-2 pages viewed
  ├─ <2 minutes on site
  ├─ High bounce rate
  └─ Product rating <3.5
```

---

### Segment Classification

**Customer Value**:
```
High-Value (VIP):
  ├─ LTV > $500
  ├─ Repeat rate > 5 purchases
  ├─ AOV > $150
  └─ Loyalty > 2 years

Mid-Value:
  ├─ LTV $200-500
  ├─ Repeat rate 2-4 purchases
  ├─ AOV $80-150
  └─ Loyalty 6-24 months

Low-Value:
  ├─ LTV < $200
  ├─ Single purchase
  ├─ AOV < $80
  └─ At risk of churn
```

---

## USAGE GUIDELINES

### For Marketing Teams
- Focus on **Traffic_Source** for channel optimization
- Use **Discount_Applied** to test pricing
- Monitor **Conversion_Rate** by source
- Track **Customer_Status** for retention

### For Product Teams
- Analyze **Pages_Viewed** vs conversion
- Monitor **Product_Rating** impact
- Track **Add_to_Cart** rates
- Identify **Cart_Abandonment** reasons

### For E-Commerce Managers
- Review **Order_Value** trends
- Monitor **Checkout_Completion**
- Track **Revenue** by segment
- Plan **Inventory** based on demand

---

## GLOSSARY

**Conversion**: Customer completes purchase  
**Funnel**: Stages from awareness to purchase  
**Drop-off**: Customer exits funnel without converting  
**AOV**: Average Order Value  
**LTV**: Lifetime Value  
**CPA**: Cost Per Acquisition  
**ROAS**: Return on Ad Spend  
**Cart Abandonment**: Add to cart but don't checkout  
**Session**: Single website visit  
**Touchpoint**: Interaction with brand  

---

**Last Updated**: March 2026  
**Data Version**: E-Commerce v1.0  
**Refresh Rate**: Daily
