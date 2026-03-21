# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**CocoNUT Cracker** - A visual coconut analysis tool built as a single-page HTML application. Users upload coconut images, analyze them with drawing tools, and receive precision metrics about the coconut's characteristics.

**Tech Stack:**
- Vanilla HTML5 + CSS3 (no build step needed)
- Canvas API for image drawing and analysis
- CDN libraries: tsParticles, Anime.js, canvas-confetti
- Single `index.html` file (self-contained)

**Repository:** https://github.com/adibenyaakov98-boop/test-claude

## Running & Development

**To view the application:**
- Open `index.html` directly in a browser
- No server or build process required
- Works offline after initial page load

**To edit:**
- All code is in `index.html` (styles, HTML, JavaScript)
- Changes are immediately visible when you refresh the browser

## Project Architecture

### Page Structure (3-Panel Layout)
```
┌─────────────────────────────────┐
│           HEADER                 │
├──────────┬──────────────┬────────┤
│  UPLOAD  │   CANVAS     │ RESULTS│
│  PANEL   │   & STATUS   │ PANEL  │
│          │              │        │
└──────────┴──────────────┴────────┘
```

- **Left Panel**: File upload zone + action buttons
- **Center Panel**: Canvas for image display + drawing overlay + status bar
- **Right Panel**: Analysis results (locked until analysis runs)

### JavaScript Architecture

**State Management** (`appState` object):
- `imageLoaded`: boolean - whether an image is currently loaded
- `analyzing`: boolean - whether analysis is in progress
- `lastResult`: object - cached results from last analysis
- Centralized state prevents sync issues

**Event System:**
- File upload trigger → `handleUpload()`
- Canvas interaction → drawing overlay listeners
- Analysis button → `runAnalysis()` (shows modal, calls worker functions)
- Reset button → `reset()`

**DOM Caching** (`dom` object):
- All element references cached at startup (e.g., `dom.uploadBtn`, `dom.imageCanvas`)
- Prevents repeated `querySelector()` calls
- Initialized in `setupDOM()`

**Canvas Layers:**
- `imageCanvas`: displays uploaded image (background)
- `overlayCanvas`: drawing overlay on top (interactive, cursor: crosshair)
- Both canvases are absolutely positioned and overlap

**Modal System:**
- Loading modal shows during analysis with animated radar spinner
- Steps animate in sequence using CSS and JavaScript timing
- `showModal()` / `hideModal()` control visibility

### Styling

**Color System (CSS Variables):**
- Lemonade theme: yellow (#FBBF24, #FCD34D), lime green (#86EFAC), cyan (#06B6D4)
- Typography: Poppins font (modern, playful)
- Rounded corners (12-24px) throughout
- Glass-morphism effects with soft shadows and gradients

**Animations:**
- `bounce-smooth`: upload zone + icon hover
- `glow-pulse`: status dot breathing effect
- `spin-smooth`: loading radar
- Cubic-bezier timing for playful feel (0.34, 1.56, 0.64, 1)

## Key Patterns & Details

### Image Handling
- File input is hidden; `label` click triggers it
- Image loaded via `FileReader` API into canvas
- Canvas sizing matches image aspect ratio
- Drawing overlay canvas synchronized with image canvas dimensions

### Analysis Simulation
- `runAnalysis()` shows modal, simulates work (currently hardcoded results)
- Replace this function when connecting to real analysis backend
- Results format: `{ quality, density, maturity, confidence }`
- Confidence bar animates from 0% → result value on display

### Mobile Responsiveness
- Grid layout switches from 3-column to 2-column at 1200px breakpoint
- Canvas wrapping has min-height to prevent collapse
- Button sizing scales down on smaller screens

## Design Guidance

**Lemonade Aesthetic (Current):**
- Fresh, playful, bright color palette
- High-energy animations with smooth easing
- Generous gradients and soft shadows
- Premium feel with modern typography
- Friendly, approachable tone

**When modifying UI:**
- Keep color palette cohesive (all lemonade colors should feel intentional)
- Animations should use cubic-bezier easing or spring-like feels
- Maintain rounded corner consistency (12px minimum, 24px for major containers)
- Use CSS variables for colors—never hardcode color values inline

## GitHub Integration

Claude automatically commits after file changes and pushes to GitHub. All commits attributed to user only (no co-author).

## Code Conventions

- **JavaScript style**: camelCase for variables/functions, clear naming (`handleUpload`, `appState`, `dom`)
- **Comments**: Use section headers (`// ============ SECTION NAME ============`) to organize code blocks
- **No external dependencies**: Leverage Canvas API and vanilla JS to keep the app self-contained
