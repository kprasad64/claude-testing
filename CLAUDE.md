# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This repository contains two browser-based games implemented as single HTML files:
1. `index.html` - Tic Tac Toe game with optional AI opponent (Minimax algorithm)
2. `shooter.html` - Top-down shooter game with player movement, mouse aiming, enemy spawning, and level progression

Both games are self-contained with HTML, CSS, and JavaScript in a single file, requiring no build steps or dependencies.

## Development Commands
Since these are static HTML/CSS/JS games, there are no traditional build or test commands. To develop and test:

**Viewing/Running Games**
- Open either HTML file directly in a web browser:
  - `index.html` for Tic Tac Toe
  - `shooter.html` for the top-down shooter
- For better performance and to avoid potential CORS issues with local file loading, serve via a local HTTP server:
  ```bash
  # Using Python 3
  python -m http.server 8000
  # Then navigate to http://localhost:8000/index.html or http://localhost:8000/shooter.html
  ```

**Code Editing**
- Edit the HTML files directly to modify game logic, styling, or content
- Changes take effect immediately upon reload in the browser

**Debugging**
- Use browser developer tools (F12) to inspect elements, debug JavaScript, and monitor performance
- Console.log statements are present in the code for debugging purposes

## Code Architecture & Structure

### Common Patterns Across Both Games
1. **State Management**: 
   - Centralized game state objects (`gameState` in shooter, `gameState` array and related variables in Tic Tac Toe)
   - State is updated in response to user input and game logic, then reflected in the UI

2. **Input Handling**:
   - Event listeners for keyboard and mouse actions attached to window/canvas elements
   - Input state tracked separately for smooth handling (e.g., key states for continuous movement)

3. **Separation of Concerns**:
   - HTML structure defines layout and static elements
   - CSS handles presentation and styling
   - JavaScript manages game logic, state updates, and rendering

4. **Initialization & Reset**:
   - Functions to initialize game state (`initGame` in shooter, `initBoard`/`resetGame` in Tic Tac Toe)
   - Clear reset mechanisms to restart gameplay

### Tic Tac Toe Specifics (`index.html`)
- **DOM-based rendering**: Uses CSS Grid for the board, updates cell content and classes directly
- **Turn-based logic**: Simple alternation between players with win condition checking via predefined arrays
- **AI Opponent**: Minimax algorithm for unbeatable computer play (optional via mode selection)
- **UI Feedback**: Status messages, hover effects, and visual distinction between X and O marks

### Top-Down Shooter Specifics (`shooter.html`)
- **Canvas-based rendering**: Uses HTML5 Canvas for all graphics, with a retro grid background
- **Real-time game loop**: `requestAnimationFrame` driven updates at ~60fps
- **Entity Systems**:
  - Player: Triangle shape with rotatable gun barrel, 8-directional movement
  - Bullets: Simple projectiles with lifetime and velocity
  - Enemies: Spawn from screen edges, move toward player, simple AI
  - Particles: Small effects for hits and explosions
- **Game Systems**:
  - Collision detection (bullet-enemy, enemy-player)
  - Health and scoring systems
  - Level progression with increasing difficulty
  - Audio/visual feedback (placeholder for future sound effects)

## Extending the Games
To add features:
1. **Modify Constants**: Adjust values at the top of each script (speeds, sizes, intervals) for tuning
2. **Add New Entities**: Follow existing patterns for bullets/enemies to add power-ups, obstacles, etc.
3. **Enhance Rendering**: Replace geometric shapes with sprite images or more complex canvas drawing
4. **Expand Game Logic**: Add new states (e.g., power-ups, different enemy types) by extending the state objects
5. **Improve UI**: Add more sophisticated DOM elements or canvas-based menus

## Repository Guidelines
- Keep each game in its own HTML file for simplicity
- Maintain backward compatibility when making changes
- Consider performance when adding complex visuals or many entities
- Test changes in multiple browsers if cross-browser compatibility is needed

## Future Considerations
If the project grows beyond simple games:
- Consider separating concerns into multiple files (HTML, CSS, JS modules)
- Introduce a build step for concatenation/minification if needed
- Add automated testing frameworks for game logic
- Implement asset management for images, sounds, etc.