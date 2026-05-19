# Current State

This reflects the latest implemented prototype state.

## Implemented

- **Core Room**
  - Red heartbeat dodecahedron centerpiece with pulse, rotation, layered glow, halos, plinth, and hover brightening.
  - Orbiting placeholder social links appear around the core on hover/gaze.
  - Symbolic core objects for XO Web, Galata, The Locals, Live Music Video, and XO Merch / NPC.
  - Reflective dark floor, network lines, cinematic lighting, fog, and distant silhouettes.

- **XO NPC**
  - Rebuilt as a subtle humanoid in all black: hoodie/body, hood/head, arms, and pants.
  - XO logo is loaded through `<a-assets>` from `assets/xo-logo.jpg` and placed on the hoodie chest.
  - Uses faint rim lighting and dark materials instead of the old glowing yellow placeholder.

- **Core-to-Dance Transition**
  - Old bridge/threshold system was replaced.
  - Current structure is: Core Room -> liminal corridor -> arrival/decompression zone -> Dance Room.
  - Corridor uses open side scrims, overhead bars, floor linework, and dark magenta/teal lighting.
  - Arrival zone has lowered side framing so the walking path and Dance labels remain readable.

- **Dance Room Shell**
  - Distinct warm, kinetic branch room positioned beyond the arrival zone.
  - Represents New World Dance Project, The Locals, Valluri Sisters Choreography Project, and Riya Patel Collective Dance Project.
  - Uses layered circular platforms, formation lines, pulsing rings, project-specific symbolic geometry, and subtle animations.
  - Recent readability pass lowered/repositioned blocking scrims so labels, especially Valluri Sisters, are easier to read from the room center.

- **Hidden Nook**
  - Existing dark nook with floating yellow sphere remains as a hidden discovery placeholder.

## Technical State

- Single-file A-Frame scene in `index.html`.
- No React, no engine changes, no heavy external assets.
- Runtime image asset: `assets/xo-logo.jpg`.
- Content is still mostly config/data-array driven for socials, core symbols, Dance projects, and generated linework.
- `npm run build` has been passing; Vite still reports the expected large A-Frame/Three bundle warning.

## Next Likely Work

- Tune Dance Room label readability in headset/browser after more manual navigation.
- Add lightweight interactions for the Dance project placeholders.
- Expand hidden-gem/NPC behavior without adding UI panels.
- Eventually split scene data/components only if `index.html` becomes difficult to maintain.
