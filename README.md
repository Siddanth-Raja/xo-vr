# XO VR

XO VR is a Phase 1 immersive concept for XO Collective: a calm, atmospheric digital art space where projects become symbolic objects inside a living archive.

## Vision

The goal is not to recreate a website in VR. XO VR should feel like stepping into the living center of XO: dark, surreal, quiet, expandable, and emotionally specific. The first room is designed as a meeting-ready creative prototype that can evolve into a deeper digital museum for projects, rituals, collaborations, and hidden discoveries.

## Current Features

- Dark gallery-like environment with fog, intentional ground treatment, and soft ambient lighting.
- Red dodecahedron heartbeat core that rotates, pulses, and brightens on hover or gaze.
- Subtle orbiting placeholder social links for Instagram, TikTok, YouTube, and Website.
- Five symbolic project objects: The Monolith, The Fragment, The Slab, The Oblique, and The Standard.
- Hover and gaze reactions for project objects, including temporary floating labels.
- Hidden nook around `x=10, z=5` with dark structure and a softly glowing yellow sphere.
- Desktop testing with WASD and mouse look.
- WebXR-compatible A-Frame scene with cursor and VR-style raycaster support.

## Tech Stack

- A-Frame
- WebXR
- Vite
- HTML, CSS, and vanilla JavaScript

## How to Run Locally

```bash
npm install
npm run dev
```

Then open the local Vite URL shown in the terminal, usually:

```text
http://localhost:5173
```

## Phase 1 Roadmap

- Replace placeholder social URLs with XO's actual channels.
- Define what each project object represents and tune shape, color, motion, and proximity behavior.
- Add richer project interactions, such as spatial audio, short text fragments, object-specific lighting, or portals.
- Explore a stronger hidden-discovery system for ideas that should not appear in the main room.
- Test the room in an actual VR headset and adjust scale, comfort, movement speed, and gaze timing.
- Decide whether Phase 2 needs split files, reusable components, or content loaded from external data.

## Meeting Notes

Questions for XO:

- What does each project represent?
- What emotion should each project object create?
- Which projects belong in the core room?
- Which ideas should be hidden or discovered later?
