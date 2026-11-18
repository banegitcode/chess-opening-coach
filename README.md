# Chess Opening Coach

Learn chess openings by testing them. Pick an opening, then play the opponent and make any move you like. The coach answers with the best move and explains why, move by move, until the opening is over.

## How it works

1. **Pick an opening.** There are 11 openings, each labeled Beginner, Intermediate or Advanced. The coach plays the opening side:
   - White openings (you play Black): Italian Game, Ruy Lopez, Queen's Gambit, London System, English Opening
   - Black openings (you play White): Sicilian Najdorf, French Defense, Caro-Kann, King's Indian, Scandinavian, Slav
2. **Make any move for the opponent.** Drag a piece, or tap it and then tap a square. Popular moves are listed with the variation each one leads to, but any legal move is allowed.
3. **Read the coach's answer.** A gold arrow shows the best reply, with a plain-English explanation of why it's best. Every move goes into a move-by-move log:
   - **Your moves** are graded Book, Good move, Inaccuracy, Mistake or Blunder, with the better move named when there was one.
   - **The coach's moves** come from opening theory while you stay in the main lines (49 variations), and from the Stockfish engine once you leave them.
4. **It runs until the opening is over:** when a main line ends, or at move 15 once you've left the main lines. Press "Keep going" to continue with the engine.

An evaluation bar shows who is better. "Take back" undoes your last move, and "Best moves: I'll play them" lets you play the coach's moves yourself.

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

A move written as `["SAN", "why"]` carries its explanation. A bare `"SAN"` reuses the explanation already given for that same move in an earlier variation. Lines that share moves merge into one tree automatically. The opening side should have only one book move in each position, because that's the move the coach plays. The opponent can have several.

Move legality comes from [chess.js](https://github.com/jhlywa/chess.js) 0.10.3 and analysis from [Stockfish.js](https://github.com/nmrugg/stockfish.js) 10.0.2, both loaded from cdnjs. Stockfish runs in a Web Worker for about one second per position. If it can't load, a small built-in engine takes over.

## License

MIT
