# Spiral Project Navigator — Minimal Demo

Independently authored implementation of the 3D cylindrical spiral project navigator.

## Architecture

```
src/
├── config/
│   ├── spiral.ts          # Centralized geometric, motion, camera, and shader constants
│   └── theme.ts           # Visual shell tokens and styling parameters
├── content/
│   └── projects.ts        # 9 authoritative project records with procedural canvas texture generators
├── core/
│   ├── spiralMath.ts      # Pure math for cylindrical helix coordinates and index wrapping
│   ├── SpiralCard.ts      # Three.js Mesh wrapper with ShaderMaterial & uniform updates
│   ├── SpiralControls.ts  # Wheel, touch drag, mouse move, damping, clamping, idle drift
│   ├── SpiralScene.ts     # WebGL2 renderer, camera, effect composer, raycaster hit testing
│   └── shaders/
│       ├── cardVertex.ts    # Curvature, Y² screen warp, scroll speed bending
│       ├── cardFragment.ts  # Aspect contain/cover, front/back (3x3 blur) & SDF rounded rect
│       └── noiseFragment.ts # EffectComposer fullscreen subtle film grain pass
├── components/
│   └── ProjectHover.ts    # DOM project pill with cubic-bezier enter/leave transitions
├── styles/
│   └── main.css           # Visual shell framing, grid background, pill transitions
└── main.ts                # Application entry point & lifecycle management
```

## Setup & Running

```bash
npm install
npm run dev
npm run build
```
