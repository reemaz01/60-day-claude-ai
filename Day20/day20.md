Day 20
Build an AI Face Puzzle Game

Face Puzzle Game Generator

This project uses a single advanced prompt to generate a complete browser-based Face Puzzle Game as a standalone HTML application.

The generated application allows users to capture their face using their device camera, automatically convert the image into a puzzle, and solve it using drag-and-drop interactions on desktop and mobile devices.

The output is a fully self-contained HTML file with inline CSS and JavaScript and requires no build process or framework.



## Prompt Objective

Generate a production-ready Face Puzzle Game that:

* Accesses the user's webcam
* Captures a face photo
* Creates a puzzle from the captured image
* Supports multiple difficulty levels
* Tracks moves and completion time
* Detects puzzle completion automatically
* Stores leaderboard results locally
* Works across desktop and mobile browsers



## Key Features

### Camera System

* Webcam access using `getUserMedia()`
* Front-facing camera support
* Live camera preview
* Snapshot capture functionality
* Graceful handling of permission denial

### Puzzle Generation

* Difficulty options:

  * 3×3
  * 4×4
  * 5×5
* Automatic image slicing
* Random puzzle scrambling
* Solvable puzzle generation
* Dynamic tile rendering

### Gameplay

* Mouse drag-and-drop support
* Mobile touch gesture support
* Tile swapping mechanics
* Snap-to-grid positioning
* Correct-position indicators
* Active drag highlighting

### Progress Tracking

* Real-time timer
* Move counter
* Correct-piece counter
* Completion progress indicator

### Results System

* Automatic win detection
* Completion statistics
* Best-time leaderboard
* LocalStorage persistence
* Historical performance tracking

### User Experience

* Responsive design
* Modern UI
* Retake photo option
* Play again functionality
* New photo workflow
* Cross-browser compatibility



## Technical Implementation

### Technologies Used

* HTML5
* CSS3
* Vanilla JavaScript
* Canvas API
* MediaDevices API
* LocalStorage API

### Architecture

1. Camera Capture Layer
2. Image Processing Layer
3. Puzzle Generation Engine
4. Drag-and-Drop Controller
5. Game State Manager
6. Timer & Statistics System
7. Local Leaderboard Storage

### Browser Requirements

* HTTPS or localhost
* Camera permissions enabled
* Modern browser support

Supported browsers:

* Chrome
* Firefox
* Safari
* Edge


## Prompt Engineering Highlights

The prompt was designed to ensure:

* Single-file deployment
* No framework dependencies
* Mobile-first interaction support
* Complete feature coverage
* Production-ready output
* Responsive user interface
* Persistent leaderboard functionality



## Learning Outcomes

### Front-End Development

* Camera API integration
* Canvas image manipulation
* Dynamic DOM generation
* Touch event handling
* Drag-and-drop interactions

### Game Development

* Puzzle generation algorithms
* State management
* Win-condition detection
* Progress tracking
* Performance optimization

### Prompt Engineering

* Feature specification
* Constraint-driven generation
* Large-scale HTML generation
* Full-stack browser application creation
* AI-assisted game development


## Output

Generated artifact:

face-puzzle.html



Commit: [f4df568](https://github.com/reemaz01/60-day-claude-ai/commit/f4df568ac2cdb5e77222a2ac10562b4a9f25cf73)




