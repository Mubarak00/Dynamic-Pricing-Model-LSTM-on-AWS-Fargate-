# Dynamic Pricing Model (LSTM on AWS Fargate)

## Project Summary
Developed and deployed a real-time dynamic pricing engine using LSTM to adjust prices based on demand trends, historical patterns, and product-level elasticity.

## Problem Statement
Static pricing models were leaving revenue on the table in fast-moving sales environments. The business needed a dynamic, data-driven pricing engine to optimize margins without losing competitiveness.

## Tools & Technologies Used
- **Language & Frameworks**: Python, Pandas, Flask  
- **Machine Learning**: LSTM (Keras)  
- **Infrastructure**: AWS Fargate, Docker, CloudWatch  
- **MLOps**: CI/CD, Scheduled retraining, Container orchestration  
- **Data Source**: Product sales history, inventory levels, competitor pricing (via API)

## Modeling Approach
- Created a time series dataset of daily sales volume per SKU
- Incorporated features like holiday flags, promotions, and competitor prices
- Trained LSTM to forecast optimal price range per SKU based on expected demand and margin targets
- Conducted sensitivity analysis on pricing elasticity

## System Architecture
```
ETL (sales + pricing API) ─▶ Feature Engineering ─▶ LSTM Model ─▶ Flask API ─▶ Docker ─▶ AWS Fargate ─▶ Pricing Decision Engine
```

## API Endpoint (Example)
```
POST /get_price
{
  "product_id": "SKU12345",
  "current_stock": 150,
  "day_of_week": "Friday",
  "comp_price": 21.5,
  "is_promo": true
}
```
**Response**
```json
{
  "recommended_price": 23.75,
  "confidence": 0.87
}
```

## Deployment Details
- Dockerized the pricing engine and deployed it via AWS Fargate
- Set up autoscaling for burst traffic
- Scheduled nightly model retraining and CI/CD via GitHub Actions

## Results & Business Impact
- **8% increase in profit margins** due to optimized pricing recommendations  
- Improved stock rotation and reduced over-discounting  
- Enabled product teams to test different pricing strategies via API access

## Monitoring & Maintenance
- Integrated AWS CloudWatch for usage and error tracking
- Used SHAP to explain price suggestions to business analysts
- Set model decay alerts and confidence thresholds for retraining

## Challenges & Learnings
- Managing cold starts for new SKUs was mitigated with rule-based fallback
- LSTM tuning for volatility was critical — required walk-forward validation
- Business trust improved with transparent confidence scores and interpretability

## Team Collaboration
- Collaborated with product managers and marketing analysts to define pricing rules
- Deployed the API in coordination with DevOps for staging and production rollout

## Code Availability
Due to NDA constraints, source code and data are not publicly shareable.
