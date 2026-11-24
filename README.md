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

**Lobby:** each player presses jump to join. Enter or Start begins the match (2–4 players; 1 player gives solo practice). C, Tab, `[` `]`, LB/RB or Select changes the course mode (Grand Tour, Shuffle, or a single course). Backspace removes the last player who joined.

**Anywhere:** F = fullscreen (there is also a button in the top-right corner), M = cycle sound, music off, mute, Esc/P = pause (Q quits to the lobby).

Players collide with each other. You can stand on someone's head, ride on top of them, and get launched when the player under you jumps. A fast charge shoulder-bumps other players, which is handy for knocking them into pits.

## Phone controllers (scan the QR code)
When the game is opened from its web link (for example `https://crush-course.pages.dev`), the lobby shows a **QR code** in the top-left corner. Scan it with a phone to open `controller.html`, which turns the phone into a controller:

- **4P mode:** the screen splits into 4 colour zones (Blue, Red, Green, Yellow), each with ◀ ▶ JUMP, so 4 people can share one phone. Hold the phone sideways for a 2×2 grid; upright gives 4 stacked rows. The ⇅ button flips the top zones for players sitting across a table.
- **1P mode:** one big full-screen controller, so each player can scan with their own phone.
- Tap **JUMP** in a zone to join; that zone's player slot lights up in the lobby. **START** on the phone starts the match or pauses it.
- If the camera can't scan, open `/controller.html` on the phone and type the 5-letter room code shown under the QR code.

The phone connects straight to the game with WebRTC. The free public PeerJS service introduces the two devices (PeerJS and the QR generator load from the jsDelivr CDN). It works best when the phone and PC are on the **same Wi-Fi**. The QR code doesn't appear when `index.html` is opened by double-clicking it; keyboard and gamepads still work offline as before.

## Courses
1. **Meadow Dash**: the warm-up, with spikes, pits, first crushers and a spring wall
2. **Crusher Works**: crusher rows, crusher pits and a spiked-ceiling corridor where you need short hops
3. **Saw Mill**: rail saws, bobbing saws, orbiting saws and a moving platform
4. **Sky Bridges**: crumbling bridges, moving platforms and pillar hops
5. **The Gauntlet**: everything together, over lava

## Deploy to Cloudflare
- **Pages:** connect this repo, leave the framework preset as *None* and the build command empty, and set the output directory to `/`.
- **Workers (static assets):** run `npx wrangler deploy`. It uses `wrangler.jsonc`, and `.assetsignore` keeps non-game files out of the upload.
