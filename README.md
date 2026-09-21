# Hotel Bar Inventory Forecasting & Par Level System

Forecasting and inventory recommendation system for hotel bars, built from raw pour-level transaction logs. Predicts item-level demand per bar and recommends a dynamic par level (how much stock to keep on hand), then backtests the recommendation against real historical data.

## Problem

A hotel chain's bars face two conflicting issues: stockouts of popular drinks (lost sales, unhappy guests) and overstocking of slow movers (wasted cash and storage). Stock levels are currently set by guesswork rather than data.

## What this does

- Cleans raw transaction logs and fills in implicit zero-demand days (81% of all possible bar-brand-days had no sale, and that had to be made explicit before any modeling)
- Compares three forecasting approaches — a 7-day rolling average baseline, a day-of-week adjusted version, and a linear regression — and picks whichever actually performs best on held-out data
- Computes a par level per bar/brand using expected demand plus a volatility-scaled safety stock
- Backtests the recommendation against real history to quantify the trade-off

## Results

- Simplest model (7-day rolling average) won on accuracy (WAPE ~1.66), beating both the day-of-week adjustment and linear regression
- Simulated stockout-days dropped **68.6%** using the recommended par-level policy vs. a naive fixed-average policy
- Average stock held per item rose **347%** — the real cost of fewer stockouts

## Structure

```
notebooks/inventory_forecasting_solution.ipynb   # full end-to-end solution
report/business_report.md                        # write-up: problem, assumptions, model choice, results
video_script/video_walkthrough_outline.md        # script for the video walkthrough
data/raw/                                         # original dataset
data/processed/                                   # cleaned daily series, par levels, simulation output
```

## How to run

**Option 1 — Colab**
Open `inventory_forecasting_solution.ipynb` in Google Colab, run the first cell, upload the dataset CSV when prompted, then Runtime → Run all.

**Option 2 — Locally**
```
pip install -r requirements.txt
jupyter notebook notebooks/inventory_forecasting_solution.ipynb
```

## Stack

Python, pandas, numpy, scikit-learn, matplotlib
