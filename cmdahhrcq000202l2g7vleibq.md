---
title: "Building an Interactive Hand-Tracking Game with React, MediaPipe, and GSAP"
seoTitle: "Building an Interactive Hand-Tracking Game"
seoDescription: "The game displays a video feed from your webcam. Birds fly across the screen, and you “hit” them by showing a single raised finger (the “OK” gesture)"
datePublished: Sat Jul 19 2025 16:50:24 GMT+0000 (Coordinated Universal Time)
cuid: cmdahhrcq000202l2g7vleibq
slug: building-an-interactive-hand-tracking-game-with-react-mediapipe-and-gsap
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1752943687296/ad28538d-521d-455c-be5e-31006f3365bd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1752943784084/4761d7a1-324a-4f23-8993-2303899ff1e2.png
tags: react, learning, reactjs, gsap, learning-in-public, mediapipe, gsap-animation

---

## Introduction

Have you ever wanted to control a game with just your hand gestures, no mouse or keyboard required? In this blog, I’ll walk you through how I built a fun, interactive “Bird Hit Game” using React, MediaPipe Hands for real-time hand tracking, and GSAP for smooth animations. We’ll also discuss how to keep your codebase clean and maintainable by splitting large files into smaller, reusable modules.

---

## Demo Overview

The game displays a video feed from your webcam. Birds fly across the screen, and you “hit” them by showing a single raised finger (the “OK” gesture) in front of your camera. Each successful hit increases your score. The game runs for 60 seconds, and your final score is displayed at the end.

---

## Key Technologies

* **React**: For building the UI and managing state.
    
* **MediaPipe Hands**: For real-time hand landmark detection.
    
* **GSAP**: For smooth, performant animations (optional, but recommended for more advanced effects).
    
* **Canvas API**: For rendering the video, birds, and overlays.
    

---

## Project Structure

To keep the codebase clean and maintainable, I split the logic into three main files:

* `HandCanvas.tsx`: The main React component, handles state, effects, and rendering.
    
* `handDrawingUtils.ts`: Contains all drawing helper functions for the canvas.
    
* `handGameUtils.ts`: Contains utility functions for game logic and hand gesture detection.
    

---

## Code Walkthrough

### 1\. HandCanvas.tsx (Main Component)

This file manages the game state, handles the webcam and MediaPipe setup, and orchestrates the game loop.

**Key responsibilities:**

* Setting up the webcam and MediaPipe Hands.
    
* Managing game state (score, timer, game over, etc.).
    
* Handling the main animation and game logic loop.
    
* Rendering the UI and canvas overlays.
    

**Example: Importing Helpers**

```typescript
import {
  drawBird,
  drawGameInfo,
  drawClouds,
  drawPop,
  drawCanvasInfo,
  drawHandOverlay,
} from "./handDrawingUtils";
import { randomBird, dist, isOnlyOneFingerUp, Bird } from "./handGameUtils";
```

**Game Loop and Hand Detection:**

* The game uses `requestAnimationFrame` for smooth rendering.
    
* MediaPipe Hands detects hand landmarks in real time.
    
* If the “one finger up” gesture is detected, the code checks if the finger tip is close to any bird, marking it as “hit” and increasing the score.
    

**UI Rendering:**

* The canvas is used to draw the video feed, birds, hand overlays, and score.
    
* React state is used to trigger re-renders for score, timer, and game over screens.
    

---

### 2\. handDrawingUtils.ts (Drawing Helpers)

This file contains all the functions responsible for drawing on the canvas, such as:

* `drawBird`: Draws a bird with a beak and shadow.
    
* `drawGameInfo`: Renders the score and timer.
    
* `drawClouds`: (Optional) Draws animated clouds for a lively background.
    
* `drawPop`: Shows a pop effect when a bird is hit.
    
* `drawCanvasInfo`: Displays messages on the canvas.
    
* `drawHandOverlay`: Draws the detected hand landmarks and connections.
    

**Example: Drawing a Bird**

```typescript
export function drawBird(ctx: CanvasRenderingContext2D, bird: { x: number; y: number; radius: number; hit: boolean }) {
  ctx.save();
  ctx.beginPath();
  ctx.arc(bird.x, bird.y, bird.radius, 0, 2 * Math.PI);
  ctx.fillStyle = bird.hit ? "#aaa" : "#ffeb3b";
  ctx.shadowColor = "#333";
  ctx.shadowBlur = 8;
  ctx.fill();
  ctx.lineWidth = 3;
  ctx.strokeStyle = "#333";
  ctx.stroke();
  // Draw beak
  ctx.beginPath();
  ctx.moveTo(bird.x + bird.radius, bird.y);
  ctx.lineTo(bird.x + bird.radius + 12, bird.y - 6);
  ctx.lineTo(bird.x + bird.radius + 12, bird.y + 6);
  ctx.closePath();
  ctx.fillStyle = "#ff9800";
  ctx.fill();
  ctx.restore();
}
```

---

### 3\. handGameUtils.ts (Game Logic Helpers)

This file contains utility functions for the game logic:

* `randomBird`: Spawns birds at random positions and directions.
    
* `dist`: Calculates the distance between two points (used for hit detection).
    
* `isOnlyOneFingerUp`: Determines if the user is showing the “one finger up” gesture using hand landmarks.
    

**Example: Gesture Detection**

```typescript
export function isOnlyOneFingerUp(landmarks: NormalizedLandmarkList): boolean {
  const indexUp = landmarks[8].y < landmarks[6].y - 0.03;
  const othersDown = [12, 16, 20].every(
    (tip) => landmarks[tip].y > landmarks[tip - 2].y + 0.03
  );
  return indexUp && othersDown;
}
```

---

## Final Thoughts

This project is a great example of combining modern web technologies to create interactive, gesture-based experiences. By leveraging MediaPipe for hand tracking and keeping the code modular, you can build powerful and maintainable web apps.

---

### Source Code

Github Link:- [https://github.com/Ingole712521/HandTracking.git](https://github.com/Ingole712521/HandTracking.git)

**Happy coding! If you have questions or want to see more features, let me know in the comments.**

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)
    
* GitHub : [https://github.com/Ingole712521](https://github.com/Ingole712521)