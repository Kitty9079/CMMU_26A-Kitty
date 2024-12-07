# Low-risk Anomaly: Betting-Against-Correlation 
This Repository is for educational Purpose only.The objective of this code is to create BAC BAB and BAV Factor.
This research is aim to create Betting Against Correlation Factor return.

## Objective 
This research investigates the anomalies in excess returns after risk adjustment in groups of securities through two theories: Leverage Constraint Theory, which explains return anomalies through systematic risk using the BAC model, and Behavioral Effect Theory, which emphasizes the impact of idiosyncratic risk using the BAV model. The objectives of the study are to:

- Examine whether low-risk securities provide higher excess returns after risk adjustment compared to high-risk securities, which yield lower excess returns after risk adjustment.
- Determine whether the anomalies in excess returns explained by the BAC and BAV models can jointly account for excess returns after risk adjustment.
- Assess whether the anomalies in excess returns explained by the BAC model have a greater impact on the excess returns after risk adjustment, as measured by the BAB model, than those explained by the BAV model.

## Scope
This study utilizes data from companies listed on the Stock Exchange of Thailand (SET) that are included in the SET100 index, covering the period from January 2012 to December 2023, spanning 144 months and 226 securities. The research involves grouping securities by ranking them based on their risk coefficients from low to high, using percentiles to allocate the securities into groups. Portfolio rebalancing is conducted at the beginning of each month annually (Monthly Rebalancing), with group weights determined primarily by the Equal Weight method.

## Source of Data
- The study uses securities return data from the SETSMART database, specifically the Total Return Index (TRI) or Return on Investment (ROI). 
- The risk-free rate of return is calculated using the monthly return of 1-month maturity Treasury Bills (T-Bill1M). The return rate at the beginning of each month is sourced from the ThaiBMA database.

## Methodology
### 1.RiskFree Transform
Extract The riskfree return from First trading day of each month 
``` python 
# Convert 'Date' column to datetime format
df['Date'] = pd.to_datetime(df['Date'], dayfirst=True)

# Create 'Month_Year' column in the required format
df['Month_Year'] = df['Date'].dt.to_period('M').astype(str)

# Filter only the first trading day of each month
first_trading_day = df.groupby('Month_Year').first().reset_index()

```
### 2.Construct Volatility,Correlation,Beta
- Construct log_return with ROI from SETSMART DB 
``` python
    # Change ROI from decimal form to float form
    Data["pct_ROI"] = pd.to_numeric(Data.ROI).div(100)
    Data["pct_ROI"] = Data["pct_ROI"].round(5)
    # Calculate the log return
    Data["log_return"] = np.log(1 + Data["pct_ROI"])
    Data["log_return"] = Data["log_return"].round(5)
```
- Construct Volatility
  The volatility of each security is calculated using the one-day log-return over a one-year lookback period, employing the Rolling Window method.



