# 🎰 Classic 3-Reel Slot Machine Game

A responsive 2D slot machine game developed in Unity (Unity 6 / C#) featuring decoupled RNG logic, sequential reel spinning animations, dynamic UI layout anchoring, and a win celebration state.

---

## 🎮 Game Overview

- **Grid Architecture:** 3-reel, 3-row layout with a primary central payline.
- **Starting Bankroll:** Players begin with 1,000 credits.
- **Core Loop:**
  - Players set their bet and press **SPIN**.
  - Credits are immediately deducted and the reels initiate a fast continuous spin.
  - The game evaluates RNG targets and stops each reel sequentially from left to right to build anticipation.
  - Matching symbols along the payline evaluate payout multipliers, update total credits, and trigger a win celebration announcement.

---

## 🚀 Instructions to Run WebGL Build

The compiled WebGL build is included directly in this repository inside the `/Build/WebGL` directory.

Because modern web browsers enforce CORS restrictions on local `file://` protocols for WebAssembly (`.wasm`) files, the build must be served over a local HTTP server:

### Option 1: Python (Quickest)
1. Open a terminal or command prompt and navigate to the build directory:
   ```bash
   cd Build/WebGL

```

2. Start a local server:
```bash
# Python 3.x
python -m http.server 8000

```


3. Open your browser and navigate to:
```text
http://localhost:8000

```



### Option 2: Node.js / `http-server`

```bash
npx http-server Build/WebGL -p 8000

```

Open `http://localhost:8000` in your browser.

---

## ✨ Bonus Features

* **Sequential Reel Braking:** Reels stop with a staggered delay (Reel 1 → Reel 2 → Reel 3) rather than simultaneously, replicating mechanical slot cabinet pacing.
* **Dynamic UI Layout Groups:** The top celebration banner utilizes Unity UI Auto Layout (`HorizontalLayoutGroup` and dynamic text anchoring) to dynamically expand and center win messages without clipping or manual resizing.
* **Viewport Clipping via RectMask2D:** The visual symbol roll is cleanly bounded within the cabinet aperture using non-allocating 2D rect-masking.
* **Audio & Visual Pacing:** Real-time feedback for button states, coin balance updates, and spin lockout while rounds are active.

---

## 🧠 Thought Process & Technical Approach

1. **Separation of Presentation & Simulation:**
* The RNG outcome calculation (`SlotEvaluator` / `GameManager`) is entirely decoupled from the animation presentation (`Reel`).
* The final landing symbols are determined *before* the visual spin completes. This mirrors real-world casino software architecture, preventing client-side desyncs and guaranteeing verifiable outcomes.


2. **Reel Animation System:**
* Rather than relying on physics rigidbodies, the symbols loop using mathematical modulo offsets and coroutine-driven interpolation. This guarantees exact landing coordinates with zero physical drift or settling latency.


3. **Responsive UI Layout:**
* The canvas is structured around a reference resolution of `1920x1080` (Match Height/Width: 0.5).
* Text elements leverage TextMeshPro SDF materials and Auto-Sizing constraints to ensure readability across aspect ratios without overflowing button boundaries.



---

## 📂 Repository Structure

```text
├── Assets/
│   ├── Art/                # Raw sprites, UI frames, buttons, and symbol sheets
│   ├── Scenes/             # Slot machine main gameplay scene
│   ├── Scripts/            # GameManager, Reel, and logic controllers
│   └── TextMesh Pro/       # Typography assets and fonts
├── Build/
│   └── WebGL/              # Compiled HTML5, JS, and WebAssembly binaries
├── ProjectSettings/        # Unity project configurations & build profiles
├── .gitignore              # Standard Unity gitignore excluding Library/Temp
└── README.md

```

```

```
