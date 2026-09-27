# Space Invaders

A single-file browser remake of the 1978 arcade game. Open `index.html` in any modern browser; there is no build step and no dependencies beyond two Google Fonts.

> **About this project:** this game is one of a [series of experiments](../README.md) by Thomas to evaluate the capabilities of frontier large language models (LLMs). The code, tests and documentation were produced with an AI coding agent working from Thomas's requests.

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

## Players and their game history

Each player enters a name (1 to 12 letters, numbers, spaces, dots, dashes or underscores) before their first game. The name shows next to the score as `SCORE<NAME>`, and the HI-SCORE counter shows that player's own best. Use **Switch player** on the title or game-over screen to hand the game to someone else. Names you have used before are suggested as you type.

Below the playfield, each player has their own record: games played, their best score and wave, and their last 10 games, which you can sort by **Latest** or **Best**. The last 50 games per player are stored. The game-over screen says which game number it was and how it compares with the player's best.

Players and the sound preference are kept in `localStorage`, so each browser keeps its own records. They aren't shared between devices or with other people. If storage is blocked, as in some private windows, everything still works for the visit but is forgotten when the page closes.

Beating your own previous best mid-game plays a short disco-style celebration jingle, an original tune synthesized live with WebAudio. It also shows a "New personal best!" banner and flashes the hi-score counter.

## Contributing

Contributions are welcome, from bug fixes to new features.

### Step by step

1. **Fork the repository.** Open [kernpartner/games](https://github.com/kernpartner/games) and select **Fork** at the top right. You get your own copy that you can push to.
2. **Clone your fork and create a branch:**

   ```sh
   git clone https://github.com/<your-username>/games.git
   cd games/space-invaders
   git checkout -b my-change
   ```

3. **Run the game.** Open `index.html` in a browser. If your browser restricts `localStorage` on `file://` pages, serve the folder instead:

   ```sh
   python3 -m http.server 8000
   # then open http://localhost:8000
   ```

4. **Make your change.** Follow the ground rules below, then work through [Before you open a pull request](#before-you-open-a-pull-request).
5. **Commit and push to your fork:**

   ```sh
   git add .
   git commit -m "Say what you changed"
   git push -u origin my-change
   ```

6. **Open a pull request.** Your fork on GitHub shows a **Compare & pull request** button. Target `kernpartner/games` on `main`, and say in the description what you changed and how you tested it.

For a small fix you can skip the clone: open the file on GitHub and select the pencil icon. GitHub forks the repository and opens the pull request for you.

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

## Notes

A fan remake for fun. Space Invaders is a trademark of Taito; this project is not affiliated with or endorsed by them.

## How the original was made

Space Invaders was created by Tomohiro Nishikado at Taito and released in 1978. By his own accounts, the game itself was quick to write: about 3 to 4 months of programming. Most of the effort went into what came before it. Taito had no microcomputer development system, so Nishikado built the hardware around an Intel 8080 and his own development tools largely by himself, down to making his own RAM to hold instructions and programming each ROM chip separately.

His interviews give slightly different totals. In one, setting up the development environment took about 6 months before the programming started. In a 2017 interview he said the whole project took "close to one and a half years, and half of that time was used to develop the hardware and development tools." So building the tools took about half the time or a little more, not the overwhelming majority that is sometimes claimed.

Sources:

- [Tomohiro Nishikado – 2000 Developer Interview (shmuplations.com)](https://shmuplations.com/nishikado/)
- [Space Invaders – 30th Anniversary Interview (shmuplations.com)](https://shmuplations.com/spaceinvaders/)
- [How Tomohiro Nishikado created Space Invaders 46 years ago (GamesBeat)](https://gamesbeat.com/how-tomohiro-nishikado-created-space-invaders-46-years-ago-exclusive-interview/)
- [Tomohiro Nishikado Revisits His 1978 Game Space Invaders (The New Stack)](https://thenewstack.io/tomohiro-nishikado-revisits-his-1978-game-space-invaders/)
