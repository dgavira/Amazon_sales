Kaggle: https://www.kaggle.com/datasets/rohiteng/amazon-sales-dataset/data

# Amazon_sales
This dataset of 100,000 Amazon-style sales simulates a real e-commerce business. It is ideal for practicing Data Science from scratch by solving business problems: measuring if discounts are profitable, classifying customers by purchases, finding logistical flaws, and creating basic models to recommend products or predict future sales.
# Amazon Sales Dataset - E-commerce Behavior Analysis

## About the Dataset
This dataset contains 100,000 synthetic Amazon-style sales transactions, designed to closely simulate real e-commerce behavior. With 20 clear and well-structured columns, it gathers detailed information about customers, products, pricing, payments, logistics, and order outcomes.

Although the data is artificially generated, it reflects realistic patterns such as:
- Dynamic product pricing
- Variable discounts and taxes
- Multiple product categories and brands
- Seasonal order trends
- Diversity of payment methods
- Realistic customer names and locations
- Order statuses such as Delivered, Canceled, Shipped, Returned

This makes the dataset highly suitable for analysis, machine learning, data visualization, dashboards, and business case studies.

## Column Summary

### Order Details
- **Order ID**
- **Order Date**
- **Order Status**
- **Seller ID**

### Customer Information
- **Customer ID**
- **Customer Name**
- **City, State, Country**

### Product Information
- **Product ID**
- **Product Name**
- **Category**
- **Brand**
- **Quantity**

### Pricing and Revenue Metrics
- **Unit Price**
- **Discount**
- **Tax**
- **Shipping Cost**
- **Total Amount**

### Payment Details
- **Payment Method**

---

## 5 Business Questions Addressed

**1. The real impact of "offers": Do discounts generate more money or just more volume?**
Anyone can see how many discounts have been given. The hard part is cross-referencing the `Discount`, `Quantity`, and `TotalAmount` columns. The question is: When Amazon applies a discount, do people buy so much extra quantity that it makes up for the price drop, or is the company losing money per sale? This is called studying price elasticity.

**2. Customer Segmentation (RFM Model)**
Not all customers are the same. Instead of just calculating a simple sales average, we want to classify buyers (using their `CustomerID`) into strategic groups by cross-referencing three things:
- **Recency**: How long ago was their last purchase? (using `OrderDate`)
- **Frequency**: How many orders have they placed? (counting their `OrderID`)
- **Monetary Value**: How much total money have they spent? (summing `TotalAmount`)

The goal is to identify who the "golden customers" are that need to be taken care of, and who are the ones that bought once and never returned.

**3. Detecting logistical bottlenecks**
You have an `OrderStatus` column (whether it has been delivered or not) alongside geographic data (`City`, `State`) and the sellers (`SellerID`). A good analysis would look for hidden failure patterns: Is there a particular state where orders fail more often? Or is it the fault of a specific seller who always has shipping problems regardless of where they ship?

**4. Predictive seasonality by categories**
We don't settle for just knowing which month had the most sales. We want to cross-reference the order date (`OrderDate`) with the product type (`Category`). Maybe the "Books" category sells the same all year round, but "Home & Kitchen" has hidden peaks. The goal here is to find those repeating patterns so we can tell the company: "In the third week of November, prepare the warehouse for products in this specific category."

**5. The trap of hidden costs and real profitability**
Sometimes a product seems like a bestseller because many units are ordered (`Quantity`), but if we cross-reference the unit price (`UnitPrice`) and subtract taxes (`Tax`) and shipping costs (`ShippingCost`), the reality might be different. The idea is to create a new mathematical metric with these columns to discover which brands (`Brand`) or products actually leave a profit margin, and which ones create a lot of work for little money.

---

## Predictive Models & Business Applications

### 1. Discount Optimization Model (Regression)
- **The goal:** Stop giving discounts blindly. Instead of a boss deciding to offer a 15% discount based on intuition, we will feed our entire history to an algorithm (like Random Forest or Linear Regression).
- **The prediction:** The model will learn the relationship between the `Discount` column and the `Quantity` column for each type of product. It will be able to tell us: *"For the 'Books' category, if you raise the discount from 10% to 15%, I predict you will sell 400 more units, but you will lose profit margin. The optimal discount to maximize real money is 12%."*

### 2. Customer Churn Prediction (Classification)
- **The goal:** Save customers before they leave for the competition. Once we do the customer segmentation (our question 2), we will know who our best buyers are.
- **The prediction:** We will train a classification model (like Logistic Regression) that studies the patterns of customers who stopped buying. The algorithm will monitor current customers and give us an alert: *"Customer CUST001504 shows the same inactivity pattern as lost customers; they have an 85% probability of not buying again."*
- **The business improvement:** We will send an automatic email with an aggressive discount to this specific group (and not everyone) to win them back.

### 3. Product Recommendation System (Cross-Selling)
- **The goal:** Increase the average ticket of each order. We only have 50 products in the catalog, which is ideal for doing what is called a "Market Basket Analysis" (using association rules like the Apriori algorithm).
- **The prediction:** The system will learn what things are bought together by analyzing all `OrderID`s. It will discover hidden rules like: *"70% of people who buy a 'Microphone' (P00040) also buy a 'Full HD Webcam' in the same order."*
- **The business improvement:** We can propose that the company create "Indivisible bundles" with a slight joint discount, or configure the website so that when someone puts a microphone in their cart, an automatic ad for the webcam pops up.

### 4. Future Demand Prediction (Time Series)
- **The goal:** Not run out of stock in the warehouse or have products gathering dust.
- **The prediction:** We will use time models (like ARIMA or Prophet) that will analyze the `OrderDate` and `Quantity` columns. The model will detect upward and downward trends throughout the year and tell us: *"For the second week of November, expect to sell 4,500 units of the 'Home & Kitchen' category."*
- **The business improvement:** It allows the logistics department to buy from suppliers in advance, negotiating better prices and reducing last-minute shipping costs.
