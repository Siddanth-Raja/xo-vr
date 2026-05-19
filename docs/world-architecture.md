# XO VR World Architecture

XO VR is currently structured as one connected immersive world, not separate pages or menu-driven rooms.

## Spatial Sequence

1. **Core Room**
   - Central sacred hub for XO identity.
   - Anchored by a red heartbeat dodecahedron with layered glow, halos, plinth, and social orbit reveal.
   - Symbolic core objects represent XO Web, Galata, The Locals, Live Music Video, and XO Merch / NPC.

2. **Liminal Corridor**
   - Semi-open passage from the Core Room toward Dance.
   - Uses dark floor treatment, side scrims, overhead edge bars, low linework, and magenta/teal lighting.
   - Designed as an emotional transition, not a bridge inserted into either room.
   - Must maintain visible clearance from core objects, especially XO Web.

3. **Arrival / Decompression Zone**
   - Small pause space between corridor and Dance Room.
   - Uses lower side scrims and subtle lintels to frame movement without blocking the walking path or labels.
   - Marks the shift from sacred/networked core energy into rhythmic dance energy.

4. **Dance Room**
   - Warm, kinetic branch room shell.
   - Uses layered circular platforms, formation lines, pulsing rings, and warmer pink/teal lighting.
   - Represents New World Dance Project, The Locals, Valluri Sisters Choreography Project, and Riya Patel Collective Dance Project.

5. **Hidden Nook**
   - Discoverable side space around `x=10, z=5`.
   - Dark structure with a floating yellow sphere and subtle proximity/hover response.
   - Placeholder for secret content, hidden gems, sound cues, or Easter eggs.

## Navigation Language

- Desktop movement uses WASD and mouse look through the camera rig.
- WebXR remains enabled through A-Frame.
- Gaze/cursor and laser raycasters target `.interactive` objects.
- Spatial guidance comes from floor traces, lighting gradients, thresholds, and silhouettes rather than UI arrows or menus.

## Visual Language

- Dark, atmospheric, surreal, premium installation-art tone.
- Core Room: red, sacred, still, networked.
- Corridor: liminal, darker, compressed but passable.
- Arrival Zone: open pause, visual breath, subtle lighting shift.
- Dance Room: warmer, rhythmic, circular, body-centered.
- Hidden Nook: secretive, peripheral, softly glowing.
