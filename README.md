# Crush Course

A 4-player local multiplayer trap-race platformer. The game is one `index.html` with no build step and no asset files, plus an optional `controller.html` that lets phones act as controllers. Graphics are drawn on `<canvas>` and sound effects come from the Web Audio API.

The camera scrolls right and slowly speeds up. Players race through crushers, saw blades, spikes, pits, crumbling bridges and moving platforms. Fall off the left edge and you're **BLOCKED OUT**. You win a round by reaching the flag first or by being the last player alive. The first player to **5 round wins** takes the match.

## Play locally
Double-click `index.html`. It opens in Chrome; no server is needed.

## Controls
| Player | Left | Right | Jump |
|---|---|---|---|
| P1 Blue | A | D | W |
| P2 Red | ← | → | ↑ |
| P3 Green | J | L | I |
| P4 Yellow | Numpad 4 | Numpad 6 | Numpad 8 |

Gamepads (up to 4) use the left stick or D-pad to move and **A** (the bottom button) to jump. Start begins the match or pauses; B leaves the lobby.

**Lobby:** each keyboard or gamepad player presses jump to join (phones pick a colour on the phone). Enter or Start begins the match (2–4 players; 1 player gives solo practice). C, Tab, `[` `]`, LB/RB or Select changes the course mode (Grand Tour, Shuffle, or a single course). Backspace removes the last player who joined.

**Anywhere:** F = fullscreen (there is also a button in the top-right corner), M = cycle sound, music off, mute, Esc/P = pause (Q quits to the lobby).

Players collide with each other. You can stand on someone's head, ride on top of them, and get launched when the player under you jumps. A fast charge shoulder-bumps other players, which is handy for knocking them into pits.

## Phone controllers (scan the QR code)
Each phone is one player. Four players can be 4 phones, or any mix such as 1 keyboard + 3 phones, or 2 gamepads + 2 phones.

When the game is opened from its web link (for example `https://scottish-7qd.pages.dev`), the lobby shows a **QR code** in the top-left corner. On each phone:
1. Scan the QR code. It opens `controller.html`.
2. Type your **name** (the phone remembers it).
3. Tap a free colour (Blue, Red, Green or Yellow). Colours other players already have are greyed out and show their names.
4. The phone becomes one big controller with ◀ ▶ JUMP. **START** starts the match or pauses it; **Change** (lobby only) lets you pick another colour or rename.

If a phone reloads or drops out mid-match, it gets its player back when it reconnects. If the camera can't scan, open `/controller.html` and type the 5-letter room code shown under the QR code.

The phone connects straight to the game with WebRTC. The free public PeerJS service introduces the two devices (PeerJS and the QR generator load from the jsDelivr CDN). It works best when the phones and the PC are on the **same Wi-Fi**. The QR code doesn't appear when `index.html` is opened by double-clicking it; keyboard and gamepads still work offline.

## Player names
There's no backend, so each device stores names locally:
- **Phone players** type their name on the phone. It's saved on that phone and sent to the game when it connects.
- **Keyboard/gamepad players** click their player card in the lobby and type a name. It's saved in that browser.

Names appear above each character, on the HUD, in "BLOCKED OUT!" pop-ups, on round and match win banners, and on the scoreboard.

## Courses
1. **Meadow Dash**: the warm-up, with spikes, pits, first crushers and a spring wall
2. **Crusher Works**: crusher rows, crusher pits and a spiked-ceiling corridor where you need short hops
3. **Saw Mill**: rail saws, bobbing saws, orbiting saws and a moving platform
4. **Sky Bridges**: crumbling bridges, moving platforms and pillar hops
5. **The Gauntlet**: everything together, over lava
6. **Frostbite Peaks**: snowy climbs over spike beds, ice bridges and a spring launch over a chasm
7. **Dune Sprint**: a fast desert dash with rail saws, pits and pillar hops
8. **Steel Foundry**: crusher gauntlets, crusher pits and a spiked ceiling
9. **Haunted Hollow**: orbiting saws, crumbling bridges and toxic goo
10. **Final Ascent**: the fastest course, with every trap in the game

Course modes in the lobby: **Grand Tour** (all 10 in order), **Starter Tour** (1–5), **Pro Tour** (6–10), **Shuffle**, or any single course.

## Deploy to Cloudflare
- **Pages:** connect this repo, leave the framework preset as *None* and the build command empty, and set the output directory to `/`.
- **Workers (static assets):** run `npx wrangler deploy`. It uses `wrangler.jsonc`, and `.assetsignore` keeps non-game files out of the upload.
