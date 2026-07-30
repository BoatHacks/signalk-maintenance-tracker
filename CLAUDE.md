# signalk-maintenance-tracker (fork)

Fork of hoeken/signalk-maintenance-tracker. Work is on the
`inventory-interaction` branch. A PR has been opened back to
hoeken/signalk-maintenance-tracker.

## What this branch adds
Integrates with [[signalk-stowage-mgmt]]'s REST API (exact surface area
documented in the README for API stability). Full inventory integration built:
- `task_consumables` table (schema v2 migration), `ConsumablesRepo`
- `StowageClient` backend module (write path only), distinguishing
  `StowageUnavailableError` vs `StowageRequestError`
- Frontend: `ConsumablesPicker` component, `StockBadge` for worst-case stock
  status, `PlacementAllocator` for split-item location selection on task
  completion
- Frontend reads (picker autocomplete, stock badges) use same-origin browser
  fetches directly to stowage-mgmt
- A `stowageMgmtUrl` config option gates the entire integration

## Side-finding
The upstream maintenance-tracker docs incorrectly describe stowage-mgmt's
error shape as nested. The actual shape is flat: `{error: "..."}`.
