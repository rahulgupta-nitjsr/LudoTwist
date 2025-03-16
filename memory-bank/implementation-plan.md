# Implementation Plan for Ludotwist - Phase 1 (Basic Ludo Game)

This document provides a detailed, step-by-step implementation plan for building the base version of "Ludotwist," a web-based Ludo game as outlined in Phase 1 of the Game Design Document (GDD). The plan is tailored for AI developers, ensuring each step is small, specific, and includes a test to validate correct implementation. The focus is on core mechanics and features for single-player (against AI) and local multiplayer modes, using the specified tech stack (React front-end) and adhering to Cursor rules. Future features like online multiplayer are excluded from this plan.

---

## Step 1: Set Up the React Project

**Instruction:**
- Use Create React App (CRA) to initialize a new React project by running `npx create-react-app ludotwist --template typescript` in the terminal.
- Install dependencies: `npm install styled-components react-router-dom @types/styled-components @types/react-router-dom jest @testing-library/react @testing-library/jest-dom`.
- Create a modular directory structure in `src/`:
  - `src/components/` for UI components.
  - `src/game/` for game logic.
  - `src/contexts/` for state management.
  - `src/hooks/` for custom hooks.
  - `src/utils/` for utility functions.
  - `src/assets/` for static assets.
  - `src/types/` for TypeScript interfaces and types.
  - `src/tests/` for test files.

**Test:**
- Run `npm start` and confirm the development server starts, displaying the default React page in the browser.
- Verify the directory structure matches the layout above by inspecting the `src/` folder.

---

## Step 2: Build the Main Menu UI

**Instruction:**
- Create `src/components/MainMenu.tsx`.
- Add buttons for "Play," "Settings," and "Help/Rules" using `styled-components` for styling (e.g., colored buttons with hover effects).
- Set up basic routing with `react-router-dom`:
  - Wrap the app in `BrowserRouter` in `src/index.tsx`.
  - Define routes in `src/App.tsx` for Main Menu, Game Screen, Settings, and Help (use placeholders for non-menu screens).
- Ensure the UI is responsive with appropriate breakpoints for mobile (< 768px) and desktop (≥ 768px).

**Test:**
- Write a Jest test using React Testing Library to verify the Main Menu renders with all buttons.
- Load the app and ensure the Main Menu displays with all three buttons visible and styled.
- Click each button and confirm navigation occurs (e.g., "Settings" leads to a blank Settings page).
- Test responsiveness by resizing the browser window to mobile dimensions.

---

## Step 3: Design the Game Board UI

**Instruction:**
- Create `src/components/Board.tsx`.
- Use CSS Grid to render the Ludo board based on standard Ludo board dimensions and layout:
  - 15x15 grid for the main board structure.
  - 52 main path spaces in a loop.
  - Four colored starting areas (Red, Blue, Green, Yellow) with 4 spaces each.
  - Four home stretches (5 spaces each) leading to a central home triangle.
- Style with `styled-components` for responsiveness (e.g., scale based on screen size).
- Mark safe spaces visually (e.g., with a star icon).
- Use standard Ludo colors:
  - Red: #FF0000
  - Blue: #0000FF
  - Green: #00FF00
  - Yellow: #FFFF00
  - Board background: #F5F5F5
  - Safe spaces: #FFD700 (gold)

**Test:**
- Write a Jest test to verify the Board component renders correctly.
- Render the `Board` component and confirm all spaces (main path, starting areas, home stretches, home triangle) are visible and correctly positioned.
- Resize the browser window to verify the board scales proportionally without breaking on both mobile and desktop viewports.

---

## Step 4: Implement the Dice UI

**Instruction:**
- Create `src/components/Dice.tsx`.
- Display a six-sided die graphic or number with simple 3D styling.
- Add a "Roll" button styled with `styled-components`.
- Implement a dice rolling animation (e.g., spinning or tumbling effect for 0.5-1 second).
- Simulate a roll by showing a random number (1–6) when the button is clicked.

**Test:**
- Write a Jest test to verify the Dice component renders and responds to clicks.
- Load the `Dice` component and confirm the die and "Roll" button appear.
- Click "Roll" and ensure a number between 1 and 6 displays with the animation.

---

## Step 5: Add Player Indicators

**Instruction:**
- Create `src/components/PlayerIndicator.tsx`.
- Display indicators for up to 4 players (e.g., colored boxes or icons for Red, Blue, Green, Yellow).
- Highlight the active player (e.g., with a glowing border or arrow).
- Add a timer display showing the 5-second countdown for each player's turn.
- Include player names or labels (e.g., "Player 1", "AI (Medium)").

**Test:**
- Write a Jest test to verify the PlayerIndicator highlights the correct player.
- Render the component with mock player data and verify all indicators appear with correct colors.
- Switch the active player manually and confirm the highlight updates accordingly.
- Verify the timer counts down from 5 seconds.

---

## Step 6: Create Settings and Help UI

**Instruction:**
- Create `src/components/Settings.tsx` and `src/components/Help.tsx`.
- In `Settings`, add:
  - Sound toggle switch.
  - AI difficulty selection (Easy, Medium, Hard).
  - Animation toggle.
  - Turn timer toggle.
- In `Help`, add static text summarizing Ludo rules (e.g., "Roll a 6 to start, move all pieces to the home triangle to win").
- Include a section about special rules (e.g., 3 consecutive sixes rule).
- Link both to the Main Menu via routes.

**Test:**
- Write Jest tests for both components.
- Navigate to Settings and Help from the Main Menu; ensure each loads correctly.
- Toggle each setting and confirm the UI updates.
- Verify all rule text is readable on both mobile and desktop viewports.

---

## Step 7: Define Board Logic

**Instruction:**
- Create `src/game/Board.ts` and `src/types/BoardTypes.ts`.
- Define TypeScript interfaces for board spaces and positions.
- Represent the board as data:
  - Array of 52 main path spaces with properties (e.g., `isSafe` for starred spaces).
  - Four starting areas (4 spaces each) and home stretches (5 spaces each).
  - Home triangle as a single endpoint per player.
- Export a function to access space details by index or player.
- Include utility functions for calculating valid moves and paths.

**Test:**
- Write Jest tests to verify:
  - The main path has 52 spaces.
  - Safe spaces are marked at correct positions (e.g., every 8th space).
  - Path calculations work correctly for each player color.

---

## Step 8: Model Players and Pieces

**Instruction:**
- Create `src/game/Player.ts`, `src/game/Piece.ts`, and corresponding type files.
- In `Player.ts`, define properties: 
  - `color` (Red, Blue, Green, Yellow)
  - `pieces` (array of 4 pieces)
  - `isAI` (boolean)
  - `difficulty` (Easy, Medium, Hard) for AI players
  - `name` (string)
- In `Piece.ts`, track position: 
  - `startingArea` (boolean)
  - `mainPath` (with index)
  - `homeStretch` (with index)
  - `homeTriangle` (boolean)
  - `id` (unique identifier)

**Test:**
- Write Jest tests to verify player and piece functionality.
- Instantiate a player with 4 pieces and verify all pieces start in the `startingArea`.
- Check that `color`, `isAI`, and other properties are set correctly.
- Test piece movement between different board areas.

---

## Step 9: Implement Dice Rolling Logic

**Instruction:**
- Create `src/utils/rollDice.ts` with a function returning a random integer between 1 and 6.
- Add logic to track consecutive sixes (reset after 3 consecutive sixes).
- Update `Dice.tsx` to call this function on "Roll" button click and display the result.
- Implement the animation for dice rolling.

**Test:**
- Write Jest tests for the dice rolling logic.
- Test the consecutive sixes rule (after 3 sixes, the turn should reset and player gets a 4th roll).
- Call `rollDice` multiple times and confirm all results are between 1 and 6.
- Click "Roll" in the UI and verify the displayed number matches the function output with animation.

---

## Step 10: Define Movement Rules

**Instruction:**
- Create `src/game/GameRules.ts` and `src/types/RuleTypes.ts`.
- Add functions:
  - Move a piece from `startingArea` to the main path entry point on a roll of 6.
  - Move a piece along the main path by the dice value.
  - Move a piece into the home stretch or home triangle (requires exact roll).
- Prevent illegal moves (e.g., moving a piece already in `homeTriangle`).
- Implement the 3 consecutive sixes rule (nullify the moves and reset).

**Test:**
- Write Jest tests for all movement rules.
- Test moving a piece from `startingArea` to main path with a 6.
- Test advancing a piece 3 spaces on the main path with a roll of 3.
- Test requiring an exact roll to enter `homeTriangle`.
- Test the 3 consecutive sixes rule.

---

## Step 11: Add Capturing Mechanics

**Instruction:**
- In `GameRules.ts`, add logic:
  - If a piece lands on an opponent's piece on the main path (not a safe space), return the opponent's piece to its `startingArea`.
  - Prevent capturing on safe spaces.
- Add visual and audio feedback for captures.

**Test:**
- Write Jest tests for capturing mechanics.
- Simulate a move where a Red piece lands on a Blue piece (not on a safe space); confirm Blue returns to `startingArea`.
- Test the same on a safe space and verify no capture occurs.
- Verify visual and audio feedback works correctly.

---

## Step 12: Set Up Winning Conditions

**Instruction:**
- In `GameRules.ts`, add a `checkWin` function:
  - Return `true` if all 4 pieces of a player are in `homeTriangle`.
  - Return `false` otherwise.
- Add a victory screen or modal to display when a player wins.

**Test:**
- Write Jest tests for win conditions.
- Set all 4 pieces of a player to `homeTriangle` and confirm `checkWin` returns `true`.
- Leave one piece out and verify it returns `false`.
- Test the victory screen appears correctly when a player wins.

---

## Step 13: Implement AI Logic with Difficulty Levels

**Instruction:**
- Create `src/game/AI.ts` and `src/types/AITypes.ts`.
- Define three AI difficulty levels using standard Ludo game approaches:
  - **Easy**: Makes random valid moves with basic strategy (20% chance to prioritize getting pieces out with 6, otherwise random).
  - **Medium**: Moderate strategy - prioritizes getting pieces out with 6 (70% chance), captures when possible (80% chance), otherwise moves the piece closest to home (60% chance) or random move.
  - **Hard**: Advanced strategy - evaluates all possible moves with weighted scoring:
    - Getting pieces out: 100 points
    - Capturing opponents: 90 points
    - Reaching safe spaces: 80 points
    - Moving pieces closer to home: 70 points
    - Avoiding capture risk: -50 points
    - Choose highest scoring move with 90% probability, random valid move with 10% probability
- Implement turn timers based on difficulty:
  - Easy: 10 seconds
  - Medium: 8 seconds
  - Hard: 5 seconds
  - Timer starts after dice roll, not during roll animation
- Add visual countdown (both circular and numerical) and audio cues at 3 seconds remaining

**Test:**
- Write Jest tests for each AI difficulty level.
- Simulate turns for each AI difficulty and verify they make appropriate moves.
- Test Easy AI makes random but valid moves.
- Test Medium AI prioritizes getting pieces out and captures.
- Test Hard AI makes strategically sound decisions.

---

## Step 14: Manage Game State with Context

**Instruction:**
- Create `src/contexts/GameContext.tsx`.
- Define state: 
  - `players` (array)
  - `currentPlayer` (index)
  - `diceRoll` (number)
  - `consecutiveSixes` (number)
  - `gameStatus` (e.g., "playing", "won")
  - `turnTimer` (number)
  - `settings` (object with sound, animation toggles, etc.)
- For consecutive sixes:
  - Track count in state
  - On third six, allow one more roll
  - Use the final roll result for movement
  - Add warning animation/sound on second and third six
- Auto-save game state to localStorage after each player completes their turn
- Provide this context in `App.tsx` and use `useContext` in components

**Test:**
- Write Jest tests for the context and state management.
- Update `currentPlayer` in the context and confirm `PlayerIndicator` reflects the change.
- Set `diceRoll` and verify `Dice.tsx` displays it.
- Test turn timer functionality.

---

## Step 15: Handle User Interactions

**Instruction:**
- In `Dice.tsx`:
  - Add click handler for "Roll" button to update `diceRoll` in context
  - Implement dice rolling animation (0.5-1 second)
  - Start difficulty-based turn timer after roll animation completes
  - Add visual and audio feedback for consecutive sixes
- In `Board.tsx`:
  - Highlight eligible pieces after roll (e.g., pulsing glow effect)
  - Move pieces on click/tap with smooth animation
  - Show capture animations and play sound effects
  - Support touch gestures and keyboard controls
- Implement turn timer with difficulty-based durations:
  - Circular progress indicator around active player
  - Numerical countdown in center
  - Audio warning at 3 seconds remaining
  - Automatic turn pass if no move made
  - Reset timer on valid piece selection

**Test:**
- Verify dice roll and timer mechanics for each difficulty level
- Test piece movement and capture animations
- Confirm audio feedback works as expected
- Check keyboard and touch controls

---

## Step 16: Integrate Visual and Audio Assets

**Instruction:**
- Add assets to `src/assets/`:
  - Board background image, piece icons, dice graphics
  - High-impact sound effects (all with adjustable volume):
    - Dice roll: Rolling sound with satisfying impact
    - Piece move: Sliding sound with soft impact
    - Capture: Dramatic impact sound
    - Victory: Triumphant fanfare
    - Warning: Alert sound for consecutive sixes
  - Sound effects should be impactful but not overwhelming
  - Implement volume control for different sound categories
- Use them in components (e.g., `<img>` for pieces, `<audio>` for sounds)
- Add sound toggle and volume controls in `Settings.tsx`

**Test:**
- Write tests to verify assets load correctly.
- Confirm all assets load in the UI (e.g., board image displays).
- Trigger a dice roll and verify the sound plays (unless toggled off).
- Test that toggling sound in settings works correctly.

---

## Step 17: Implement Game Setup Flow

**Instruction:**
- Create `src/components/GameSetup.tsx`.
- Add options for:
  - Number of players (2-4)
  - Player types (Human or AI)
  - AI difficulty for AI players
  - Player colors
- Link this to the "Play" button in the Main Menu.
- Ensure the setup flow is intuitive and responsive.

**Test:**
- Write Jest tests for the game setup flow.
- Navigate through the setup process and verify all options work.
- Start a game with various configurations and confirm they're applied correctly.

---

## Step 18: Add Game State Persistence

**Instruction:**
- Create `src/utils/storage.ts` for local storage functions.
- Save game state to `localStorage` after each move.
- Add an option to continue a saved game from the Main Menu.
- Include a "New Game" option to reset the state.

**Test:**
- Write Jest tests for state persistence.
- Make several moves, refresh the page, and verify the game state is restored.
- Test the "New Game" option resets the state correctly.

---

## Step 19: Test the Full Game Flow

**Instruction:**
- Implement comprehensive error handling:
  - Invalid moves: Clear visual/audio feedback
  - Connection issues: Retry mechanism with user feedback
  - Undo feature: Allow undoing last move within 3 seconds
  - Edge cases: Handle all game state anomalies
- Add accessibility features:
  - High contrast mode with distinct patterns for colors
  - Screen reader support for all game events
  - Keyboard controls with visual indicators
  - Color-blind friendly patterns for pieces and board
- Test responsive design across devices:
  - Desktop: Optimize for large screens (≥1200px)
  - Tablet: Adjust layout for medium screens (768px-1199px)
  - Mobile: Portrait and landscape orientations (<768px)
  - Touch controls: Large hit areas and clear feedback
  - Test on various browsers and devices

**Test:**
- Write end-to-end tests for complete game flows.
- Play full games against each AI difficulty level and ensure all mechanics work without errors.
- Verify turn indicators and timers switch correctly in multiplayer.
- Test all special rules and edge cases.

---

## Step 20: Optimize for Performance and Accessibility

**Instruction:**
- Implement responsive design with breakpoints:
  - Desktop (≥1200px): Full-size board with side panels
  - Tablet (768px-1199px): Scaled board with reorganized controls
  - Mobile (<768px): 
    - Portrait: Vertical layout with board on top
    - Landscape: Horizontal layout with optimized spacing
- Add accessibility features:
  - High contrast mode:
    - Distinct patterns for each player color
    - Enhanced border contrast
    - Clear visual feedback for actions
  - Screen reader support:
    - Descriptive announcements for all game events
    - Turn status and timer updates
    - Piece movement confirmation
  - Keyboard controls:
    - Tab navigation with visual indicators
    - Spacebar for dice roll
    - Arrow keys/WASD for piece selection
    - Enter for piece movement
  - Color-blind modes:
    - Pattern overlays for pieces
    - Texture differences for board sections
    - Icon indicators for special spaces
- Optimize performance:
  - Lazy load audio assets
  - Compress and cache images
  - Minimize render cycles
  - Efficient animation handling

**Test:**
- Verify responsive layout on various devices and orientations
- Test all accessibility features with screen readers
- Check keyboard navigation flow
- Validate color-blind friendly design
- Monitor performance metrics across devices

---

## Step 21: Prepare for Future Phases

**Instruction:**
- Structure the code to facilitate future online multiplayer:
  - Separate game logic from UI components.
  - Design the state management to be compatible with server synchronization.
  - Add placeholder hooks for network functionality.
- Document the codebase thoroughly with comments and TypeScript types.

**Test:**
- Review the code structure to ensure it's modular and extensible.
- Verify all functions have proper TypeScript types and documentation.

---

## Step 22: Deploy the Game

**Instruction:**
- Set up a CI/CD pipeline with GitHub Actions:
  - Run tests on pull requests.
  - Build and deploy on merges to main.
- Run `npm run build` to create a production build.
- Deploy to Netlify or Vercel by connecting the GitHub repository.
- Configure environment variables if needed.
- Access the deployed URL.

**Test:**
- Open the URL in various browsers (Chrome, Firefox, Safari, Edge) and confirm the game loads and plays as expected.
- Test on mobile and desktop to verify responsiveness.
- Verify all features work in the production environment.

---

This plan ensures a systematic build of Ludotwist's base game, with each step validated to guarantee a functional, enjoyable Ludo experience. The plan now includes more specific details about board dimensions, AI difficulty levels, game flow specifics (like the 3 consecutive sixes rule and 5-second turn timer), and preparations for future phases. Developers can follow these instructions to deliver Phase 1 successfully, ready for future enhancements.