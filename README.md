# Crypto-NLP-FinBERT-microsecond-execution

Overview
This Python-based system ingests live crypto news headlines from multiple RSS feeds, applies natural language processing (NLP) to score sentiment in real time, and simulates trades based on those signals.
It is designed for low-latency market reaction, with the ability to process, score, and trade within milliseconds of a headline appearing.

Key features:

Live polling of multiple reputable crypto news sources
Sentiment classification using FinBERT (finance-tuned BERT model)
Configurable position sizing and trade holding periods
One trade per ticker at a time to prevent overexposure
Human-readable terminal output with timestamps and structured columns
Skips stale news — only fresh headlines are eligible for trading


System Flow
RSS Feed Polling
Pulls headlines from a whitelist of crypto-focused publishers.
Filters for max age (default: 90 seconds).
Sentiment Analysis
Classifies as Positive, Negative, or Neutral.
Only trades if abs(score) >= min_abs_score (default: 0.4).
Trade Execution
Allocates a fixed % of total capital per eligible headline.
Only one open position per ticker at any time.
Positions auto-close after hold_sec seconds (default: 60).
Terminal Output
Shows classification events, trade entries, exits, and performance stats.


| Argument          | Description                                       | Default                 |
| ----------------- | ------------------------------------------------- | ----------------------- |
| `--tickers`       | List of tickers to trade                          | BTCUSDT ETHUSDT SOLUSDT |
| `--rss`           | RSS feed URLs to poll                             | Multiple crypto sites   |
| `--whitelist`     | Approved domains for headlines                    | Matches RSS list        |
| `--max_age`       | Max age (seconds) for headlines                   | 90                      |
| `--hold_sec`      | Position holding time in seconds                  | 60                      |
| `--capital`       | Total simulated capital                           | 1,000,000               |
| `--alloc_pct`     | Fraction of capital per trade                     | 0.05                    |
| `--model`         | NLP model (`finbert`, `roberta`, `vader`)         | finbert                 |
| `--minutes`       | Minutes of historical context for sentiment model | 30                      |
| `--long_th`       | Sentiment threshold to go long                    | 0.6                     |
| `--short_th`      | Sentiment threshold to short                      | -0.6                    |
| `--min_abs_score` | Minimum sentiment magnitude to trigger trade      | 0.4                     |
| `--cooldown`      | Cooldown per ticker (seconds) after a trade       | 600                     |

I use a bash wrapper to ensure the environment is activated and the script is launched correctly.
