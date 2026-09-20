# Track 4: Games & Creative Canvas Playbook

Use this playbook when designing browser games, 2D/3D canvas simulations, interactive generative art, physics sandboxes, or gamified product interfaces.

---

## 1. Loop Architecture & State Simulation

- **Delta-Time Decoupling**:
  - Never tie movement or physics to raw frame ticks (different monitors run at 60Hz, 120Hz, 144Hz).
  - Always calculate delta time (`dt = (now - lastTime) / 1000`) and cap max delta to prevent physics explosion after tab backgrounding:
    ```js
    let lastTime = performance.now();
    function loop(currentTime) {
      const dt = Math.min((currentTime - lastTime) / 1000, 0.1);
      lastTime = currentTime;
      update(dt);
      render();
      requestAnimationFrame(loop);
    }
    requestAnimationFrame(loop);
    ```
- **State vs Render Separation**:
  - Keep game entities (positions, velocities, health, collisions) in a pure data structure.
  - The render function reads game state and draws—it never mutates game logic.

---

## 2. Rendering Layers: Canvas World vs. DOM/SVG HUD

- **Layer 1: Canvas / WebGL (Game World)**:
  - Handle entity sprites, background parallax, particle systems, physics effects.
  - DPR Scaling: Always scale for high-DPI (Retina) screens to prevent blurry canvas rendering:
    ```js
    const dpr = window.devicePixelRatio || 1;
    canvas.width = rect.width * dpr;
    canvas.height = rect.height * dpr;
    ctx.scale(dpr, dpr);
    ```
- **Layer 2: DOM / SVG Overlay (HUD & Chrome)**:
  - Render health bars, scores, dialog boxes, pause menus, inventory screens in crisp HTML/CSS overlaying the canvas (`pointer-events: none` on HUD container, `pointer-events: auto` on buttons).
  - Why: Vector-crisp typography, accessible text, responsive UI layout without tedious manual canvas text alignment.

---

## 3. Input Handling & Ergonomics

- **Keyboard Multi-Key Sets**:
  - Never rely on default `keydown` repeat rates. Maintain a set of currently pressed keys:
    ```js
    const keys = new Set();
    window.addEventListener('keydown', (e) => {
      if (['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight', ' '].includes(e.key)) {
        e.preventDefault(); // Prevent accidental page scrolling
      }
      keys.add(e.code);
    });
    window.addEventListener('keyup', (e) => keys.delete(e.code));
    ```
- **Pointer & Canvas Coordinate Normalization**:
  - Always convert mouse/touch viewport coordinates into canvas local game coordinates:
    ```js
    const rect = canvas.getBoundingClientRect();
    const scaleX = canvas.width / rect.width;
    const scaleY = canvas.height / rect.height;
    const gameX = (e.clientX - rect.left) * scaleX;
    const gameY = (e.clientY - rect.top) * scaleY;
    ```
- **Mobile Touch Controls**:
  - Provide a virtual on-screen joystick or directional touch pad for mobile viewports, using touch identifiers (`e.changedTouches`) to support multi-touch (e.g. moving while shooting).

---

## 4. Game "Juice" & Tactile Polish

A great game feels tactile and alive:
- **Screen Shake**: Add subtle camera offset decays on heavy impacts or explosions (`shakeIntensity * Math.sin(time)`).
- **Hit Stops / Freeze Frames**: Freeze simulation for 30–60ms on major impacts to deliver tactile weight.
- **Particle Systems**: Small bursts of sparks, dust, or debris on collisions, jumps, and deaths.
- **Procedural Audio (Web Audio API)**:
  - Synthesize basic sound effects (beeps, explosions, jumps, powerups) with simple oscillators so the game is immediately playable with zero external audio assets required.
  - Resume `AudioContext` only upon the user's first click/keypress to comply with browser autoplay policies.

---

## 5. Anti-Patterns to Avoid in Games

- **No unscaled canvas blur**: Never stretch a 300x150 default canvas via CSS without setting internal `width` and `height`.
- **No memory leaks in loops**: Never allocate new objects, arrays, or anonymous closures inside `update()` or `render()`—reuse vectors and particle pools to avoid garbage collection stutter.
- **No unpaused background tabs**: Automatically pause the game loop when `document.hidden` becomes true.
