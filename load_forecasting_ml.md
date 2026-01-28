[Back](https://zenjen-devs.github.io)

# Machine Learning for Grid Ops: Day-Ahead Load Forecasting for NYC Energy Market

><img src="images/extrawide_3x1.jpg?raw=true" title="Source: Shutterstock"/>

[View Repository](https://github.com/zenjen-dev/load_forecasting_ml) <br>

Energy grid operators face a critical daily decision that affects all New Yorkers: which plants should start tomorrow?
When too many are turned on, wasted fuel and startup operations can be costly. Inversely, when too too few are turned on there is increased risk for emergency energy purchases 10x normal prices. Traditional forecasting methods hit 5-7% error rates, forcing operators to hedge with expensive backup units on an as-needed basis. I built an XGBoost model on real NYISO hourly data that achieves 1.7% MAPE with strong peak performance (2.3% on high-load hours), enabling confident unit commitment decisions worth $15-25M annually.

## Model Performance & Results

The model uses real NYISO hourly load data with peak-weighted training (high-demand hours get 3x importance in the loss function) and achieves performance competitive with best-in-class utility systems. This isn't about perfect predictions, it's about confidence intervals that matter for operations. With 1.7% accuracy on a 20 GW system, operators get ±340 MW confidence versus ±1,000 MW with traditional methods. That difference eliminates hedging decisions and unnecessary plant startups.

**Key Metrics:**
- Overall MAPE: 1.70% (industry standard: 5-7%)
- Peak hour MAPE: 2.34% (critical period)
- R²: 0.940 (strong explanatory power)
- Range coverage: 85.5% (captures load variability)
- 7-day forecast capability proven

<p align="center">Forecast Dashboard: Historical validation, future projections, and performance breakdown</p>

<img width="2602" height="560" alt="Screenshot 2026-01-28 at 2 19 32 PM" src="https://github.com/user-attachments/assets/e13b4131-404a-4d5a-8a88-2ee1304c8f9c" />
<img width="1710" height="616" alt="Screenshot 2026-01-28 at 2 19 53 PM" src="https://github.com/user-attachments/assets/17958d28-2632-40c5-803d-5d1b92dfcc23" />

The model maintains strong performance across all hours with particularly good results during peak periods when accurate predictions matter most for capacity planning. Feature importance analysis shows recent lags (1h, 24h) drive 45% of predictions, with rolling averages and temporal patterns accounting for the rest. No signs of overfitting and consistent performance across weekday/weekend patterns.

<img width="2602" height="912" alt="Screenshot 2026-01-28 at 2 23 05 PM" src="https://github.com/user-attachments/assets/c2ee0889-2115-4386-a64c-174c59fb700d" />
<p align="center">Business Applications: Daily peak forecasting and accuracy by load level</p>

## Methodology

**Data:** NYISO public hourly load data covering 480 hours of grid operations. Load range 15,884 - 23,817 MW representing real operational conditions.

**Feature Engineering:** Built 10 features focused on temporal patterns and historical context:
- Temporal: Hour/day/month cyclical encoding (sine/cosine transforms)
- Historical: 1-hour and 24-hour lags
- Rolling stats: 24-hour and 168-hour moving averages
- Peak indicators: Business hours and seasonal peak flags

**Model:** XGBoost regressor (500 trees, depth 8) with peak-weighted training. Top 25% of load hours get 3x importance during training to ensure the model learns critical high-demand patterns. Bias correction applied from validation set, plus range adjustment to ensure predictions span realistic load variability.

**Why XGBoost:** Handles non-linear temporal patterns efficiently, works well with tabular time series, provides interpretable feature importance, and delivers production-ready performance. Considered LSTM but XGBoost proved more reliable and faster to iterate on this scale of data.

## From Accuracy to Operational Impact

Better forecasting translates directly to better decisions. The primary application is day-ahead unit commitment where operators decide which plants to start 24 hours ahead. With 1.7% accuracy versus traditional 5%, you get ±340 MW confidence instead of ±1,000 MW. This eliminates hedging with expensive backup units.

**Operational Value Breakdown:**
- Avoid 15-20 unnecessary plant startups annually: $4-6M savings (each startup is $300K)
- Reduce over-running of peaking units: $8-12M savings (fuel waste)
- Prevent emergency energy purchases: $3-5M savings (10 events/year avoided at 10x cost)
- **Total: $15-25M annual value** just from optimized unit commitment

As New York pushes toward 70% renewable energy by 2030, accurate load forecasting becomes even more critical. Solar and wind add variability to net load (demand minus renewables), making confident forecasting essential for grid reliability during the energy transition.

**Next Steps:** Current model uses historical load and temperature proxies. Adding real weather forecasts and probabilistic outputs (P10/P50/P90 confidence intervals) could improve to 1.2-1.5% MAPE. The methodology is production-ready with daily retraining, bias correction, and comprehensive validation. Timeline for deployment: 6-12 months including weather integration and API development.

*Technical artifacts and code will are available at my GitHub repo:* [GitHub Repo](https://github.com/zenjen-dev/load_forecasting_ml) 
---

