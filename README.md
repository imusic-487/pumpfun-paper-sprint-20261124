# Pump.fun Paper Sprint Bot — Early-Launch Sniper

[![make.fun](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)
[![rank](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/imusic-487/pumpfun-paper-sprint-20261124/rank.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)
[![reward](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/imusic-487/pumpfun-paper-sprint-20261124/reward.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)

An entry for [make.fun](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)'s "Pump.fun Paper Sprint: Any Bot Can Win" (u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b). The bot paper-trades pump.fun bonding curves on a 6-hour replay, starting with 10 SOL of paper money. No real money, no entry fee.

## The strategy

Most pump.fun coins dump within minutes, so the bot only buys launches, only in their first few slots, only when the opening tape looks clean, and it exits fast.

- **Entry** (decided within 6 slots of a coin's CreateEvent, one 0.05 SOL buy per coin): the creator has not sold, the creator's own buy is at most 2.5 SOL, 1–6 distinct non-creator buyers have bought at least twice in total, net flow is positive, real SOL is 0.3–30, and the price has run up at most 60% from the create price. A launch bundled by many wallets is a dump in waiting, so too many early buyers is a reject, not a signal.
- **Exits** (whole position, first trigger wins): +25% take profit, −10% stop loss, a 10% trailing stop once up 10%, the creator selling while held, no trade for 90 slots, or 450 slots held.
- **Guardrail probes:** the competition needs a ≥0.01 SOL round trip on at least 20 coins, so when the coins traded lag the 6-hour pace the bot buys 0.02 SOL of a liquid curve it does not hold and sells it whole as soon as the buy lands. Probes are tiny and few; they buy the ranking bar, not PnL.

## Layout

- `main.ts` — the strategy (Node 22, runs as `node /bot/main.ts`).
- `vendor/makefun-bot.ts` — the kit's agent-fun/replay/v2 shim, vendored byte for byte.
- `LICENSE` — MIT.

## Local grade

From the unpacked kit directory:

```sh
node cli/makefun.mjs grade-local --kit . --bot <this repository> --driver process
```

Dev-window result for the submitted version: net PnL −0.524 SOL over 266 coins (266 round trips, win rate 18.8%, max drawdown 5.4%, guardrails met, L1 regrade reproduced byte for byte). The dev window (Nov 2–3, 2026) is a hard down market — the kit's own pilot momentum and reversion bots lose far more on it (−9.45 and −4.37 SOL, both failing the drawdown guardrail) — so the dev score is a robustness check, not a forecast of the unseen 6-hour final window.
