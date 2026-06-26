# OVERLOAD

A mobile-first arcade game built for the Cribl conference booth. Players act as a security analyst triaging a stream of falling telemetry events — dismissing safe ones and investigating threats before they hit the bottom. Built as a single self-contained HTML file, playable in any mobile browser with no installation required.

## Gameplay

Events fall as colour-coded cards from the top of the screen. The player uses two buttons at the bottom to act on the card currently in focus (the lowest active card):

- **Dismiss 🗑️** — for safe events (green cards, safe purple cards)
- **Investigate 🔍** — for threats (red cards, threat purple cards)

### Card types

| Colour | Meaning |
|--------|---------|
| 🟢 Green | Always safe — Dismiss |
| 🔴 Red | Always a threat — Investigate |
| 🟣 Purple | Ambiguous — check the icon carefully |
| 🤖 Gold | AI Agent powerup — tap the card directly to collect |

### Lives & scoring

- Correct action: earn points (multiplied by your active combo)
- Threat reaches the bottom or is dismissed by mistake: **lose a life** 💔
- Safe event investigated by mistake: **point deduction** (false alarms waste time)
- Safe event reaches the bottom: **0 points**, no life lost
- Gold card missed: no penalty, card disappears

### Combo system

Consecutive correct player actions build a combo multiplier (up to ×4). Every 5 correct actions in a row increases the multiplier and triggers a visual burst. Every 20 consecutive correct actions restores a lost life (up to the maximum of 3).

### AI Agent powerups

Collecting a gold 🤖 card grants one AI Agent charge (up to 3). Activating an agent auto-protects one column for 15 seconds, automatically swiping every card that falls into it. The agent button deploys one agent per tap; when multiple columns are active you can stack agents across all columns simultaneously.

### Levels

Each level lasts 30 seconds. Cards fall faster and spawn more frequently with each level. The number of simultaneous columns increases at levels 3 and 7.

| Levels | Columns | Fall duration | Spawn interval |
|--------|---------|--------------|----------------|
| 1 | 1 | 3.2s | 1.2s |
| 2 | 1 | 2.6s | 1.0s |
| 3 | 2 | 2.2s | 0.9s |
| 4–6 | 2 | 1.8s | 0.75s |
| 7–9 | 3 | 1.4s | 0.6s |
| 10+ | 3 | 0.95s | 0.45s |

### Agent Orchestration (Level 10+)

At level 10 the game shifts into **Agent Orchestration** mode. Agents auto-deploy the moment a charge is available and a column needs coverage. The player's focus becomes catching every gold card before it falls off the bottom — if fast and accurate enough, all columns stay protected indefinitely. Miss enough gold cards and columns go unprotected, letting threat cards through to drain lives.

## Sound

All sound effects are generated via the Web Audio API — no audio files required. Toggle sound on/off with the **🔊/🔇** button in the top bar during play.

## Deployment

The game is a single file (`index.html`) with no external dependencies or build step. It is deployed via GitHub Pages from the `main` branch root.

```bash
git add index.html
git commit -m "your message"
git push origin main
```

GitHub Pages redeploys automatically on every push.

## Development

To test Agent Orchestration mode without playing through levels 1–9, use the **JUMP TO L10** button on the start screen. This skips the how-to-play screen and starts at level 10 with:
- 3 agent charges in reserve
- All 3 columns already under agent protection, each with a randomised amount of time remaining

## Project structure

```
index.html   — complete game (HTML, CSS, JS in one file)
cribl-logo.png — Cribl wordmark, used on the splash screen
README.md    — this file
```
