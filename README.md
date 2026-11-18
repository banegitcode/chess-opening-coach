# Chess Opening Coach

Learn chess openings by playing them. Pick an opening, pick your side, and the board shows an arrow for the next move, with a plain-English reason for it.

## How it works

1. **Pick an opening.** There are 11, each with 3 to 7 variations:
   - White openings: Italian Game, Ruy Lopez, Queen's Gambit, London System, English Opening
   - Black openings: Sicilian Najdorf, French Defense, Caro-Kann, King's Indian, Scandinavian, Slav
2. **Pick your side.**
   - **Against it:** you play the opponent, and the coach plays the opening. When you have more than one book move, you pick one, and each choice leads to a different variation.
   - **With it:** you play the opening, and the coach plays the opponent. It picks variations you haven't seen yet.
3. **Play the move the arrow shows.** Click a piece and then its square, or click the move in the side panel. A move that isn't in the opening is taken back, and you're shown the right one.

Your progress (variations played per opening) is saved in your browser.

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
