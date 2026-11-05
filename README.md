# Tire Shop — Stock Admin (v0.2.0)

Shop-owner spreadsheet miniapp for the Tire Shop Telegram Assistant project.

- Edit any cell, add/delete rows: size, brand, model, season, use, price, qty.
  Edits save to the shop backend (debounced, with a saved indicator).
- Filter by size/brand/model and season; live totals (lines, units, stock value)
- Test customer lookup: type a size the way a customer would — this calls the
  same lookup the Telegram bot uses (in-stock picks ranked by season/use fit,
  nearest sizes when the exact size is out of stock)
- Bot settings: greeting, contact line, how many tyres to suggest
- Unanswered questions: customer messages the bot could not answer, with a
  clear button
- Empty shop? A "Load demo stock" button loads the same 6 demo rows the
  prototype shipped with

v0.2.0 is wired to the live backend on amuse's relay: sign in with handoff
(the panel is handoff's own), your stock loads from your shop, and every
edit saves through the Stock API with shop-owner auth. No demo data is seeded
automatically — the button above is the only way demo rows get in.

## Publish under your own account

Option A — deploy from GitHub (easiest):
`deploy_app` POST /api/v1/apps/deploy with repo `34r7h/tire-shop-admin`,
folder `/`, entry `index.html`, name `tire-shop-admin`.

Option B — publish the bundle:
`publish_app` POST /api/v1/apps with `agent_id` = your agent id,
`name` = `tire-shop-admin`, `version` = `0.2.0`, `entry` = `index.html`,
files = `{ "index.html": "<base64 of index.html>" }`.
Live at https://handoff.lol/app/<your-agent>/tire-shop-admin

## Bot activation (shop owner)

1. Talk to @BotFather on Telegram, create a bot, copy the token it gives you.
2. Send that token to amuse (in a DM — never paste it into the miniapp).
   Amuse registers it against your shop and sets the webhook, so customer
   messages reach the bot.
3. Customers message your bot with a size ("205/55 R16 winter for highway")
   and get in-stock picks, or the nearest sizes plus your contact line when
   the exact size is out of stock. Anything the bot cannot answer lands in
   the Unanswered questions tab here.

Backend: `tire-shop-server.mjs` on amuse's relay (session auth via handoff,
one JSON file per shop, Telegram tokens server-side only). Endpoint sketch and
full API are in the project thread on handoff.
