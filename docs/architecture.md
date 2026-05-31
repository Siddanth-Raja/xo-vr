# XO VR Architecture

XO VR is a single connected A-Frame world defined in `index.html`. Rooms are not separate routes or pages; they are spatial zones inside one scene, connected by floor traces, transitions, light gradients, and generated project objects.

This document explains the current room map, room responsibilities, interaction systems, naming conventions, and the process for adding future rooms without disturbing the existing world.

## Room Map

Approximate top-down layout using world coordinates:

```text
                          z-

                 Dance Room
             center: -24.2, -14.2
                       ^
                       |
        Dance Arrival / Liminal Corridor
                       |
                       |
 Live Events Room <---- Core Room ----> Hidden Nook
 center: 21.5, -7.75   center: 0, 0   center: 10, 5
                       |
                       |
                Brand Transition
                       |
                       v
                Brand Work Room
                center: 0, 18.25

                          z+
```

Primary rooms are registered in `ROOM_REGISTRY`:

| Room key | Anchor / center | Purpose |
| --- | --- | --- |
| `core` | `0 0 0` | Central identity hub and navigation origin |
| `dance` | `-24.2 0 -14.2` | Kinetic branch room for dance projects |
| `live` | `21.5 0 -7.75` | Event branch for performances, crowd energy, and social gatherings |
| `brand` | `0 0 18.25` | Polished showroom branch for product and merch work |

Secondary spaces:

| Space | Anchor / center | Purpose |
| --- | --- | --- |
| `liminal-corridor` | `-12.75 0 -5.45` | Transition from Core to Dance |
| `dance-arrival-zone` | `-19.7 0 -11.35` | Pause zone before Dance |
| `live-events-transition` | `13.2 0 -4.85` | Transition from Core to Live Events |
| `live-events-arrival-zone` | `18.15 0 -6.9` | Pause zone before Live Events |
| `brand-transition` | `0 0 10.15` | Axial transition from Core to Brand Work |
| `brand-arrival-zone` | `0 0 14.15` | Pause zone before Brand Work |
| `hidden-nook` | `10 0 5` | Hidden expansion point for secret content |

## Room Purposes

### Core Room

The Core Room is the sacred identity hub for XO. It contains the heartbeat core, social orbit, symbolic project objects, floor rings, network lines, and overhead network fragments.

Core responsibilities:

- Establish the emotional and visual identity of the world.
- Host foundational symbolic objects: XO Web, Galata, The Locals, Live Music Video, and XO Merch / NPC.
- Provide navigation signals to branch rooms through `BRANCH_NAV_CUES`.
- Drive core proximity behavior through `core-presence` and `heartbeat-core`.

### Dance Room

The Dance Room is the warm, rhythmic branch for choreography and movement-based projects.

Dance responsibilities:

- Represent dance projects through generated `DANCE_PROJECTS`.
- React to user movement with restrained floor pulses.
- Use rings, formation lines, suspended ribbons, and trail lines to express motion.
- Keep movement response local to the Dance Room.

### Live Events Room

The Live Events Room is the event branch for rave, DJ, coffee, and crowd-based work.

Live Events responsibilities:

- Represent event projects through generated `LIVE_EVENT_PROJECTS`.
- Maintain crowd markers and venue atmosphere.
- React to proximity by subtly lifting object emissive intensity, room beams, rings, lights, steam, and auras.
- Support future event-specific metadata or media without changing the room shell.

### Brand Work Room

The Brand Work Room is a cool, polished showroom for product and merch presentation.

Brand responsibilities:

- Represent commercial/product work through generated `BRAND_PROJECTS`.
- Keep product presentation centered, axial, and gallery-like.
- React to user presence through scan lines, column glows, focal elements, ceiling lights, and architectural sheens.
- Provide a natural future home for project metadata, external product assets, or richer media displays.

### Transitions

Transitions are not rooms. They are navigational connective tissue.

Transition responsibilities:

- Preserve walking clearance between rooms.
- Use architecture, trails, thresholds, and lighting cues instead of UI arrows.
- Keep branch identity legible before the visitor reaches the room.
- Provide clean extension points for future rooms and hidden paths.

### Hidden Nook

The Hidden Nook is a discoverable side chamber.

Hidden-space responsibilities:

- Provide a future location for secret content, easter eggs, spatial audio, or hidden project variants.
- Stay peripheral so it does not compete with the main branch-room structure.
- Use lightweight proximity/hover behavior through `secret-sphere`.

## Interaction Systems

Interaction code is grouped under the `INTERACTIONS` section in `index.html`.

| Component / system | Purpose | Main selectors/config |
| --- | --- | --- |
| `interactive-surface` | Shared hover behavior for generated project objects | `INTERACTION_CONFIG.hover`, `COMMON_MATERIALS.label` |
| `billboard` | Keeps labels facing the active camera | Attached to generated labels |
| `heartbeat-core` | Handles heartbeat pulse, hover activation, and social orbit reveal | `ROOM_SELECTORS.core`, `INTERACTION_CONFIG.core` |
| `environmental-reactivity` | Computes active room, room presence, and movement presence | `ROOM_REGISTRY`, `ROOM_REACTIVITY_CONFIG` |
| `core-presence` | Proximity lift for core aura, network lines, overhead fragments, core objects, and social details | `ROOM_SELECTORS.core` |
| `dance-room-response` | Movement and proximity response inside Dance Room | `ROOM_SELECTORS.dance`, `INTERACTION_CONFIG.dance` |
| `live-events-room-response` | Proximity response for live event objects, beams, crowd markers, steam, rings, and lights | `ROOM_SELECTORS.liveEvents` |
| `brand-room-response` | Proximity response for brand objects, columns, scan lines, ceiling accents, sheens, and focal elements | `ROOM_SELECTORS.brandWork` |
| `orbit` | Simple continuous rotation for the social orbit | `orbit="speed: ..."` |
| `secret-sphere` | Hidden Nook proximity/hover scale and glow response | `INTERACTION_CONFIG.secretSphere` |

Interaction principles:

- Use `ROOM_REGISTRY` for room centers and reactivity radii.
- Use `ROOM_SELECTORS` instead of hard-coded selectors inside components.
- Cache repeated DOM lookups with `ensureElement` and `ensureCachedElements`.
- Use `data-base-*` attributes for base intensity, opacity, or radius values that are modified during interaction ticks.
- Keep reactions local to their room unless the behavior is intentionally global.

## Naming Conventions

Use consistent naming so generated code, static markup, and interaction components stay easy to connect.

### Room Keys

Room keys are short lowercase identifiers used by reactivity systems:

- `core`
- `dance`
- `live`
- `brand`

Add new keys to `ROOM_KEYS` and `ROOM_REGISTRY`.

### Room Anchors

Room anchor IDs should follow:

```text
<room-name>-room-anchor
```

Examples:

- `dance-room-anchor`
- `live-events-room-anchor`
- `brand-work-room-anchor`

### Generated Roots

Generated content roots should follow:

```text
<room-name>-projects
<room-name>-trails
<room-name>-columns
<room-name>-crowd
```

Examples:

- `dance-projects`
- `live-event-trails`
- `brand-columns`

### Object Classes

Interactive project objects should use:

```text
interactive <room-name>-object
```

Examples:

- `interactive dance-object`
- `interactive live-object`
- `interactive brand-object`

Core symbolic objects use:

```text
interactive core-symbol
```

### Effects And Reactive Elements

Use room-prefixed classes for anything a response component mutates:

```text
<room-name>-floor-ring
<room-name>-room-light
<room-name>-object-aura
<room-name>-scan-line
<room-name>-hanging-ribbon
```

Examples:

- `dance-floor-ring`
- `live-room-light`
- `live-object-aura`
- `brand-scan-line`
- `brand-architectural-sheen`

### Data Attributes

Use `data-base-*` attributes for mutable visual values:

```text
data-base-opacity
data-base-emissive
data-base-intensity
data-ring-radius
```

The response systems read these with `materialNumber(...)` so each element can preserve its own baseline while still reacting consistently.

## How To Add A New Room

Use this checklist when adding a future room. Do not start by copying a large block of existing markup; first add the room to config and generated content.

1. Add a room key.

Update `ROOM_KEYS`:

```js
const ROOM_KEYS = Object.freeze({
  core: "core",
  dance: "dance",
  liveEvents: "live",
  brandWork: "brand",
  narrative: "narrative",
});
```

2. Add IDs and selectors.

Update `ROOM_IDS` and `ROOM_SELECTORS` with the room anchor, generated roots, and any reactive classes.

```js
narrative: {
  anchor: "narrative-room-anchor",
  projectsRoot: "narrative-projects",
  trailsRoot: "narrative-trails",
}
```

3. Register the room center and reactivity radius.

Add the new room to `ROOM_REGISTRY`:

```js
[ROOM_KEYS.narrative]: {
  label: "Narrative Room",
  center: new THREE.Vector3(0, 0, -24),
  radius: 6.2,
  fullRadius: 2.4,
}
```

`ROOM_REACTIVITY_CONFIG.rooms` is built from `ROOM_REGISTRY`, so new room presence will be available automatically.

4. Add room content config.

Create a project array such as `NARRATIVE_PROJECTS`, then add it to `ROOM_CONTENT`.

```js
[ROOM_KEYS.narrative]: {
  projects: NARRATIVE_PROJECTS,
  trails: NARRATIVE_TRAILS,
}
```

5. Add a room creation function.

Use `createInteractiveProjectObject(...)`, `appendTrailLines(...)`, and room-specific detail helpers as needed.

```js
const createNarrativeRoom = () => {
  const roomRoot = getRoot(ROOM_SELECTORS.narrative.projectsRoot);

  ROOM_CONTENT[ROOM_KEYS.narrative].projects.forEach((project) => {
    const object = createInteractiveProjectObject(project, {
      className: "narrative-object",
      baseEmissive: 0.32,
      hoverScale: 1.07,
      idleAnimationName: "narrative",
      includeDetailDataset: true,
    });

    roomRoot.appendChild(object);
  });

  appendTrailLines(
    getRoot(ROOM_SELECTORS.narrative.trailsRoot),
    ROOM_CONTENT[ROOM_KEYS.narrative].trails,
  );
};
```

6. Add static room shell markup.

Add the anchor and generated roots in the body:

```html
<a-entity id="narrative-room-anchor" position="0 0 -24">
  <!-- Room shell geometry here. -->
  <a-entity id="narrative-projects"></a-entity>
</a-entity>

<a-entity id="narrative-trails"></a-entity>
```

Keep shell geometry responsible for room atmosphere and spatial boundaries. Keep generated project objects in JavaScript config.

7. Add transition cues.

Add a `BRANCH_NAV_CUES` entry if the room should be discoverable from Core.

Use:

- `trail` for floor guidance.
- `particles` for subtle motion hints.
- `threshold` for the entry marker.
- `anchor` for distant room preview geometry.

8. Add a response component only if needed.

If the room needs custom environmental behavior, create a focused component:

```js
AFRAME.registerComponent("narrative-room-response", {
  init() {
    this.narrativeObjects = [];
    this.cameraPosition = new THREE.Vector3();
  },
  tick(_time, delta) {
    const presence = this.el.components["environmental-reactivity"]?.getRoomPresence(
      ROOM_KEYS.narrative,
    ) ?? 0;

    // Mutate only narrative-prefixed elements here.
  },
});
```

Then attach it to `<a-scene>`.

9. Add bootstrap call.

Call the room creation function inside the `DOMContentLoaded` bootstrap block:

```js
createNarrativeRoom();
```

10. Verify behavior.

Run:

```bash
npm run build
```

Then browser-check that:

- Existing rooms still appear unchanged.
- Existing project counts are unchanged.
- New generated objects mount inside the correct root.
- Movement and hover interactions still work.
- No new response system mutates another room's classes.

## Future Extension Points

The current architecture intentionally leaves hooks for future work without implementing those features yet.

| Extension point | Current placeholder | Intended use |
| --- | --- | --- |
| External room content | `FUTURE_EXTENSION_POINTS.roomContentLoaders` | Load room/project data from JSON or CMS later |
| Project metadata | `FUTURE_EXTENSION_POINTS.projectMetadata` | Attach descriptions, credits, links, media, or tags |
| Spatial audio | `FUTURE_EXTENSION_POINTS.spatialAudioZones` | Add room-local ambience or proximity sounds |
| Hidden spaces | `FUTURE_EXTENSION_POINTS.hiddenSpaces` | Register discoverable spaces like `hidden-nook` |
| Branch navigation | `BRANCH_NAV_CUES` | Add paths, thresholds, and distant anchors for future rooms |

Keep these as extension points until the feature is intentionally designed and implemented.
