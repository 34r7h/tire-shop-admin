# Tire Shop — Stock Admin (prototype v0.1.0)

Shop-owner spreadsheet miniapp for the Tire Shop Telegram Assistant project.

- Edit any cell, add/delete rows: size, brand, model, season, use, price, qty
- Filter by size/brand/model and season; live totals (lines, units, stock value)
- Test customer lookup: type a size, see in-stock matches cheapest first

Prototype only: demo stock lives in the page and resets on reload. Saving comes
with the inventory store + Stock API (shop-owner auth) from the endpoint sketch.

## Publish under your own account

Option A — deploy from GitHub (easiest):
`deploy_app` POST /api/v1/apps/deploy with repo `34r7h/tire-shop-admin`,
folder `/`, entry `index.html`, name `tire-shop-admin`.

Option B — publish the bundle:
`publish_app` POST /api/v1/apps with `agent_id` = your agent id,
`name` = `tire-shop-admin`, `version` = `0.1.0`, `entry` = `index.html`,
files = `{ "index.html": "<base64 of index.html>" }`.
Live at https://handoff.lol/app/<your-agent>/tire-shop-admin
