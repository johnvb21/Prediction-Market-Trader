# Roadmap

## 1. Define the workflow

- Support Kalshi and Polymarket through separate adapters; choose the application interface.
- Specify market, forecast, trade, position, and settlement records.
- Define how partial fills, fees, sales, void markets, and settlements affect the ledger.

Done when: sample scenarios can be represented without ambiguous accounting.

## 2. Manual journal and paper portfolio

- Create and search a watchlist.
- Record versioned forecasts and supporting notes.
- Enter paper purchases, sales, fees, and settlements.
- Calculate positions and P&L from the transaction ledger.
- Export and restore local data.

Done when: a complete market lifecycle works with synthetic data, including a partial sale and settlement.

## 3. Read-only market data

- Verify the chosen venue's current official API documentation.
- Add separate Kalshi and Polymarket adapters for market metadata and prices, using a shared normalized model.
- Display source timestamps and stale-data status.
- Handle pagination, rate limits, and unavailable markets.

Done when: imported data can be reconciled with the venue and failures are visible.

## 4. Performance review

- Separate realized P&L, unrealized P&L, fees, deposits, and withdrawals.
- Track forecast calibration and Brier scores on resolved binary outcomes.
- Report exposure by market, category, and correlated event.

## 5. Optional execution

Separate future scope. Define explicit user controls, order validation, duplicate prevention, reconciliation, and execution limits before adding an order-capable adapter.
