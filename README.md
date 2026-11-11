# Game Night

Three friends, six co-op games, one pick. Browse the games, rank them in a tier list from your own device, and watch the group result update live.

**Play:** https://naulio.github.io/game-night/

## How it works

1. Open the link. You get a fresh room, and its code is in the URL.
2. Click **Copy invite link** (bottom right) and send it to the other two.
3. Each person picks a seat (Player 1, 2 or 3) and optionally a name.
4. Rank the six games: drag cards into S–D, or press **S A B C D** on a slide.
5. When all three lists are in, open **See the group result**.

- **Browse together** (on by default) keeps everyone on the same slide and opens or closes the results screen for the whole room. Turn it off to read at your own pace.
- Everyone sees every list live, and anyone can switch to another player's list to view or edit it.
- Points: S 5, A 4, B 3, C 2, D 1, unranked 0. The highest total wins. Ties go to the game with the better lowest vote, then the most S votes.

## Games

Void Crew · GTFO · Project Zomboid · PlateUp! · Valheim · Abiotic Factor

Facts, prices (EUR/USD) and disk requirements come from each game's Steam store page and the developers' Steam announcements, checked 11 Nov 2026. Prices change with sales and region.

## Tech

- A single static `index.html` (HTML, CSS, vanilla JS), served by GitHub Pages. No build step.
- Live rooms use a small built-in MQTT client over WebSocket, talking to the free public broker `broker.emqx.io`. Each player's list is a retained message, so late joiners get the current state instantly. Presence uses MQTT last-will messages.
- Each browser also keeps a copy in `localStorage`, so votes survive refreshes and dropped connections, and re-sync when the connection returns.
- The public broker has no access control. Anyone with a room link can read and change that room, so keep player names casual.
- To use a different broker, add `&broker=wss://your-broker/mqtt` to the URL.
