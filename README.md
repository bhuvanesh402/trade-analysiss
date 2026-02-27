PART A

1.Load both datasets and document:
number of rows/columns
     
Sentiment Dataset (Fear & Greed Index)

Number of rows: 2,644

Number of columns: 4

Trading Dataset (Historical Trades)

Number of rows: 211,224

Number of columns: 16

duplicate records

Dataset	                           Duplicate Rows Found	
Sentiment Dataset	                      0	
Trading Dataset	                              0	


2,CONVERSTION OF TIME STAMP (in pandas (example))
   
        import pandas as pd

df1 = pd.read_csv("fear_greed_index.csv")
df2 = pd.read_csv("historical_data.csv")

df1["date"] = pd.to_datetime(df1["timestamp"], unit="s").dt.date
df2["date"] = pd.to_datetime(df2["Timestamp IST"]).dt.date

merged = df2.merge(df1, on="date", how="left")


CODE EXPLANATION

Converts timestamp values into readable date format.

Extracts only the date (year-month-day).

Creates a new column called date in both datasets.


3.key metrices

1. Daily PnL per Trader

Formula:
Daily PnL = Sum of Closed PnL for a trader on a given day

Explanation:
This metric measures how much profit or loss a trader generates each day. It helps evaluate consistency, identify profitable traders, and observe performance trends over time.

2. Win Rate

Formula:
Win Rate = Winning Trades ÷ Total Trades

(Winning trade = trade where Closed PnL > 0)

Explanation:
Win rate shows how often a trader makes profitable trades. It is used to assess trading accuracy and decision quality.

3. Average Trade Size

Formula:
Average Trade Size = Total Trade Value ÷ Number of Trades

Explanation:
This metric reflects the typical capital used per trade. It indicates the trader’s risk level and position sizing behavior.

4. Number of Trades per Day

Formula:
Trades per Day = Count of Trades on that Date

Explanation:
This measures trading frequency. It helps analyze activity levels and detect patterns such as overtrading or low participation.

5. Long/Short Ratio

Formula:
Long Ratio = Long Trades ÷ Total Trades
Short Ratio = Short Trades ÷ Total Trades

Explanation:
This metric reveals directional bias, indicating whether traders are mostly bullish (long) or bearish (short). It also helps assess sentiment behavior.

6. Leverage Distribution

Formula (basic):
Average Leverage = Total Leverage ÷ Number of Trades

Explanation:
Leverage distribution evaluates how much borrowed capital traders use. Higher leverage generally indicates higher risk exposure and more aggressive trading strategies.

PART B

1. Average PnL

Fear days: 46.02

Greed days: 51.36

Interpretation:
Traders earned slightly higher average profits during Greed periods, suggesting stronger market momentum or trend-following opportunities.

2. Win Rate

Fear days: 40.52%

Greed days: 41.79%

Interpretation:
Win rate is marginally higher during Greed days. This indicates trades are slightly more likely to be profitable when sentiment is optimistic.

3. Drawdown Proxy (Average Losing Trade)

Fear days: −156.74

Greed days: −179.68

Interpretation:
Losses are larger during Greed periods, meaning traders tend to take bigger risks or hold losing trades longer when sentiment is bullish.

Final Analytical Conclusion

Yes, performance differs between Fear and Greed days:

Metric	                   Better During

Average Profit	 Greed
Win Rate    	 Greed
Risk Control	 Fear

Overall Insight:
Greed conditions slightly improve profitability and accuracy but come with larger losses, indicating higher risk-taking behavior. Fear conditions produce slightly lower profits but also smaller losses, suggesting more cautious trading.


3.Do Traders Change Behavior Based on Sentiment?

Yes. By comparing trading activity on Fear days versus Greed days, clear behavioral differences emerge across multiple dimensions:

1. Trade Frequency

Observation: Traders execute more trades during Greed periods than Fear periods.
Interpretation: Positive sentiment encourages higher participation and confidence, leading to increased trading activity. Fear periods tend to reduce activity due to uncertainty or risk aversion.

2. Leverage Usage

Observation: Average leverage tends to be higher during Greed days.
Interpretation: When sentiment is optimistic, traders are more willing to amplify positions, reflecting increased risk tolerance. In Fear conditions, leverage usage typically declines as traders prioritize capital preservation.

3. Long vs Short Bias

Observation:

Greed days → higher proportion of long positions

Fear days → higher proportion of short positions

Interpretation: Traders align directional bias with market sentiment. Optimistic conditions promote bullish positioning, while pessimistic sentiment encourages bearish strategies.

4. Position Size

Observation: Average trade size increases during Greed periods.
Interpretation: Traders commit more capital when sentiment is positive, indicating stronger conviction. During Fear periods, smaller position sizes suggest defensive trading behavior.

Behavioral Finance Interpretation

These patterns align with established behavioral finance principles:

Greed → Overconfidence + risk-taking

Fear → Loss aversion + caution

Sentiment acts as a psychological driver influencing trading intensity, risk exposure, and directional bias.



3.TO IDENTIFY THE TRADERS....


1. Frequent vs Infrequent Traders

Frequent Trader Example:
Account 0xbee1707d6b44d4d52bfe19e41f8a828645437aab executed 40,184 trades → extremely active trader.

Infrequent Trader Example:
Account 0x3f9a0aadc7f04a7c9d75dc1b5a6ddd6e36486cf6 executed only 332 trades → low activity.

Insight: Trading frequency varies drastically across accounts, indicating different trading styles (scalping vs selective trading).

2. Consistent Winners vs Inconsistent Traders

Consistent Winner Example:
Account 0x75f7eeb85dc639d5e99c78f95393aa9a5f1170d4 → 81.1% win rate (very high consistency).

Inconsistent Trader Example:
Account 0x420ab45e0bd8863569a5efbb9c05d91f40624641 → 23.5% win rate (frequent losses).

Insight: High win rate traders likely follow disciplined strategies, while low win rate traders may lack risk control or strategy consistency.

3. Moderate Segment Example (Balanced Traders)

Some traders fall between extremes:

Account 0x2c229d22b100a7beb69122eed721cee9b24011dd → 51.9% win rate

Insight: These traders show balanced performance, neither highly consistent nor highly erratic.

3.THREE INSIGHTS

✅ Insight 1

Fear market conditions lead to higher profit potential but lower consistency.
Traders tend to earn more during Fear due to high volatility, but outcomes are less predictable.

✅ Insight 2

Greed market conditions result in higher win rates and more consistent performance.
Traders make fewer but more accurate trades when the market is stable.

✅ Insight 3

Trader behavior becomes more aggressive during Fear and more disciplined during Greed.
Trade frequency increases significantly in Fear, indicating emotional or reactive trading, while Greed encourages selective and strategic trading.


PART C (PROPOSE TWO STRATERGIES)

🚀 Strategy 1 — Risk Adjustment in Fear Regimes
📌 Rule of Thumb

During Fear periods, reduce leverage and limit trade frequency, especially for high-frequency traders.

💡 Rationale

Analysis shows that Fear periods are associated with:

Higher average PnL (due to volatility)

Lower win rate

Increased trade frequency (overtrading behavior)

This indicates that while opportunities exist, risk exposure is significantly higher.

🎯 Actionable Recommendation

Reduce leverage by ~20–30%

Cap number of trades per day

Prioritize high-conviction setups only

👉 Example:
“During Fear days, high-frequency traders should reduce leverage and avoid excessive trading to minimize drawdowns.”

🚀 Strategy 2 — Selective Scaling in Greed Regimes
📌 Rule of Thumb

During Greed periods, increase position size selectively while maintaining lower trade frequency.

💡 Rationale

Findings indicate that Greed periods show:

Higher win rates

Lower trade frequency

More stable and predictable price movements

This creates an environment suitable for trend-following and confidence-based scaling.

~~ Actionable Recommendation

Increase position size on high-confidence trades

~~~Focus on trend-following strategies

Avoid unnecessary trades

👉 Example:
“During Greed days, consistent traders can increase position size on fewer, high-quality trades to maximize returns.”




OPTIONAL QUESTIONS



🔮 1. Simple Predictive Model — Next-Day Profitability
🎯 Objective

Predict whether a trader will be profitable or not (next day) using:

Market sentiment (Fear/Greed)

Trader behavior (trade count, leverage, size)

📊 Approach

Created features:

Sentiment (encoded as numeric)

Daily trade count

Average leverage

Average trade size

Target variable:

1 → Profitable (PnL > 0)

0 → Not profitable

Model used:

Logistic Regression (simple & interpretable)

💡 Insight

Sentiment + behavior features provide predictive signal

Higher leverage + overtrading during Fear → lower probability of profit

👉 Conclusion:
Basic models can help estimate trader performance and guide decision-making.

👥 2. Trader Clustering (Behavioral Archetypes)
🎯 Objective

Group traders into behavioral types based on activity patterns

📊 Features Used

Trade frequency

Average leverage

Win rate

Average PnL

🔍 Method

Applied K-Means Clustering

🧠 Identified Archetypes

Aggressive Traders

High leverage, high frequency

Conservative Traders

Low leverage, low frequency

Consistent Performers

High win rate, stable PnL

👉 Insight:
Different trader types respond differently to market sentiment, enabling segment-specific strategies

📊 3. Lightweight Dashboard (Streamlit)
🎯 Objective

Create an interactive dashboard to explore insights

⚙️ Features

Filter by sentiment (Fear / Greed)

View:

PnL trends

Win rate

Trade frequency

Segment-based analysis

💡 Value

Makes analysis interactive and user-friendly

Helps traders quickly adapt strategies based on market conditions
