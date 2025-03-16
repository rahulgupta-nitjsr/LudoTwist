# Project Architecture

## Directory Structure

### `/src/components`
- Purpose: React UI components
- Contains reusable visual elements
- Each component should be self-contained with its styles
- Current/Planned Components:
  - MainMenu.tsx (navigation and game setup)
  - Board.tsx (game board display)
  - Dice.tsx (dice rolling interface)
  - PlayerIndicator.tsx (player turn and status)
  - Settings.tsx (game configuration)
  - Help.tsx (rules and instructions)

### `/src/game`
- Purpose: Core game logic and rules
- Business logic separate from UI
- Contains game state management
- Planned Components:
  - Board.ts (board state and movement logic)
  - Player.ts (player state and actions)
  - GameRules.ts (rule enforcement)
  - AI.ts (computer player logic)

### `/src/contexts`
- Purpose: React Context providers
- Global state management
- Shared data and functionality
- Planned Contexts:
  - GameContext.tsx (game state and actions)
  - SettingsContext.tsx (user preferences)
  - AudioContext.tsx (sound management)

### `/src/hooks`
- Purpose: Custom React hooks
- Reusable stateful logic
- Shared behavior between components
- Planned Hooks:
  - useGame.ts (game state management)
  - useTimer.ts (turn timer logic)
  - useAudio.ts (sound effect handling)
  - useLocalStorage.ts (persistence)

### `/src/utils`
- Purpose: Utility functions
- Helper methods and shared logic
- Pure functions without state
- Planned Utils:
  - rollDice.ts (dice mechanics)
  - storage.ts (save/load functions)
  - validation.ts (move validation)
  - animation.ts (UI animations)

### `/src/assets`
- Purpose: Static resources
- Images, sounds, and other media
- Board graphics and piece designs
- Required Assets:
  - Board background
  - Player pieces (4 colors)
  - Dice faces
  - Sound effects
  - UI elements

### `/src/types`
- Purpose: TypeScript type definitions
- Shared interfaces and types
- Type guards and utility types
- Planned Types:
  - BoardTypes.ts (board interfaces)
  - PlayerTypes.ts (player interfaces)
  - GameTypes.ts (game state types)
  - AITypes.ts (AI configuration)

### `/src/tests`
- Purpose: Test files
- Unit and integration tests
- Test utilities and mocks
- Test Coverage:
  - Component rendering
  - Game logic
  - User interactions
  - AI behavior

## Key Files

### `App.tsx`
- Root component
- Routing configuration:
  - / (Main Menu)
  - /game (Game Board)
  - /settings
  - /help
- Global providers setup

### `index.tsx`
- Application entry point
- Root render logic
- Global styles and theming
- Error boundary setup

## Design Principles

1. **Separation of Concerns**
   - UI components in components/
   - Business logic in game/
   - State management in contexts/
   - Clear module boundaries

2. **Type Safety**
   - TypeScript throughout
   - Strict type checking
   - Shared type definitions
   - No any types

3. **Component Architecture**
   - Functional components
   - React hooks for state
   - Styled-components for styling
   - Responsive design

4. **Testing Strategy**
   - Jest for unit testing
   - React Testing Library for components
   - Integration tests for game logic
   - E2E tests for critical flows

5. **State Management**
   - React Context for global state
   - Local state for component-specific data
   - Persistence with localStorage
   - Predictable state updates

## Implementation Status

1. **Completed**
   - Project setup
   - Directory structure
   - Development environment
   - Initial test configuration

2. **In Progress**
   - Main Menu UI
   - Basic routing setup
   - Component planning

3. **Upcoming**
   - Game board implementation
   - Player mechanics
   - AI development
   - Sound system

## Future Considerations

1. **Scalability**
   - Modular structure for easy expansion
   - Prepared for online multiplayer
   - Extensible game rules
   - Plugin architecture for variants

2. **Performance**
   - Code splitting for routes
   - Asset optimization
   - State management optimization
   - Caching strategies

3. **Accessibility**
   - ARIA attributes
   - Keyboard navigation
   - Screen reader support
   - High contrast mode
   - Color-blind friendly design
