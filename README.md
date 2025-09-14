# Retro 3-Reel Slot Machine

A retro-styled HTML5/JavaScript slot machine game with authentic physical reel simulation, 9 paylines, and classic arcade aesthetics. Built with pure JavaScript - no build tools required!

## Quick Start

1. **Run the game**: Simply open `index.html` in a modern web browser
2. **Play**: Click SPIN or press SPACE to play
3. **Adjust bet**: Use BET +/- buttons or LEFT/RIGHT arrow keys (1-5 credits)
4. **Change themes**: Click THEME button or press T to cycle through 5 visual themes
5. **Mute audio**: Click SOUND button or press M

## Authentic Slot Machine Experience

- **Physical Reel Simulation**: Real spinning reels with fixed symbol sequences
- **Sequential Stopping**: Left reel stops first, then middle, then right (like real slots)
- **Smooth Animation**: Symbols scroll naturally with motion blur effects
- **9 Paylines**: Complete winning combinations across rows, columns, and diagonals
- **5 Visual Themes**: Cycle through Retro Green, Neon Pink, Cyber Blue, Gold Rush, and Fire Red

## Game Features

### Authentic Slot Machine Physics
- **Physical Reels**: Each reel has 20 symbols in a fixed sequence that actually spins
- **Real Momentum**: Reels spin at different speeds and decelerate naturally
- **Sequential Stopping**: Classic slot timing - left stops first, building suspense
- **Visible Symbol Flow**: You can see symbols approaching and feel "near misses"

### Game Mechanics
- **3×3 grid** with 9 paylines (rows, columns, diagonals, V-shape)
- **6 retro symbols**: Cherry 🍒, Lemon 🍋, Diamond 💎, Bell 🔔, Star ★, Seven 7
- **Variable payouts**: SEVEN (50), BELL (40), STAR (30), DIAMOND (20), CHERRY (10), LEMON (5)
- **Betting system**: 1-5 credits per spin with payout multipliers

### Visual Themes
- **🟢 Retro Green**: Classic terminal/matrix aesthetic (default)
- **🟣 Neon Pink**: Cyberpunk synthwave vibes
- **🔵 Cyber Blue**: Futuristic tech interface
- **🟡 Gold Rush**: Luxurious casino glamour
- **🔴 Fire Red**: High-energy racing/gaming style

### Controls & Accessibility
- **Mouse**: Click buttons for all actions
- **Keyboard**: SPACE=spin, arrows=bet, T=theme, M=mute, TAB=navigate
- **Audio**: Generated spin/win sounds with mute toggle
- **Visual feedback**: Winning paylines highlighted with animations
- **Theme switching**: Smooth animated transitions between 5 color schemes

## Project Structure

```
/
├── index.html                 # Game shell, loads main.js
├── README.md                  # This file
└── src/
    ├── main.js                # App bootstrap & initialization
    ├── game/
    │   ├── GameEngine.js      # State machine & game orchestration
    │   ├── ReelController.js  # Reel spinning & symbol generation
    │   ├── PaylineEvaluator.js# Win detection & payout calculation
    │   └── RNG.js             # Random number generator (seedable)
    ├── state/
    │   └── Store.js           # Reactive state management
    ├── ui/
    │   ├── Renderer.js        # Canvas rendering & animations
    │   ├── Controls.js        # Input handling & accessibility
    │   ├── Audio.js           # Sound effects management
    │   └── Theme.js           # Retro styling & palettes
    ├── config/
    │   ├── paylines.js        # 9 payline definitions
    │   ├── symbols.js         # Symbol data & weights
    │   └── paytable.js        # Payout rules
    └── utils/
        ├── dom.js             # DOM helper functions
        └── math.js            # Animation & math utilities
```

## Configuration & Extension

### Adding New Symbols

Edit `src/config/symbols.js`:

```javascript
export const SYMBOLS = [
    {
        name: 'DIAMOND',
        displayChar: '💎',
        weight: 3,        // Lower = rarer
        colorIndex: 6     // Color palette index
    },
    // ... existing symbols
];
```

### Modifying Payouts

Edit `src/config/paytable.js`:

```javascript
export const PAYTABLE = {
    DIAMOND: { 3: 100 },  // 3 diamonds = 100 credits
    SEVEN:   { 3: 50 },   // 3 sevens = 50 credits
    // ... other payouts
};
```

### Customizing Paylines

Edit `src/config/paylines.js`:

```javascript
// Grid positions (0-8, row-major):
// 0 1 2
// 3 4 5
// 6 7 8

export const PAYLINES = [
    [0, 1, 2],  // Top row
    [0, 4, 8],  // Diagonal
    // ... add your custom patterns
];
```

## Testing & Debugging

### Console Commands

Open browser dev tools and use these debug functions:

```javascript
// Set deterministic seed for testing
window.__debug.setSeed(12345);

// Force specific grid result (symbol indices)
window.__debug.forceGrid([0, 0, 0, 1, 1, 1, 2, 2, 2]);

// Check current game state
window.__debug.getState();
```

### Unit Tests

The codebase includes validation for core game logic:

1. **PaylineEvaluator**: Test win detection with known grids
2. **RNG**: Verify deterministic behavior when seeded
3. **Store**: Check state management and subscriptions

Example test in console:

```javascript
// Test PaylineEvaluator
import { PaylineEvaluator } from './src/game/PaylineEvaluator.js';
import { SYMBOLS } from './src/config/symbols.js';

// Create test grid: 3 cherries on top row
const testGrid = [
    SYMBOLS[0], SYMBOLS[0], SYMBOLS[0],  // Top row: all cherries
    SYMBOLS[1], SYMBOLS[2], SYMBOLS[3],  // Mixed middle
    SYMBOLS[4], SYMBOLS[5], SYMBOLS[1]   // Mixed bottom
];

const wins = PaylineEvaluator.evaluateGrid(testGrid);
console.log('Expected 1 win (top row):', wins);
```

## Architecture

### State Machine (GameEngine)
```
IDLE → SPINNING → STOPPING → EVALUATING → PAYOUT → IDLE
```

### Data Flow
1. **User Input** → Controls → GameEngine
2. **Game Logic** → Store (state updates)
3. **State Changes** → Renderer (visual updates)
4. **Win Detection** → PaylineEvaluator → Audio/Visual feedback

### Modularity
- **Config-driven**: Easy to modify symbols, paylines, payouts
- **Reactive**: UI automatically updates when state changes  
- **Extensible**: Add new features by extending existing classes
- **Testable**: Deterministic RNG and pure functions

## Browser Compatibility

- **Modern browsers** with ES6 module support
- **Canvas 2D** rendering (widely supported)
- **Web Audio API** for sound (graceful fallback)
- **No external dependencies** - works offline

## Performance

- **60fps animations** on typical hardware
- **Efficient rendering** with canvas optimization
- **Minimal DOM manipulation** for smooth gameplay
- **Small footprint** (~15KB total, no external assets)

## Accessibility

- **Keyboard navigation** with visible focus states
- **ARIA labels** on interactive elements
- **Screen reader friendly** with live regions for win announcements
- **High contrast** retro color scheme

## License

Open source - modify and extend as needed!

---

**Enjoy the retro gaming experience!** 🎰