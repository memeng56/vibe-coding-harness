# Track 1: Mobile & Touch-First UI Playbook

Use this playbook when designing mobile applications (Capacitor, Cordova, React Native, iOS/Android webviews), mobile-first responsive web apps, PWAs, cover-screen / wearable surfaces, or touch-driven interfaces.

---

## 1. Task Focus & Glanceability (The "Seconds, Not Minutes" Rule)

Inspired by Android Wear & Mobile App Principles:

- **Focused on 1–2 Core Tasks**:
  - Never replicate an entire complex desktop screen onto a phone or compact display. Identify the **single primary goal** of each screen (e.g. view balance + send money; check next workout step; confirm ride).
- **Glanceable Hierarchy**:
  - Information must be parseable in **3–5 seconds**. Use prominent typography for key status metrics (e.g. "Arriving in 4 min", "$1,420.50"), accompanied by high-contrast status icons.
- **Shallow Navigation Trees**:
  - Keep navigation shallow: max 1–2 levels deep. Prefer flat bottom navigation, inline tabs, or self-dismissing bottom sheets rather than nested drill-down mazes that disorient users on the go.

---

## 2. Touch Ergonomics & Tap Targets

- **Minimum Hit Areas**:
  - Every interactive element (buttons, icon triggers, list items, checkboxes) must have a touch target of at least **44×44px** (iOS HIG) or **48×48px** (Material 3).
  - When visual icons are small (e.g. 20px), expand the hit target using transparent padding or `::before` / `::after` hit-slops.
- **Thumb Zone Architecture**:
  - Primary actions (submit buttons, bottom navigation, search trigger, FABs, filter sheets) belong in the **bottom third** of the screen within natural one-handed thumb reach.
  - Secondary or non-destructive metadata (titles, filters summary, read-only badges) go at the top.
  - Destructive actions (delete, reset) must require explicit reach or two-step confirmation.

---

## 3. Safe Areas, Bezels & Curved Boundaries

- **Viewport Setup**:
  - Ensure `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, maximum-scale=1, user-scalable=no">` is configured.
- **Safe Area Insets**:
  - Account for notches, camera cutouts, dynamic islands, and bottom home indicator bars:
    ```css
    padding-top: env(safe-area-inset-top, 20px);
    padding-bottom: env(safe-area-inset-bottom, 20px);
    padding-left: env(safe-area-inset-left, 0px);
    padding-right: env(safe-area-inset-right, 0px);
    ```
- **Curved & Compact Screen Safety (Vignettes & Insets)**:
  - For screens with extreme rounded corners, foldables, or wearable/circular displays, ensure critical content sits within a centered safe-content circle/box.
  - Use subtle top and bottom scrolling vignettes (fade masks) so scrolling lists fade elegantly instead of clipping abruptly against physical hardware bezels:
    ```css
    mask-image: linear-gradient(to bottom, transparent 0%, black 10%, black 90%, transparent 100%);
    ```

---

## 4. Gestures & Mobile-Native Patterns

- **Bottom Sheets over Center Modals**:
  - Replace desktop-style centered dialogs with sliding bottom sheets (drawers).
  - Include an interactive drag handle bar at the top of the sheet.
  - Implement swipe-down-to-dismiss with spring damping.
- **Touch Feedback & Active States**:
  - Remove gray flash tap highlights on WebKit: `-webkit-tap-highlight-color: transparent`.
  - Use instant `:active` states for tactile touch confirmation (e.g. `active:scale-[0.96] active:opacity-90 transition-transform duration-75`).
  - Trigger subtle haptic vibrations (`navigator.vibrate?.([10])` or native bridge) on primary button presses or sheet snaps.
- **Horizontal Carousels & Snap Points**:
  - Use native smooth touch scrolling with CSS snap points for horizontal cards:
    ```css
    display: flex;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none; /* hide scrollbars */
    ```

---

## 5. Non-Typing Input & Quick Actions

Typing on mobile keyboards while on the go is error-prone. Prioritize tap over type:
- **Predefined Action Chips**:
  - Provide quick-tap response chips (e.g. "$10", "$20", "$50", "Running 5m late", "Yes, on my way") instead of forcing text entry.
- **Input Types & Keypads**:
  - Match `inputmode` to exact data:
    - Numeric PINs/Codes: `inputmode="numeric" pattern="[0-9]*"`
    - Emails: `type="email" autocomplete="email"`
    - Tel: `type="tel" autocomplete="tel"`
  - Disable auto-capitalization and spellcheck on usernames, codes, and IDs (`autocapitalize="none" spellcheck="false"`).
- **Interactive Keyboard Resizing**:
  - Ensure focused inputs auto-scroll into view above the virtual keyboard (`interactive-widget=resizes-content`).

---

## 6. Battery & OLED Consciousness

- On OLED/AMOLED mobile and compact displays, dark mode should leverage true **pitch black (`#000000`)** backgrounds.
- True black turns off OLED pixels completely, saving significant battery life while blending software seamlessly into the hardware bezel.

---

## 7. Anti-Patterns to Avoid on Mobile

- **No Deep Navigation Mazes**: Never require users to drill down 3+ screens to complete a routine task.
- **No Reliance on Hover**: Never hide critical actions behind hover states. If an action exists, make it visible or accessible via tap/swipe.
- **No Rubber-Band Scroll Leakage**: Fixed overlays and drawers must declare `overscroll-behavior-y: contain` to prevent scrolling the page underneath.
- **No Tiny Inline Links**: Never place dense text links close together where fingers will mis-tap.
