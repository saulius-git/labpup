# Development updates

## 2026-10-13 — Refresh recovery

- Added background market and trade refreshes from page requests when collection or 24-hour trade synchronization is overdue.
- Shared a database lease between scheduled and page-triggered collection to prevent concurrent scans and excessive retries.
- Reduced the browser polling interval to 30 seconds and API edge-cache lifetime to 15 seconds.
- Production build, TypeScript and Worker syntax checks passed. All 20 targeted tests passed, including stale trade recovery with fresh price samples and concurrent collection.
- Cloudflare reported a successful production deployment. Live API inspection remains blocked for the verification client, so the production cause of the reported delay has not been independently confirmed.

## 2026-10-13 — Trading-volume correction

- Replaced the indexed 24-hour volume with the sum of verified pump.fun buy and sell amounts in the rolling 24-hour window.
- Excluded failed transactions, fee sweeps and out-of-window events; repeated scans do not duplicate volume.
- Added synchronization coverage and freshness checks. An incomplete or stale scan displays a syncing state rather than a misleading partial total.
- Displayed volume in SOL by default. The USD view is explicitly an estimate using the latest available SOL/USD conversion rate.
- Production build, TypeScript and Worker syntax checks passed. All 18 targeted tests passed, including real LABPUP buy/sell fixtures, retry behavior and rolling-window boundaries.
- Cloudflare reported a successful production deployment.

## 2026-10-13 — On-chain SOL pricing and trade history

- Made LABPUP / SOL the default chart view and price metric, retaining the USD option.
- Added direct Solana RPC reads of the verified pump.fun bonding-curve account for SOL pricing before migration.
- Added bounded, retryable recovery of actual pump.fun trade events, including exact timestamps, post-trade prices and transaction links. Fee sweeps and failed transactions are excluded.
- Separated authoritative on-chain SOL history from older index-derived observations. USD prices and trading-volume data continue to use the existing index source.
- Added a refresh when recorded market data is overdue, and improved chart time labels and trade tooltips.
- Production build, TypeScript and Worker syntax checks passed. All 14 targeted market, chart and on-chain tests passed, including an actual LABPUP buy fixture and SQLite tests with an unavailable DEX index.
- Cloudflare reported a successful production deployment. Live browser verification was unavailable.

## 2026-10-12 — USD and SOL chart views

- Added a USD / SOL selector to the price chart, updating its heading, displayed price, axis labels and tooltips.
- Started recording native SOL prices for the selected SOL-quoted trading pair, with independent update times and stale-data handling.
- Preserved existing USD history. SOL history begins with this deployment; older USD observations are not converted using a current exchange rate.
- Production build, TypeScript checks and 11 targeted market and chart tests passed, including real SQLite coverage of history storage and timestamp joins.
- Cloudflare reported a successful production deployment.

## 2026-10-11 — Chart continuity and token links

- Improved chart continuity for sparse price and supply readings: nearby observations use solid lines; longer gaps use dashed connections between recorded observations.
- Kept price histories separate when the selected trading pair changes. Missing readings are not presented as recorded prices.
- Added regression tests for sparse readings, missing and invalid values, and trading-pair changes.
- Added a “View on Rugcheck” link beside the token address copy action, opening the token report in a new tab.
- Production build, TypeScript checks and targeted chart and market tests passed. Cloudflare reported successful production deployments.

## 2026-10-10 — Website deployment and navigation

- Connected the private application repository to Cloudflare Workers Builds for automatic production deployment from the main branch.
- Confirmed the first deployment and successful website opening.
- Renamed the primary trading action to “Trade on pump.fun”.
- Added a public GitHub repository link in the website footer.
- Simplified public repository wording to focus on completed development work.
- Production build and TypeScript checks passed for the website navigation changes. Cloudflare reported successful deployments.

## 2026-10-10 — GitHub development setup

- Established separate private application and public documentation repositories.
- Connected GitHub and verified access to both repositories.
- Added the project overview and initial development roadmap.

This entry records repository setup, not a website release.

## 2026-10-10 — Application source import

- Imported the complete website project into the private application repository, including frontend, Cloudflare Worker, database migrations and source assets.
- Added a dependency lockfile and excluded generated assets and local secret files from version control.
- Updated development documentation to reflect the imported implementation.
- Production build, TypeScript checks and Worker syntax checks passed.
- Local database migrations succeeded. Integration tests remain unverified because the local Worker server encountered an environment error.

No production deployment or production database change was performed.
