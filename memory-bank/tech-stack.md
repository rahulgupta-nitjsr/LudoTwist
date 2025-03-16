# Tech Stack for Ludotwist (Side Project with Minimal Budget)

This document outlines the technology stack for "Ludotwist," a web-based Ludo game built as a side project. The stack is optimized for minimal cost, leveraging free or low-cost tools, while remaining flexible for future enhancements like online multiplayer. The front-end is built with **JavaScript and React**, and the back-end (for future phases) will use **Python** with FastAPI.

## Front-End: React-Based Web App

The front-end is the core of Ludotwist for Phase 1, running entirely in the browser using React.

### Technologies
- **HTML5**
  - **Purpose**: Structures the game board, UI elements, and layout.
  - **Why**: Essential for web apps, integrates seamlessly with React via JSX.
- **CSS3 with Styled Components**
  - **Purpose**: Styles the game for a responsive, visually appealing experience. Styled Components keeps CSS modular and tied to React components.
  - **Why**: Simplifies styling, avoids global CSS conflicts, and ensures responsiveness.
- **JavaScript with React.js**
  - **Purpose**: Powers the interactive UI and game logic (dice rolls, piece movement, turn management) using React components and hooks.
  - **Why**: React’s component-based architecture ensures reusable, maintainable code, and its virtual DOM optimizes performance.
- **React Context API**
  - **Purpose**: Manages global game state (e.g., current player, piece positions, dice roll results) across components.
  - **Why**: Built into React, lightweight, and sufficient for Phase 1’s needs.

### Game Logic (Client-Side)
- **JavaScript Classes within React**
  - **Purpose**: Structures game entities (e.g., `Player`, `Piece`, `Board`) as classes or objects, integrated into React’s state or Context.
  - **Why**: Keeps logic organized and reusable, with React managing state updates.
- **Basic Rule-Based AI**
  - **Purpose**: Simulates opponents in single-player mode with simple logic (e.g., prioritize moving pieces out, capture when possible).
  - **Why**: Easy to implement in JavaScript, runs locally in the browser.

## Back-End: Future Online Multiplayer

No back-end is required for Phase 1 (single-player and local multiplayer run locally in the browser). This stack is planned for future phases when online multiplayer is introduced.

### Technologies
- **Python with FastAPI**
  - **Purpose**: Serves as the back-end framework to handle game sessions, API requests, and server-side logic.
  - **Why**: FastAPI is lightweight, modern, and Python-based (per your preference), offering simplicity and high performance with asynchronous support.
- **WebSockets (via FastAPI)**
  - **Purpose**: Enables real-time communication for online multiplayer (e.g., syncing dice rolls, moves).
  - **Why**: Built into FastAPI, keeps the back-end Python-centric, and supports real-time features efficiently.

### Integration with React
- **API Calls**: React uses `fetch` or `axios` to communicate with FastAPI endpoints (e.g., `/game/move`).
- **WebSockets**: React connects to FastAPI WebSockets using the `WebSocket` API for real-time updates.

## Deployment

### Phase 1: Static Hosting for Front-End
- **Platform**: Netlify or Vercel
  - **Purpose**: Hosts the React app as a static site after building with `npm run build`.
  - **Why**: Free tiers, automatic scaling, and CI/CD integration with Git. Ideal for a side project with no server costs for Phase 1.

### Future Phases: Back-End Hosting
- **Platform**: Heroku, Render, or Fly.io
  - **Purpose**: Hosts the Python FastAPI back-end with WebSocket support.
  - **Why**: Offers free or low-cost tiers for small projects, supports Python apps, and integrates well with static front-end hosting.

## Version Control

- **Git with GitHub (or GitLab/Bitbucket)**
  - **Purpose**: Tracks code changes, enables collaboration, and integrates with deployment platforms.
  - **Why**: Free for public repositories; private repos are available on GitHub’s free plan with limitations. GitLab and Bitbucket also offer free private repos.

## Testing

- **Jest with React Testing Library**
  - **Purpose**: Runs unit tests for React components and game logic.
  - **Why**: Jest is widely used with React, and React Testing Library ensures components behave as expected.
- **Pytest** (Future)
  - **Purpose**: Tests the Python FastAPI back-end when implemented.
  - **Why**: Python-native, lightweight, and pairs well with FastAPI.

## Development Tools

- **Node.js and npm**
  - **Purpose**: Runs the React development environment and manages dependencies (e.g., `react`, `styled-components`).
  - **Why**: Required for React apps, even with a Python back-end.
- **Create React App (CRA)**
  - **Purpose**: Bootstraps the React project with a pre-configured setup (Webpack, Babel, etc.).
  - **Why**: Simplifies initial development, allowing focus on coding rather than build configuration.
- **Python Environment**
  - **Purpose**: Runs the FastAPI back-end locally during development (future phases).
  - **Why**: Ensures compatibility with your chosen Python back-end.

## Database (Future Phases)

- **SQLite** or **PostgreSQL**
  - **Purpose**: Stores game data (e.g., user accounts, game history) if needed in future phases.
  - **Why**: SQLite is simple and file-based (no server needed), while PostgreSQL is available on Heroku’s free tier for more complex needs.

## Why This Stack?

- **Minimal Budget**: 
  - Phase 1 uses only a front-end hosted on free platforms (Netlify or Vercel), eliminating server costs initially.
  - Future phases leverage free tiers from Heroku, Render, or Fly.io for the back-end, alongside free tools for version control and testing.
- **Flexibility for Future Phases**: 
  - React’s modular structure supports adding new features (e.g., special rules, power-ups) without major refactoring.
  - Python with FastAPI is lightweight yet powerful, making it easy to implement online multiplayer with WebSockets when needed.
- **Your Preferences**: 
  - Front-end uses JavaScript with React (assuming "Reach" was a typo), a robust and popular choice.
  - Back-end uses Python, aligning with your request, with FastAPI providing a modern, efficient framework.

## Key Considerations

- **Phase 1 Simplicity**: The game runs entirely in the browser for single-player and local multiplayer, avoiding back-end complexity and costs initially.
- **Scalability**: Adding a Python back-end with FastAPI in future phases is straightforward, with REST APIs or WebSockets connecting seamlessly to the React front-end.
- **Modular Code**: React components and JavaScript classes keep the codebase organized, easing the addition of new features or rules later.

This stack ensures Ludotwist can be built as a side project with minimal costs while remaining scalable for future enhancements like online multiplayer. Let me know if you’d like to adjust anything further!