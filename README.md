**SUPERTREND PARAM SETTINGS:**



SUPERTREND\_ATR\_PERIOD = 10    # ← Change ATR lookback period

SUPERTREND\_MULTIPLIER = 3.0   # ← Change band multiplier



**Setting		More Signals (Sensitive)	Fewer Signals (Strict)**

ATR Period	Lower (e.g. 7)			Higher (e.g. 14)

Multiplier	Lower (e.g. 2.0)		Higher (e.g. 4.0)


Combo			Style			Good For

ATR=7, Mult=2.0		Tibght — flips often	Scalping / short-term

ATR=10, Mult=3.0	Standard (current)	Swing trading

ATR=14, Mult=4.0	Wide — rarely flips	Long-term trend following



**Interval	Data Available	Best For**

5m		5 days		Scalping

10m		5 days		Quick trades

15m		5 days		Short-term swing

20m		5 days		Balanced

30m		5 days		Intraday swing

45m		5 days		Less noise

1h		60 days		Intraday trend





**Interval	Max Data	Best For**

1m	1 day	Ultra scalping

2m	1 day	Fast scalping

5m	5 days	Scalping

10m–45m	5 days	Intraday swing

1h	60 days	Intraday trend



SUPERTREND PARAM SETTINGS:

SUPERTREND_ATR_PERIOD = 10    # ← Change ATR lookback period
SUPERTREND_MULTIPLIER = 3.0   # ← Change band multiplier

Setting		More Signals (Sensitive)	Fewer Signals (Strict)
ATR Period	Lower (e.g. 7)			Higher (e.g. 14)
Multiplier	Lower (e.g. 2.0)		Higher (e.g. 4.0)

Combo			Style			Good For
ATR=7, Mult=2.0		Tight — flips often	Scalping / short-term
ATR=10, Mult=3.0	Standard (current)	Swing trading
ATR=14, Mult=4.0	Wide — rarely flips	Long-term trend following



Interval	Data Available	Best For
5m		5 days		Scalping
10m		5 days		Quick trades
15m		5 days		Short-term swing
20m		5 days		Balanced
30m		5 days		Intraday swing
45m		5 days		Less noise
1h		60 days		Intraday trend

1m and 2m only give ~1 day of bars (~390 bars for 1m, ~195 for 2m). Ichimoku needs 52 bars so it'll work, but signals will be based on very short-term data — use with caution.

Confirmation	What It Means					Strength
CONFIRMED BUY	Daily says BUY + Intraday says BUY		Strongest — both timeframes aligned
CONFIRMED SELL	Daily says SELL + Intraday says SELL		Strongest bearish
DAILY ONLY	Daily says BUY/SELL, but intraday says HOLD	Good setup, but intraday hasn't caught up yet
INTRADAY ONLY	Intraday says BUY/SELL, but daily says HOLD	Short-term move, no daily support — riskier
-		Both say HOLD					No trade


1. Filter scanner → Confirmation: [CONFIRMED BUY, CONFIRMED SELL]
2. Check the R/R ratio → only take R/R ≥ 1.5
3. Enter at live price → SL at Supertrend → Target at BB band



R/R = Potential Reward ÷ Potential Risk

Reward = Target price − Entry price
Risk   = Entry price − Stop Loss


def fetch_history(symbol, **kwargs):
    """Bulletproof history fetch — works with ALL yfinance versions."""
    try:
        df = yf.download(symbol, progress=False, **kwargs)
    except:
        df = pd.DataFrame()
    if df.empty:
        try:
            df = yf.Ticker(symbol).history(**kwargs)
        except:
            return pd.DataFrame()
    if isinstance(df.columns, pd.MultiIndex):
        df.columns = [c[0] if isinstance(c, tuple) else c for c in df.columns]
    df = df.loc[:, ~df.columns.duplicated()]
    return df






