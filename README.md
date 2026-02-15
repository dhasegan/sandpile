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
The game starts with a randomly initialized board where each cell contains 0-3 grains of sand. This means the system begins already close to criticality, allowing you to trigger avalanches more quickly.

### Rules
1. **Players alternate turns** - Player 1 starts first
2. **On your turn, click any cell** to add one grain of sand
3. Each cell can hold 0-4 grains
4. When a cell reaches **4 grains or more**, it **topples**:
   - The cell loses 4 grains
   - Each of its 4 neighbors (up, down, left, right) gains 1 grain
5. **Avalanches occur** when toppling triggers more toppling in a chain reaction
6. **The active player scores 1 point per topple** in the avalanche they triggered
7. After your move, the turn passes to the other player

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
- **Turn indicator**: Clear visual display of whose turn it is
- **Separate player scores**: Each player's score is tracked and displayed independently
- **Random initialization**: Each game starts with cells randomly containing 0-3 grains, placing the system near criticality from the start
- **Adjustable grid size**: From 5x5 to 30x30 cells
- **Real-time visualization**: Watch avalanches cascade across the grid
- **Score tracking**:
  - Individual scores for Player 1 and Player 2
  - Number of moves made
  - Largest avalanche achieved (by either player)
- **Avalanche history**: Track the last 20 avalanches with player attribution, positions, and sizes
- **Smooth animations**: Visual feedback when cells topple
- **Responsive design**: Works on desktop and tablet screens

## Game Statistics

The game tracks several key metrics:

1. **Player 1 Score**: Total topples triggered by Player 1
2. **Player 2 Score**: Total topples triggered by Player 2
3. **Moves Made**: Total number of turns taken by both players
4. **Largest Avalanche**: The biggest single avalanche created by either player

The active player's score box is highlighted with a colored border to indicate whose turn it is.

## Scientific Background

This implementation follows the Abelian sandpile model (Bak-Tang-Wiesenfeld model):

- **Discrete cellular automaton** on a 2D grid
- **Local toppling rule**: When height ≥ 4, distribute to 4 neighbors
- **Conservation**: Sand grains at edges fall off the grid
- **Emergent behavior**: System self-organizes to critical state
- **Power-law avalanche distribution**: P(s) ∝ s^(-τ) where s is avalanche size

The model was introduced by Per Bak, Chao Tang, and Kurt Wiesenfeld in 1987 as the first discovered example of self-organized criticality.

## Technical Details

- **Pure HTML/CSS/JavaScript**: No frameworks or dependencies
- **Single file**: Everything contained in `sandpile.html`
- **Efficient algorithm**: Uses iterative relaxation to compute avalanches
- **Responsive grid**: Adapts to different screen sizes

## Experiments to Try

1. **Competitive Strategy**: Try different strategies - aggressive (always going for big avalanches) vs defensive (blocking opponent's setups)
2. **Random Initial States**: Each new game starts with a different random configuration - observe how different initial conditions affect avalanche behavior
3. **Grid Size Effects**: Compare avalanche distributions on small (10x10) vs large (25x25) grids - does grid size favor one strategy over another?
4. **Pattern Recognition**: Notice how certain configurations reliably produce large avalanches
5. **Edge Effects**: Observe how avalanches behave near boundaries vs. grid center

## License

This project is open source and free to use for educational purposes.

## References

- Bak, P., Tang, C., & Wiesenfeld, K. (1987). "Self-organized criticality: An explanation of the 1/f noise". Physical Review Letters, 59(4), 381.
- Bak, P. (1996). "How Nature Works: The Science of Self-Organized Criticality". Copernicus/Springer-Verlag.

---

Enjoy exploring the fascinating world of self-organized criticality!
