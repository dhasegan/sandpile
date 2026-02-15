!WARNING: This message is the only thing I wrote myself in this repo: The following README.md is auto-generated while vibe-coding the project. Please use it at your discretion and feel free to edit for clarity, accuracy, and style. It may be totally wrong or contain inaccuracies, so please verify all information before using it as a reference. The README is meant to provide an overview and guide for users, but it may not be perfect. Always refer to the actual code and comments for the most accurate information about the project.

# Self-Organized Criticality Sandpile Game

A competitive two-player browser game that demonstrates the Self-Organized Criticality (SOC) model through the classic Bak-Tang-Wiesenfeld sandpile simulation. Players take turns triggering avalanches and compete for the highest score!

## What is Self-Organized Criticality?

Self-Organized Criticality is a property of dynamical systems that naturally evolve toward a critical state without external tuning. The sandpile model is one of the simplest examples:

- Imagine slowly adding grains of sand to a pile
- Eventually, the pile reaches a critical slope where adding one more grain can trigger an avalanche
- These avalanches follow a power-law distribution - small avalanches are common, large ones are rare
- The system naturally maintains itself at this critical state

This phenomenon appears throughout nature: earthquakes, forest fires, stock market crashes, and even neuronal avalanches in the brain.

## How to Run

### Option 1: Direct File Open
1. Navigate to the project folder
2. Double-click `sandpile.html`
3. The game will open in your default web browser

### Option 2: From Terminal/Command Line
```bash
# On macOS/Linux
open sandpile.html

# On Windows
start sandpile.html

# Or use Python's built-in server for a cleaner experience
python3 -m http.server 8000
# Then open http://localhost:8000/sandpile.html in your browser
```

### Requirements
- Any modern web browser (Chrome, Firefox, Safari, Edge)
- No installation or dependencies required
- Works offline - everything runs in your browser

## How to Play

### Game Mode
This is a two-player competitive game where players take turns trying to create the largest avalanches.

### Objective
Compete against another player by creating larger avalanches. The player with the highest total score at the end wins!

### Initial State
The game starts with a randomly initialized board where each cell contains 1-3 grains of sand. This initialization allows immediate avalanche activity while maintaining realistic near-critical dynamics.

### Rules
1. **Players alternate turns** - Player 1 starts first
2. **On your turn, click any cell** to add one grain of sand
3. **Turn-based locking** - Players cannot click during animations or when it's not their turn
4. **Between turns, X random grains are added** to random locations (X is configurable, default is 2)
   - This simulates continuous energy input, keeping the system near criticality
   - Random avalanches from these additions are tracked separately and displayed in the Random Score
5. Each cell can hold 0-4 grains (though cells with 4+ immediately topple)
6. When a cell reaches **4 grains or more**, it **topples**:
   - The cell loses 4 grains
   - Each of its 4 neighbors (up, down, left, right) gains 1 grain
7. **Avalanches occur** when toppling triggers more toppling in a chain reaction
8. **The active player scores 1 point per topple** in the avalanche they triggered
9. After your move and the random additions, the turn passes to the other player

### Visual Guide
- **Gray (0)**: Empty cell
- **Light yellow (1)**: One grain
- **Yellow (2)**: Two grains
- **Orange (3)**: Three grains - close to toppling!
- **Red (4+)**: Critical - will topple immediately

### Strategy Tips
- Build up multiple cells to 3 grains near each other to set up large avalanches
- Target areas that are already unstable for immediate points
- Watch what your opponent is setting up and decide whether to trigger it or block them
- Sometimes it's better to take smaller avalanches now than let your opponent trigger a large one
- Edge and corner cells have fewer neighbors, making avalanches harder to propagate there
- Consider both offensive (creating big avalanches) and defensive (preventing opponent's avalanches) moves

## Features

- **Two-player competitive mode**: Players take turns and compete for the highest score
- **Step-by-step avalanche visualization**: Watch avalanches propagate wave-by-wave with animated transitions
  - Each toppling wave is displayed with a 150ms delay for clear visual feedback
  - Toppling cells glow with bright red animations and scale effects
- **Turn-based locking**: Grid is disabled during animations and between turns to prevent mis-clicks
- **Dynamic turn indicator**: Color-coded turn display
  - Red background: "Player 1's Turn"
  - Blue background: "Player 2's Turn"
  - Gray background: "Random Adds" (when random grains are being added between turns)
- **Separate player scores**: Each player's score is tracked and displayed independently
- **Random addition tracking**: Random avalanches are tracked separately with their own score and history entries
- **Power-law visualization**: Real-time log-log plot showing avalanche size distribution
  - Stacked bar chart with logarithmic binning: [1-2], [3-4], [5-8], [9-16], [17-32], ..., up to [513-1024]
  - Equal-width bars in log space for proper statistical representation
  - Three color-coded layers: Red (Player 1), Blue (Player 2), Gray (Random additions)
  - Shows contributions from both players and system-driven avalanches
  - A straight downward slope indicates power-law behavior (characteristic of SOC)
  - X-axis: Log₂ scale for avalanche sizes
  - Y-axis: Linear scale for event count (auto-scales with minimum baseline of 10)
- **Continuous driving mechanism**: Random grains are added between turns to simulate natural energy input
  - Configurable rate (0-10 random additions per turn)
  - Default is 2 random additions between each player move
  - Avalanches from random additions are tracked separately in gray with dedicated score
  - Makes the system more faithful to the original Bak-Tang-Wiesenfeld model
- **Weighted random initialization**: Each game starts with cells containing 0-3 grains with probabilities that place the system near criticality
- **Adjustable grid size**: From 5x5 to 30x30 cells
- **Real-time visualization**: Watch avalanches cascade across the grid with smooth animations
- **Score tracking**:
  - Individual scores for Player 1, Player 2, and Random additions
  - Number of moves made
  - Largest avalanche achieved (by any source)
- **Avalanche history**: Track the last 20 avalanches with player/source attribution, positions, and sizes
- **Smooth animations**: Visual feedback when cells topple with glow effects and scaling
- **Responsive design**: Works on desktop and tablet screens

## Game Statistics

The game tracks several key metrics:

1. **Player 1 Score**: Total topples triggered by Player 1
2. **Player 2 Score**: Total topples triggered by Player 2
3. **Random Score**: Total topples triggered by random grain additions
4. **Moves Made**: Total number of turns taken by both players
5. **Largest Avalanche**: The biggest single avalanche created by any source (players or random)

The active player's score box is highlighted with a colored border to indicate whose turn it is. During random additions, the turn indicator changes to gray with "Random Adds" text.

## Scientific Background

This implementation follows the Abelian sandpile model (Bak-Tang-Wiesenfeld model):

- **Discrete cellular automaton** on a 2D grid
- **Local toppling rule**: When height ≥ 4, distribute to 4 neighbors
- **Conservation**: Sand grains at edges fall off the grid
- **Emergent behavior**: System self-organizes to critical state
- **Power-law avalanche distribution**: P(s) ∝ s^(-τ) where s is avalanche size

The model was introduced by Per Bak, Chao Tang, and Kurt Wiesenfeld in 1987 as the first discovered example of self-organized criticality.

### Is This Modified System Still SOC?

**YES!** The random additions between turns actually make this implementation **MORE faithful** to the original BTW model.

Key SOC properties maintained:
- **Continuous driving**: Random grain additions simulate natural energy input (like sand falling on a pile)
- **Fast relaxation**: Avalanches happen instantly when cells reach threshold
- **Self-organization**: System maintains near-critical density without tuning
- **Scale invariance**: Avalanches of all sizes can occur


## Technical Details

- **Pure HTML/CSS/JavaScript**: No frameworks or dependencies
- **Single file**: Everything contained in `sandpile.html`
- **Efficient algorithm**: Uses iterative relaxation to compute avalanches
- **Async/await animations**: Step-by-step avalanche visualization with 150ms delays between toppling waves
- **State management**: Turn-based locking using `isProcessing` and `isRandomPhase` flags
- **Responsive grid**: Adapts to different screen sizes

## Experiments to Try

1. **Random Addition Rate**: Try different rates (0, 1, 2, 5, 10) and observe how it affects:
   - System stability (does it stay near critical or saturate?)
   - Avalanche frequency and size distribution
   - Player strategy (more chaotic with higher rates)
2. **Avalanche Propagation**: Watch the step-by-step animations to observe:
   - How avalanches spread in waves across the grid
   - The difference between small localized avalanches and large cascading ones
   - How boundary effects limit avalanche propagation at edges
3. **Competitive Strategy**: Try different strategies - aggressive (always going for big avalanches) vs defensive (blocking opponent's setups)
4. **Random Initial States**: Each new game starts with a different weighted random distribution (0-3 grains) - observe how different initial conditions affect early game dynamics
5. **Grid Size Effects**: Compare avalanche distributions on small (10x10) vs large (25x25) grids - does grid size favor one strategy over another?
6. **Pattern Recognition**: Notice how certain configurations reliably produce large avalanches
7. **Edge Effects**: Observe how avalanches behave near boundaries vs. grid center
8. **SOC Verification**: Log avalanche sizes over many moves and plot on log-log scale to verify power-law distribution

## License

This project is open source and free to use for educational purposes.

## References

- Bak, P., Tang, C., & Wiesenfeld, K. (1987). "Self-organized criticality: An explanation of the 1/f noise". Physical Review Letters, 59(4), 381.
- Bak, P. (1996). "How Nature Works: The Science of Self-Organized Criticality". Copernicus/Springer-Verlag.

---

Enjoy exploring the fascinating world of self-organized criticality!
