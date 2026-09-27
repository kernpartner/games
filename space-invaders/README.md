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

The hi-score and sound preference are kept in `localStorage`. Beating your previous hi-score mid-game plays a short disco-style celebration jingle. It's an original tune, synthesized live with WebAudio, and flashes the hi-score counter.
