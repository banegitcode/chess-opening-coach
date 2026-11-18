# Chess Opening Coach

Learn chess openings by playing them. Pick an opening, pick your side, and the board shows an arrow for the next move, with a plain-English reason for it.

## How it works

1. **Choose an opening.** Each card shows its level (Beginner, Intermediate or Advanced) and how many of its variations you've played. There are 11 openings with 49 variations in all:
   - White openings: Italian Game, Ruy Lopez, Queen's Gambit, London System, English Opening
   - Black openings: Sicilian Najdorf, French Defense, Caro-Kann, King's Indian, Scandinavian, Slav
2. **Choose a side.** Play as the side that uses the opening, or as the opponent to learn how to face it. "Switch sides" changes this at any time.
3. **Follow the arrows.** Gold arrows are your moves and blue arrows are the opponent's. The status line above the board always says what to do, and the coach panel explains why each move is played.

- **Moving pieces:** drag a piece, or tap it and then tap a square. You can also press "Play it for me".
- **Choosing your own variation:** when you have several good moves, each one is listed with the variation it leads to. Hover over an option to highlight its arrow.
- **Choosing the opponent's reply:** with "Opponent's replies: I pick" turned on, you pick the opponent's move whenever it has more than one variation. Use the buttons or move the piece on the board. Switch to "Coach picks" and the coach chooses for you, preferring variations you haven't seen yet.
- **Mistakes:** a move that isn't in the opening is taken back, and the arrow stays up. "Undo my move" steps back one of your moves.

Your progress is saved in your browser.

## Run it

The whole app is a single file, `index.html`, with no build step. Open it in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

Then go to http://localhost:8000.

To host it on GitHub Pages, go to the repository's **Settings → Pages** and deploy from the `main` branch, root folder.

## Adding an opening or variation

Openings live in the `OPENINGS` array in `index.html`. Each variation is a full move list from move 1:

```js
{ name: "Two Knights Defense", note: "Shown when the line is finished.",
  m: ["e4", "e5", "Nf3", "Nc6", "Bc4",
      ["Nf6", "Black attacks e4 instead of copying White."],
      ...] }
```

A move written as `["SAN", "why"]` carries its explanation. A bare `"SAN"` reuses the explanation already given for that same move in an earlier variation. Lines that share moves merge into one tree automatically. The side that plays the opening should have only one book move in each position. The opponent can have several.

Move legality comes from [chess.js](https://github.com/jhlywa/chess.js) 0.10.3, loaded from cdnjs.

## License

MIT
