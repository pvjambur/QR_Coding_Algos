# Quant Track: Probability to HFT

Track 1 of 3 · Pranav's self-study roadmap · starts Tue 24 Nov 2026

This file is one of three. The three tracks rotate daily (Quant, then Investing, then Crypto, then back to Quant), and Sundays are left free for catch-up. So you do one track a day and never two. The full calendar is at the bottom of each file.

Everything linked here is free. Where a classic book is paid, it's marked "(paid, optional)" and nothing in the plan depends on it.

---

## 0. How to use this file

Each session is built for about 60 minutes:

| Block | Time | What you do |
|---|---|---|
| Warm-up | 5 min | One mental-math round on Zetamac (arithmetic.zetamac.com) or one probability puzzle |
| Watch / read | 20 to 25 min | The listed lecture or chapter. Use 1.5x speed for lectures |
| Code | 25 to 30 min | The listed notebook or C++ exercise. Always write the code yourself |
| Notes | 5 min | Three lines in `notes/quant.md`: what I learned, what confused me, one question |

If a session runs long, finish it next time the Quant day comes round instead of cramming. The dates will slip a bit, but the order is what matters.

Repo layout to create today:

```
quant-lab/
  notebooks/      q01_monte_carlo.ipynb, q02_returns.ipynb, ...
  cpp/            order_book/, spsc_queue/, mc_pricer/
  data/           cached CSVs (never commit large files)
  notes/quant.md
  reports/        checkpoint write-ups
```

Push it to your GitHub (github.com/pvjambur). By March this repo will be a portfolio piece on its own.

---

## 1. Map of the quant world (read once, today)

Quant work splits into roles that share the same foundations:

| Role | What they do daily | Core skills |
|---|---|---|
| Quant Researcher (QR) | Find signals, build models, test them | Probability, statistics, econometrics, ML, Python |
| Quant Trader (QT) | Run strategies, price risk, make markets | Fast probability, expected value, options, game theory |
| Quant Developer / HFT engineer | Build trading systems that run in microseconds | C++, concurrency, networking, OS internals, data structures |

People on r/quant keep repeating the same thing: you can't skip the math by jumping straight to strategies, and a backtest that looks great is usually wrong. This plan follows that advice. Probability and statistics come first, then time series, then stochastic calculus and options, then backtesting, and HFT systems last.

What firms like Graviton, Tower Research, Optiver and IMC actually do:
- Market making: always quoting a bid and an ask, earning the spread, and managing the inventory risk. The Avellaneda-Stoikov model (Session Q26) is the textbook version.
- Statistical arbitrage: trading small, repeatable mispricings between related instruments, like pairs, index vs futures, or options vs underlying.
- Latency-sensitive execution: being first to react to new information. This is why C++, kernel bypass networking, FPGAs and co-location matter.
- In India, most of this happens in NSE equity derivatives (Nifty and Bank Nifty options and futures). Graviton is India's homegrown HFT firm, now valued above a billion dollars, and it trades Indian stocks and derivatives. Global firms like Tower Research, Jane Street, Citadel Securities and IMC also trade in India.

---

## 2. Core resources (the spine of this track)

Math and probability
- Harvard Stat 110 (Joe Blitzstein): lectures on YouTube via [stat110.hsites.harvard.edu/youtube](https://stat110.hsites.harvard.edu/youtube). The free textbook PDF and practice problems are on the same site.
- MIT 18.S096 Topics in Mathematics with Applications in Finance: [YouTube playlist](https://www.youtube.com/playlist?list=PLUl4u3cNGP63ctJIEC1UnZ0btsphnnoHR). It covers linear algebra, probability, stochastic processes, regression, VaR, portfolio theory, Itô calculus and Black-Scholes.
- MIT RES.6-012 Introduction to Probability (Tsitsiklis), on MIT OCW and YouTube: short clips, useful when a Stat 110 lecture didn't click.
- 3Blue1Brown, "Essence of Linear Algebra" playlist on YouTube, for intuition before 18.S096 lecture 2.

Statistics, econometrics, time series
- Quantopian Lecture Series (archived after Quantopian shut down in 2020): notebooks in [quantopian/research_public](https://github.com/quantopian/research_public), browsable on [nbviewer](https://nbviewer.org/github/quantopian/research_public/tree/master/notebooks/lectures). QuantRocket kept a [maintained adaptation](https://www.quantrocket.com/codeload/quant-finance-lectures/quant_finance_lectures/Introduction.ipynb.html) covering means, variance, correlation, regression, model violations, ARCH/GARCH, cointegration, pairs trading and factor models.
- Ben Lambert, "Undergraduate Econometrics" playlist on YouTube: 199 short videos, from estimators through to cointegration.
- Forecasting: Principles and Practice, the Pythonic Way (Hyndman et al.): free online at [otexts.com/fpppy](https://otexts.com/fpppy/). The R edition is at [otexts.com/fpp3](https://otexts.com/fpp3/) if you want to try R.
- QuantEcon lectures (Sargent and Stachurski): [quantecon.org/lectures](https://quantecon.org/lectures/), for Python numerics, Markov chains and time series models.
- An Introduction to Statistical Learning with Python (ISLP): free PDF at [statlearning.com](https://www.statlearning.com/).

Stochastic calculus, Monte Carlo, options
- Quant Guild (Roman Paolucci) on YouTube, with every video's notebook in the [Quant Guild Library](https://github.com/romanmichaelpaolucci/Quant-Guild-Library). Covers Monte Carlo, Black-Scholes, SDEs, Heston, volatility and backtesting.
- sentdex, "Monte Carlo Simulation with Python" playlist on YouTube (19 videos, betting-strategy simulations). Light and fun.
- Matt Macarty on YouTube: practical Python for stock data, screeners, options and backtesting. Good for quick how-tos.

Systematic trading and backtesting
- Robert Carver's blog [qoppac.blogspot.com](https://qoppac.blogspot.com) and his open-source engine [pysystemtrade](https://github.com/robcarver17/pysystemtrade). A real systematic trader writing honestly about position sizing, costs and overfitting.
- QuantStart, [Free Quantitative Finance Resources](https://www.quantstart.com/articles/Free-Quantitative-Finance-Resources) and their self-study plan articles.
- [awesome-quant](https://github.com/wilsonfreitas/awesome-quant): the master list of libraries and data sources.

Market microstructure and HFT
- Avellaneda and Stoikov (2008), "High-frequency trading in a limit order book": [free PDF](https://math.nyu.edu/~avellane/HighFrequencyTrading.pdf).
- [hftbacktest](https://github.com/nkaz001/hftbacktest): a free Python and Rust backtester that models queue position and latency, with tutorials on market making and order book imbalance.
- Jane Street Tech Talks on YouTube, especially "How to Build an Exchange" (Brian Nigito). [List of talks](https://blog.janestreet.com/watch-all-of-jane-streets-tech-talks/).

C++, concurrency, low latency
- [learncpp.com](https://www.learncpp.com/) for C++ refreshers, and cppreference.com for reference.
- Carl Cook, "When a Microsecond Is an Eternity: High Performance Trading Systems in C++" (CppCon 2017, YouTube).
- David Gross (Optiver), "When Nanoseconds Matter: Ultrafast Trading Systems in C++" (CppCon 2024 keynote, YouTube). [Optiver's write-up](https://www.optiver.com/insights/technology-blog/designing-low-latency-cpp-systems/).
- Herb Sutter, [atomic&lt;&gt; Weapons](https://herbsutter.com/2013/02/11/atomic-weapons-the-c-memory-model-and-modern-hardware/) (memory model, 2 parts) and "Lock-Free Programming (or, Juggling Razor Blades)" (CppCon 2014, 2 parts).
- Fedor Pikus, "C++ atomics, from basic to advanced" (CppCon 2017).
- Charles Frasch, "Single Producer Single Consumer Lock-free FIFO From the Ground Up" (CppCon 2023).
- Bilokon and Gunduz, "C++ Design Patterns for Low-latency Applications Including High-frequency Trading": [arXiv 2309.04259](https://arxiv.org/abs/2309.04259), with code in [0burak/imperial_hft](https://github.com/0burak/imperial_hft).
- [awesome-lockfree](https://github.com/zodsoft/awesome-lockfree): links to Drepper's "What Every Programmer Should Know About Memory" and McKenney's free parallel programming book.

Puzzles and interview practice (5-minute warm-ups)
- [Jane Street puzzles](https://www.janestreet.com/puzzles/) (a new one every month or two)
- Brainstellar (free puzzle sets, easy to hard)
- [QuantVault](https://quantvault.org/problems.html) (the free subset with full solutions)
- Zetamac for mental math

Community
- [r/quant wiki](https://www.reddit.com/r/quant/wiki/) (FAQ plus book threads), r/algotrading, r/cpp and r/hft. Search these before asking a question; most beginner questions have already been answered there.

Classic books (paid, optional, not needed for this plan): Hull's Options, Futures and Other Derivatives; Natenberg's Option Volatility and Pricing; Zhou's "Green Book" for interviews; Chan's Quantitative Trading; Shreve's Stochastic Calculus for Finance.

---

## 3. The sessions

### Block A · Python for data and probability foundations

#### Q01 · Tue 24 Nov 2026 · Setup and your first Monte Carlo
- Setup (15 min): install Miniconda or uv, create a `quant` environment with `numpy pandas matplotlib scipy statsmodels yfinance jupyterlab`, and create the repo above.
- Watch: Stat 110 Lecture 1 (sample spaces, the naive definition of probability, counting).
- Code: open the starter notebook `q01_starter.ipynb` I've sent with this file. It walks through coin flips, the law of large numbers, Monte Carlo estimation of pi and its error, a random walk, and your first simulated stock path. Finish every TODO cell.
- Answer in your notes: why does the Monte Carlo error shrink like 1/sqrt(n), and what does that cost you in compute to get one more correct decimal place?

#### Q02 · Fri 27 Nov 2026 · Python data stack on real prices
- Read/run: Quantopian lectures on Python, NumPy, pandas and plotting (lectures 2 to 5 in the QuantRocket version).
- Code `q02_returns.ipynb`: download 10 years of `^NSEI` (Nifty 50), `RELIANCE.NS`, `^GSPC` and `BTC-USD` with yfinance. Compute simple and log returns, cumulative returns and rolling 30-day volatility, and plot all of them. Save the data to `data/` so you aren't downloading it again every time.
- Question: when do log returns and simple returns differ meaningfully, and why do quants prefer log returns for adding up returns over time?

#### Q03 · Tue 1 Dec 2026 · Counting, conditional probability, Bayes
- Watch: Stat 110 Lectures 2 to 4 (story proofs, axioms, conditional probability, Monty Hall, Bayes).
- Code: simulate the Monty Hall problem, the birthday problem (find the smallest group where P(shared birthday) is over 50%) and a medical-test Bayes example. Check each simulation against the exact formula.
- Puzzles: 5 easy Brainstellar puzzles.

#### Q04 · Fri 4 Dec 2026 · Random variables and distributions
- Watch: Stat 110 lectures on random variables, Binomial, Poisson and expectation (lectures 7 to 10 roughly; follow the playlist order).
- Read: Quantopian lectures "Means", "Variance" and "Statistical Moments".
- Code: plot a histogram of Nifty daily returns against a fitted Normal, draw a QQ plot, compute skewness and kurtosis, and count how many days are more than 4 sigma away. A Normal distribution predicts almost none, so compare that with what you actually find.
- This session is the first time you'll see "fat tails" in real data. Every risk model later on has to deal with them.

#### Q05 · Tue 8 Dec 2026 · Expectation, variance, conditioning, and EV thinking
- Watch: Stat 110 lectures on LOTUS, variance, and conditional expectation.
- Practice: 10 free QuantVault problems tagged Expectation, solved on paper first and then checked with a simulation.
- Trader angle: expected value is the core of trading interviews. For each problem, write "what bet would I take, and at what price?"

#### Q06 · Fri 11 Dec 2026 · CHECKPOINT 1: Return distribution report
Mini project `reports/cp1_returns.ipynb`:
1. For Nifty 50, Reliance, S&P 500 and BTC: mean, volatility, skew, kurtosis, max drawdown, and the worst 5 days.
2. Autocorrelation of returns and of squared returns (plot both). You should find that returns are nearly uncorrelated, but squared returns are clearly correlated. That's volatility clustering.
3. One-day 99% Value at Risk three ways: historical, Normal (parametric), and Monte Carlo from a fitted Student-t distribution.
4. One paragraph: which method would you trust for BTC, and why?

Report back to me: your VaR table, your kurtosis numbers, and the one result that surprised you.

### Block B · Statistics, regression, econometrics, time series

#### Q07 · Tue 15 Dec 2026 · Normal distribution, LLN, CLT
- Watch: Stat 110 lectures on the Normal distribution and the CLT; Quant Guild "Why Monte Carlo Simulation Works".
- Code: show the CLT by averaging Uniform, Exponential and Pareto draws (use a Pareto with alpha under 2). Watch where the CLT breaks: infinite variance means no CLT. Connect this back to the fat tails you found in Q04.

#### Q08 · Fri 18 Dec 2026 · Estimation, MLE, confidence intervals, hypothesis tests
- Watch: Ben Lambert econometrics videos on estimators, unbiasedness and consistency (roughly videos 6 to 15).
- Read/run: Quantopian "Confidence Intervals", "Hypothesis Testing" and "Instability of Estimates".
- Code: estimate the mean daily return of Nifty with a 95% CI. How many years of data would you need for that CI to exclude zero? This is why alpha is so hard to prove.

#### Q09 · Tue 22 Dec 2026 · Linear regression from scratch
- Watch: Ben Lambert's OLS and Gauss-Markov videos.
- Read/run: Quantopian "Linear Regression", "Violations of Regression Models" and "Model Misspecification".
- Code: write OLS with NumPy (beta equals (X'X) inverse times X'y) and check it against `statsmodels`. Estimate the CAPM beta of 5 Nifty stocks against Nifty 50. Plot residuals and test for heteroskedasticity.

#### Q10 · Fri 25 Dec 2026 · Time series I: stationarity, AR, MA, ARIMA
- Read: FPP Pythonic, the chapters on time series graphics, stationarity and differencing, and ARIMA.
- Read/run: Quantopian "Autocorrelation and AR Models".
- Code: run an ADF test on price vs returns, look at ACF/PACF plots, fit AR(1) and ARIMA to the log of Nifty, and forecast. Then honestly compare the forecast with a random walk forecast. Spoiler: the random walk usually wins.
- Optional R detour: redo one plot in R with the fpp3 edition to get a feel for R.

#### Q11 · Tue 29 Dec 2026 · Time series II: volatility models and cointegration
- Read/run: Quantopian "ARCH, GARCH and GMM" and "Integration, Cointegration and Stationarity".
- Watch: Ben Lambert's cointegration videos (near the end of the playlist: integrated processes, cointegration intro, cointegration tests).
- Code: fit GARCH(1,1) to Nifty returns with the `arch` package and plot the conditional volatility. Then find a cointegrated pair among HDFCBANK, ICICIBANK, KOTAKBANK and AXISBANK using the Engle-Granger test.

#### Q12 · Fri 1 Jan 2027 · CHECKPOINT 2: Pairs trading study
Mini project `reports/cp2_pairs.ipynb`, following the Quantopian "Introduction to Pairs Trading" lecture:
1. Choose the pair from Q11. Estimate the hedge ratio on 2015 to 2021 data only.
2. Build the spread and its z-score. Enter at |z| > 2 and exit at |z| < 0.5.
3. Test it on 2022 to today (out of sample). Include 0.1% transaction cost per side.
4. Plot equity, Sharpe ratio, max drawdown and number of trades. Check whether the cointegration still holds out of sample.

Report back: in-sample vs out-of-sample Sharpe, and whether the relationship broke.

### Block C · Stochastic processes, Monte Carlo, options

#### Q13 · Tue 5 Jan 2027 · Markov chains and random walks
- Watch: Stat 110 Markov chain lectures (near the end of the course).
- Read: QuantEcon's finite Markov chains lecture.
- Code: gambler's ruin by simulation and by the exact formula; a 2-state "bull/bear" Markov chain for market regimes estimated from Nifty monthly returns, with its stationary distribution.

#### Q14 · Fri 8 Jan 2027 · Brownian motion and GBM
- Watch: MIT 18.S096 Lecture 5 (Stochastic Processes I).
- Code: simulate Brownian motion paths and check that variance grows linearly with time. Simulate GBM using mu and sigma estimated from Nifty, and compare the simulated distribution of 1-year returns with the actual one.

#### Q15 · Tue 12 Jan 2027 · Itô calculus without fear
- Watch: MIT 18.S096 Lectures 17 and 18 (Stochastic Processes II, Itô calculus). Quant Guild's video on SDEs for quant finance.
- Code: Euler-Maruyama for GBM vs the exact solution, then an Ornstein-Uhlenbeck (mean-reverting) process. OU is the model behind the pairs spread from Q12.
- Write in your notes, in your own words: why the extra minus half sigma squared term appears in the drift of log price.

#### Q16 · Fri 15 Jan 2027 · Options and Black-Scholes
- Watch: MIT 18.S096 Lecture 19 (Black-Scholes, risk-neutral valuation).
- Code: implement Black-Scholes call/put pricing and the Greeks (delta, gamma, vega, theta) in Python, and verify put-call parity numerically.
- Real-world look: open the NSE Nifty option chain on nseindia.com. Write down strikes, premiums and implied volatility for the nearest expiry, plug them into your pricer, and try to back out the IV with a root finder.

#### Q17 · Tue 19 Jan 2027 · Monte Carlo pricing and variance reduction
- Watch/run: Quant Guild "Monte Carlo Simulation and Black-Scholes for Pricing Options" with its notebook, and "How to Price Options with Monte Carlo Simulation".
- Code: an MC price for a European call that converges to your Black-Scholes price. Add antithetic variates and a control variate, and plot error against number of paths for each. Then price an Asian option, which has no simple closed form, so MC is the natural tool.

#### Q18 · Fri 22 Jan 2027 · CHECKPOINT 3: Option pricer lab (Python and your first C++)
Mini project `cpp/mc_pricer/` plus `reports/cp3_pricer.md`:
1. Python: Black-Scholes, a binomial tree (CRR) and MC pricers for the same option, all agreeing to within 1%.
2. C++17: port the MC pricer using `<random>` (mt19937_64) and a plain loop. Compile with `-O2`, then with `-O3 -march=native`.
3. Time 10 million paths in Python (pure loops), NumPy (vectorized) and C++. Put the timings in a table.
4. Bonus: split the paths across `std::thread`s and measure the speedup. Note what happens when every thread shares one random generator.

Report back: the timing table, and what happened with the shared generator.

### Block D · Systematic trading and backtesting

#### Q19 · Tue 26 Jan 2027 · Why most backtests lie
- Read: Robert Carver's qoppac posts on costs and overfitting (search the blog for "overfitting" and "costs"); the Quantopian lecture on overfitting ("The Dangers of Overfitting" in the lecture list).
- Paper: Bailey, Borwein, López de Prado and Zhu, "The Probability of Backtest Overfitting" (free on SSRN). Skim the intro and conclusions.
- Exercise: generate 1,000 random-signal strategies on Nifty and report the best Sharpe ratio. That number shows how much luck can produce on its own.

#### Q20 · Fri 29 Jan 2027 · Build a vectorized backtester
- Code `bt.py`: a small pandas backtester with signals, a one-bar delay (no lookahead), position sizing, costs (brokerage plus STT plus slippage), and metrics (CAGR, Sharpe, Sortino, max drawdown, turnover).
- Test it on an SMA crossover and 12-month momentum on 20 Nifty stocks. Write a unit test that deliberately introduces lookahead, so you know the delay is doing its job.

#### Q21 · Tue 2 Feb 2027 · Factor investing
- Read/run: Quantopian "CAPM and Arbitrage Pricing Theory", "Fundamental Factor Models" and "Case Study: Traditional Value Factor".
- Code: a cross-sectional momentum factor on about 50 large Indian stocks. Each month, rank, go long the top quintile, and compute the information coefficient (IC). Watch out for survivorship bias, since today's index members weren't the index members 10 years ago.

#### Q22 · Fri 5 Feb 2027 · Portfolio construction and sizing
- Watch: MIT 18.S096 Lecture 16 (Portfolio Management).
- Read: the pysystemtrade docs and Carver's posts on volatility targeting.
- Code: mean-variance optimization with a long-only constraint, risk parity, and inverse-volatility weights on 5 assets (Nifty, gold ETF, a G-sec proxy, S&P 500, BTC). Show how unstable the mean-variance weights are when you change the inputs slightly. Then simulate the Kelly criterion vs half-Kelly on a biased coin.

#### Q23 · Tue 9 Feb 2027 · Machine learning in finance, carefully
- Read: ISLP chapters on resampling and cross-validation, plus tree-based methods.
- Concept: in time series, ordinary k-fold cross-validation leaks future data into the past. Learn walk-forward validation and "purging" (López de Prado's idea).
- Code: a gradient-boosted classifier for the next-day direction of Nifty using lagged returns and volatility, with walk-forward validation. Expect about 50% accuracy, and work out why.

#### Q24 · Fri 12 Feb 2027 · CHECKPOINT 4: Your first systematic strategy report
Mini project `reports/cp4_strategy.ipynb`:
1. A volatility-targeted trend-following system (an EWMA crossover, Carver style) on 4 to 6 instruments.
2. Walk-forward parameter choice, realistic costs, and position caps.
3. A tear sheet with equity curve, drawdowns, rolling Sharpe and monthly returns heatmap, plus a comparison with buy-and-hold.
4. A "how could this be wrong" section listing at least five ways your backtest could be fooling you.

Report back: the tear sheet image and your list of five ways it could be wrong.

### Block E · Market microstructure, HFT and low-latency C++

#### Q25 · Tue 16 Feb 2027 · The limit order book
- Watch: Jane Street "How to Build an Exchange" (Brian Nigito).
- Learn: bid, ask, spread, depth, market vs limit orders, price-time priority, tick size, queue position, maker vs taker fees, and co-location (NSE offers it to members).
- Code: a Python LOB that accepts limit, market and cancel orders, matches them by price-time priority, and prints the book. Test it with 20 hand-written orders.

#### Q26 · Fri 19 Feb 2027 · The math of market making
- Read: Avellaneda-Stoikov (2008), sections 1 to 3. Focus on the reservation price (mid price shifted by inventory) and the optimal spread.
- Code: reproduce their simulation, a symmetric naive strategy vs the inventory strategy, with Poisson order arrivals. Compare the P&L distributions.
- Then run one hftbacktest tutorial (start with the basic market making example) to see queue position and latency added on top.

#### Q27 · Tue 23 Feb 2027 · C++ for speed: an order book in C++
- Refresh on learncpp.com: move semantics, templates, `std::vector` vs `std::map`, and RAII.
- Watch: Carl Cook's CppCon 2017 talk.
- Code `cpp/order_book/`: port your Q25 LOB to C++. Make two versions, one with `std::map<price, deque>` and one with a flat array indexed by price tick. Benchmark 1 million random operations with `std::chrono` (or Google Benchmark) and compare.

#### Q28 · Fri 26 Feb 2027 · Concurrency: atomics, memory order, SPSC queue
- Watch: Herb Sutter "atomic&lt;&gt; Weapons" Part 1; Charles Frasch's SPSC FIFO talk (CppCon 2023).
- Code `cpp/spsc_queue/`: a lock-free single-producer single-consumer ring buffer with `std::atomic` and acquire/release ordering. Benchmark it against a `std::mutex` plus `std::queue` version. Then add `alignas(64)` padding between the head and tail indices and measure again. The difference you see is false sharing.

#### Q29 · Tue 2 Mar 2027 · How real low-latency systems are designed
- Watch: David Gross, "When Nanoseconds Matter" (CppCon 2024).
- Read: Bilokon and Gunduz (arXiv 2309.04259), especially the patterns section (cache warming, constexpr, hot path vs cold path, branch reduction). Clone their repo and run two benchmarks.
- Skim: the CPU cache sections of Drepper's memory paper.
- Write a one-page note: "What a tick-to-trade path looks like at a firm like Graviton or Optiver." Cover the stages from the network card to the feed handler, the order book, the strategy, risk checks and the order gateway. Mention where FPGAs come in and why every component avoids allocation on the hot path.

#### Q30 · Fri 5 Mar 2027 · CHECKPOINT 5 (capstone): Mini trading engine
Project `cpp/mini_engine/` plus `reports/cp5_engine.md`:
1. Thread 1 (feed): replays a CSV of orders (generate them in Python) into an SPSC queue.
2. Thread 2 (engine): your array-based order book, which matches orders and publishes trades to a second SPSC queue.
3. Thread 3 (strategy): a toy market maker using the Avellaneda-Stoikov quoting rule from Q26.
4. Measure latency per message (p50, p99, p99.9) and plot a histogram. Then try core pinning (`taskset`) and compare.

Report back: the latency histogram, your p99 number, and the biggest bottleneck you found.

---

## 4. After the 30 sessions: where to go deep

You'll have seen every branch. Pick one based on what you enjoyed most:

| If you liked | Go deep into | Next free resource |
|---|---|---|
| Q07 to Q11 (stats, time series) | Quant research, alpha research | Quantopian lectures 30 onwards; FPP fully; López de Prado's papers on SSRN |
| Q13 to Q18 (stochastic, options) | Derivatives pricing, volatility | MIT 18.S096 in full; Quant Guild's Heston and FFT videos; QuantLib |
| Q19 to Q24 (backtesting) | Systematic trading | pysystemtrade source code; Carver's full blog archive |
| Q25 to Q30 (microstructure, C++) | Quant dev and HFT | hftbacktest's advanced tutorials; the CppCon low-latency playlist; Jane Street's tech blog |

Dates worth putting in your calendar:
- IMC Prosperity: IMC's free global trading challenge for university students, usually held in April (Prosperity 4 started 14 April 2026). You write a Python trading bot over five rounds. Watch [imc.com/prosperity](https://www.imc.com/us/prosperity) for registration around March 2027. It's the single best test of everything in Blocks D and E.
- Jane Street's monthly puzzle: try it every month.

---

## 5. Activity log (fill this in and send it to me at each checkpoint)

| Checkpoint | Date | Key numbers | What surprised me | What I'm stuck on |
|---|---|---|---|---|
| CP1 Returns | Fri 11 Dec 2026 | | | |
| CP2 Pairs | Fri 1 Jan 2027 | | | |
| CP3 Pricer | Fri 22 Jan 2027 | | | |
| CP4 Strategy | Fri 12 Feb 2027 | | | |
| CP5 Engine | Fri 5 Mar 2027 | | | |

---

## 6. Full rotation calendar

Codes: Q = Quant (01_quant.md), I = Investing (02_investing.md), C = Crypto (03_crypto.md). Sundays are catch-up days. All 90 sessions finish on Mon 8 Mar 2027. If you miss a day, just do the next session in the rotation; the order matters more than the dates.

| Week of | Mon | Tue | Wed | Thu | Fri | Sat | Sun |
|---|---|---|---|---|---|---|---|
| 23 Nov |  | 24 Q01 | 25 I01 | 26 C01 | 27 Q02 | 28 I02 | 29 catch-up |
| 30 Nov | 30 C02 | 1 Q03 | 2 I03 | 3 C03 | 4 Q04 | 5 I04 | 6 catch-up |
| 7 Dec | 7 C04 | 8 Q05 | 9 I05 | 10 C05 | 11 Q06 | 12 I06 | 13 catch-up |
| 14 Dec | 14 C06 | 15 Q07 | 16 I07 | 17 C07 | 18 Q08 | 19 I08 | 20 catch-up |
| 21 Dec | 21 C08 | 22 Q09 | 23 I09 | 24 C09 | 25 Q10 | 26 I10 | 27 catch-up |
| 28 Dec | 28 C10 | 29 Q11 | 30 I11 | 31 C11 | 1 Q12 | 2 I12 | 3 catch-up |
| 4 Jan | 4 C12 | 5 Q13 | 6 I13 | 7 C13 | 8 Q14 | 9 I14 | 10 catch-up |
| 11 Jan | 11 C14 | 12 Q15 | 13 I15 | 14 C15 | 15 Q16 | 16 I16 | 17 catch-up |
| 18 Jan | 18 C16 | 19 Q17 | 20 I17 | 21 C17 | 22 Q18 | 23 I18 | 24 catch-up |
| 25 Jan | 25 C18 | 26 Q19 | 27 I19 | 28 C19 | 29 Q20 | 30 I20 | 31 catch-up |
| 1 Feb | 1 C20 | 2 Q21 | 3 I21 | 4 C21 | 5 Q22 | 6 I22 | 7 catch-up |
| 8 Feb | 8 C22 | 9 Q23 | 10 I23 | 11 C23 | 12 Q24 | 13 I24 | 14 catch-up |
| 15 Feb | 15 C24 | 16 Q25 | 17 I25 | 18 C25 | 19 Q26 | 20 I26 | 21 catch-up |
| 22 Feb | 22 C26 | 23 Q27 | 24 I27 | 25 C27 | 26 Q28 | 27 I28 | 28 catch-up |
| 1 Mar | 1 C28 | 2 Q29 | 3 I29 | 4 C29 | 5 Q30 | 6 I30 | 7 catch-up |
| 8 Mar | 8 C30 |  |  |  |  |  |  |
