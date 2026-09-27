# Space Invaders

A single-file browser remake of the 1978 arcade game. Open `index.html` in any modern browser; there is no build step and no dependencies beyond two Google Fonts.

## Controls

| Action | Keyboard | Touch |
|--------|----------|-------|
| Move | `←` `→` or `A` `D` | ◀ ▶ buttons |
| Fire | `Space`, `↑` or `W` | Fire button |
| Start / play again | `Enter` | Play button |
| Pause | `P` or `Esc` | — (auto-pauses when the tab loses focus) |
| Sound on/off | `M` | Sound button |

## Rules carried over from the original

- 224×256 playfield with the cabinet's colour bands: red for the mystery ship, green for the laser cannon and shields.
- Invaders are worth 10, 20 and 30 points. The mystery ship's value comes from a fixed table indexed by how many shots you have fired.
- The formation moves one invader per frame, so it speeds up as it thins out.
- Shields and the ground line erode pixel by pixel from both sides' shots, and invaders chew through shields as they descend.
- Extra laser cannon at 1500 points. Each new wave starts lower. If the invaders reach the ground, the game ends whatever your lives.

## Players and the leaderboard

Each player enters a name (1 to 12 letters, numbers, spaces, dots, dashes or underscores) before their first game. The name shows next to the score, and every game counts toward that player's games played and personal best. Use **Switch player** on the title or game-over screen to hand the game to someone else. Names you have used before are suggested as you type.

The leaderboard below the playfield lists the top 10 players by their best game. Where it lives depends on how the page is opened:

- **Published as a claude.ai artifact with the `db` capability:** one shared leaderboard for everyone who opens the page. Each player's best is one document in the artifact's `leaderboard` collection, and it's only rewritten when that player beats it. Posting needs Contributor access or higher. Viewers still see the board, and their own scores are kept in their browser. Rows read from the store are validated and rendered as text only.
- **Opened as a plain file or from any other host:** there is no shared store, so the leaderboard is built from the players saved in this browser, and everyone playing on the same device shares it.

Player stats and the sound preference are kept in `localStorage`. If storage is blocked, as in some private windows, everything still works for the visit but is forgotten when the page closes.

Beating your previous hi-score mid-game plays a short disco-style celebration jingle. It's an original tune, synthesized live with WebAudio, and flashes the hi-score counter.

## Contributing

Contributions are welcome, from bug fixes to new features. The repository's top-level `CONTRIBUTING.md` covers skills, not this game. Use this section instead.

### Run it locally

Open `index.html` in a browser. If your browser restricts `localStorage` on `file://` pages, serve the folder instead:

```sh
cd examples/space-invaders
python3 -m http.server 8000
# then open http://localhost:8000
```

### Ground rules

- **One file, no build step.** All code stays in `index.html`. The only external resources are the two Google Fonts; don't add libraries or bundlers.
- **Keep the original coordinates.** The playfield is 224×256 pixels, as on the arcade cabinet, and every position in the code uses that space. The canvas is scaled up with CSS.
- **Sprites are text.** Each sprite is an array of strings where `#` is a lit pixel. Every row in a sprite must be the same length.
- **Sound is synthesized.** Every effect is generated with WebAudio in the `sfx` module. Don't add audio files or copyrighted music.
- **Keyboard and touch stay in step.** A feature you can reach from the keyboard needs a touch equivalent in the on-screen pad, and the reverse.
- **Respect `prefers-reduced-motion`.** Decorative motion (star twinkle, blinking text) switches off when it is set.

### Finding your way around the code

The script is split into sections marked by comments: backdrop, canvases, sound, game state, rendering, HUD and overlays, input, and the main loop. The game runs at a fixed 60 updates per second in `update()`, and `render()` draws each frame. Game states are `title`, `play`, `dying`, `clear` and `over`.

### Before you open a pull request

- Play at least one full wave with the keyboard, and check that pause, resume and sound on/off work.
- Check the touch controls at phone width, on a real phone or in your browser's device emulation.
- Make sure the browser console shows no errors.
- Fork the repository, work on a branch, and open a pull request against `main`. Say in the description what you changed and how you tested it.
