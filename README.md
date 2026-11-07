# Prediction Market Trader

Personal workspace for researching prediction markets, recording forecasts, tracking trades, and reviewing performance.

Status: project foundation. No exchange connections or order execution are implemented.

## First version

- Watchlist with platform, market URL, outcome, close date, and resolution rules.
- Forecast journal with probability estimates, rationale, sources, and timestamps.
- Paper trade ledger with price, quantity, fees, and settlement.
- Portfolio view with cost basis, exposure, realized P&L, and unrealized P&L.
- Review reports comparing forecasts with outcomes.

## Development sequence

See [the roadmap](docs/ROADMAP.md). Choose the initial platform and application format before selecting the stack. Start with manual entries and paper trades; add read-only market data afterward.

## Repository conventions

- Store timestamps in UTC and monetary values in decimal or integer minor units.
- Record platform and market identifiers on every trade.
- Preserve the history of forecasts and transactions.
- Keep API keys, account exports, and personal trading records out of Git.
- Use synthetic fixtures for examples and tests.

## Initial decisions

1. Platforms: Kalshi and Polymarket. Both are in scope; each gets a separate adapter behind a shared interface.
2. Interface: local web app, desktop app, or CLI.
3. Workflow: research and tracking, paper trading, or eventual order execution.

These are planning options, not implemented integrations.

## Platform architecture

Use a shared model for markets, outcomes, quotes, forecasts, transactions, and positions. Preserve venue identifiers, currencies, fee details, timestamps, and original resolution rules. Each venue adapter handles its own authentication, pagination, prices, and settlement semantics.

Market similarity does not establish equivalence: keep contracts separate unless their outcome and resolution rules have been explicitly reviewed. Live order execution is future scope.
