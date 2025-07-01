# IBR Public Overview
Basic overview of the Interval Breach Reversion options model

**Sample Output:**  
--- Combined Portfolio Greeks Analyzer (Live + Proposed) ---

--- Existing Open Positions (6 trades) ---
| ticker   | option_type   | strike   | contracts   | live_delta   | stock_beta   | live_gamma   | live_theta   | live_vega   | premium_per_share   | live_charm   | live_vanna   | live_volga   |
|:---------|:--------------|:---------|:------------|:-------------|:-------------|:-------------|:-------------|:------------|:--------------------|:-------------|:-------------|:-------------|
| ARKK     | P             | 70       | 1           | -0.412       | 1.9          | 0.0257       | -0.0306      | 0.1334      | 5.13                | -0.149       | -0.0077      | 0            |
| ARKK     | P             | 55       | -1          | -0.1137      | 1.9          | 0.0111       | -0.0186      | 0.066       | 1.07                | -0.0846      | -0.3647      | 0.0015       |
| EWY      | P             | 72       | 1           | -0.4138      | 1.58         | 0.0317       | -0.0167      | 0.1588      | 4.05                | -0.0659      | -0.063       | 0.0001       |
| EWY      | P             | 60       | -1          | -0.1238      | 1.58         | 0.0146       | -0.0113      | 0.0834      | 0.95                | -0.0396      | -0.5715      | 0.0027       |
| URA      | P             | 38       | 1           | -0.4004      | 1.13         | 0.0456       | -0.012       | 0.0839      | 2.75                | -0.0451      | -0.033       | 0            |
| URA      | P             | 29       | -1          | -0.0838      | 1.13         | 0.0116       | -0.0058      | 0.0334      | 0.4                 | -0.0196      | -0.412       | 0.0012       |

--- Proposed New Positions (1 trades) ---
| ticker   | option_type   | strike   | contracts   | live_delta   | stock_beta   | live_gamma   | live_theta   | live_vega   | premium_per_share   | live_charm   | live_vanna   | live_volga   |
|:---------|:--------------|:---------|:------------|:-------------|:-------------|:-------------|:-------------|:------------|:--------------------|:-------------|:-------------|:-------------|
| ASHR     | C             | 28       | 2           | 0.5032       | 1.14         | 0.1505       | -0.0078      | 0.0532      | 1                   | -0.0268      | 0.1762       | -0           |

--- Combined Portfolio Greek Exposure (Live + Proposed) ---
Total Portfolio Capital (sum of premiums): $1151.00
- Total Delta: 10.15
- Total Gamma: 36.67
- Total Theta: -3.92
- Total Vega: 29.97
- Total Rho: -12.11
- Total Charm: -16.98
- Total Vanna: 159.69
- Total Volga: -0.53
- Portfolio Beta (Delta-Weighted): -23.54
- Normalized Delta ($ per $1 of capital): 0.0088
- Theta / Vega Ratio: -0.1308
- Gamma / |Theta| Ratio: 9.3546
- Volga / |Theta| Ratio: -0.1352

--- Analysis Complete ---



**Current Dir Tree:**  
breaches_forecasting # signal generation and portfolio management for options allocation
├── back_testing
│   ├── batch_backtest_analyzer.ipynb (BBA)
│   └── generate_forecast_output.ipynb (GFO)
├── db # historical data tables
│   ├── ARKG.parquet
│   ├── ARKK.parquet
│   ├── ...
│   └── YINN.parquet
├── parked # dev code and code that isn't currently used in production
├── project_management # research, docs and prompts
├── results
│   ├── original_pipeline # folder with ticker level back test data from GFO
│   │   ├── ARKG_L2-8y_CP0p010p050p1_SMam.parquet
│   │   ├── ARKK_L2-8y_CP0p010p050p1_SMam.parquet
│   │   ├── ...
│   │   └── YINN_L2-8y_CP0p010p050p1_SMam.parquet
│   ├── batch_sweep_analysis.csv # table with BBA output
│   ├── current_breaches.csv # output from BS
│   ├── current_breached_tickers.txt # output from MSF (Webull format for watchlist)
│   └── daily_screener_output.csv # output from MSF (Webull format for watchlist)
├── src
│   ├── __pycache__
│   ├── env
│   │   └── .env
│   ├── __init__.py 
│   ├── data_handler.py (DH) # defines api handlers for EODHD and Yfinance
│   ├── data_manager.py (DM) # ingesting and storing of data
│   ├── forecast.py (FCST) # Prophet forecast used in back testing etc.
│   ├── visualization.py (VIZ) # viz for (EF)
│   └── ticker_betas.csv # ticker betas for Greek calculations
├── webull_trade_data
│   ├── trade_analyzer.ipynb (TA) # reviews past trade data and generates P/L
│   └── Broker_Orders_Records_Options.csv 
└── workbooks
    ├── allocation_optimizer.ipynb (AO) # two stage optimizer for portfolio structuring
    ├── daily_screener.ipynb (DS) # daily/weekly screener, identifying breaches and 300d forecasts.
    ├── cross_sectional_analysis.ipynb (CSA) # secondary filter for breaches that removes the most highly correlated and those with lowest point potential
    ├── greek_calculations.ipynb (GC) # first and second order calculations for the AO
    └── manual_screen_filter.ipynb (MSF) # initial OI filter (manual check) of current breaches
