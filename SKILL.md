---
name: blender-whitebox-previs
description: Create or audit Blender whitebox previs for shared-space multi-character staging, deliberate cinematic composition, complex camera movement, and physical action. Choose simple proxies or articulated humanoids by visible needs; ordinary dialogue uses text prompts without whitebox by default.
---

# Blender Whitebox Previs

First classify the shot and choose proxy detail using the routing rules below. Read [references/action-previs-standard.md](references/action-previs-standard.md) for physical interaction or action; do not impose its contact/force chain on composition-only shots. See [references/shot-routing.md](references/shot-routing.md) for shot routing and proxy-selection examples. A simple block scene can be sufficient for camera/layout control; it cannot demonstrate a rescue or fight without readable body action.
Create a playable Blender whitebox reference that controls changing space, motion, occlusion, timing, and camera movement. This is a standalone skill. Do not add its rules to a film-pipeline skill or invoke it as an automatic pipeline stage unless the user separately requests that integration.

## Activation boundary

Use this skill only when the user explicitly invokes `$blender-whitebox-previs` or explicitly asks for Blender whitebox/graybox previs, blocking simulation, action simulation, or camera simulation.

Do not use it merely because a project contains action scenes. Do not replace story development, asset design, final rendering, or ordinary prompt writing with this skill.

## Correct production stage

Build whitebox previs after these are stable:

- the story beat and action result;
- the approximate scene topology and scale;
- the participating characters, creatures, props, and vehicles;
- the intended generation-unit duration and aspect ratio.

Build it before the final production video prompt and before costly video generation. If a production prompt already exists, treat it as a draft and revise it after the whitebox passes.

## Decide whether a shot needs whitebox

Select by the control the shot needs, not only by action complexity:

| Shot need | Default route | What whitebox must establish |
| --- | --- | --- |
| Multiple characters sharing one space, with meaningful relative positions | `required / staging` | Spacing, facing, eyelines, foreground/background roles, occlusion and any entrances/exits; characters need not be fighting |
| A deliberate composition or strong authored camera idea | `required / composition` | Subject scale, camera height and lens, depth layers, negative space, framing geometry and reveal/hold timing; also applies to a single subject or empty environment |
| Complex camera movement plus multiple characters | `required / mixed` | Independent actor routes and camera/aim paths, timing, occlusion, parallax and continuity |
| Precise physical interactions, rescue, combat or mechanisms | `required / action` | Preparation, contact, force, reaction and visible result |
| Ordinary dialogue, facial close-ups or routine shot/reverse-shot with simple stable positions | `skip / text` | Text describes performance, eyelines, shot size and light; existing identity/location references may still be used |
| Simple walking, ordinary insert or atmosphere with no particular spatial/composition requirement | `skip / text` | Text and appearance references normally suffice |

Ordinary two-person dialogue does not become required just because two people are present. If its blocking, layered group arrangement, designed framing or moving camera is itself the requirement, route it to staging/composition/mixed instead. Similarly, an adjective such as "cinematic" alone is not a concrete camera idea: state the intended composition before building. If the user wants whitebox to explore composition, propose an explicit framing goal and build the useful comparison.

Record `required / optional / skip`, `mode`, one concrete reason, and the required fidelity of each visible object. For mixed shots, upgrade only the interacting actors/parts; do not give distant extras contact rigs. Do not build whitebox for every shot by default.

## Three-layer responsibility model

Keep the control layers separate:

1. Character reference images control identity, body proportions, hair, and wardrobe.
2. Environment reference images control location appearance, materials, weather, and lighting direction.
3. Whitebox video controls position, distance, action route, timing, contact, occlusion, and camera movement.

The text prompt states the verb chain, visible result, acting pressure, physical constraints, and what must not change. Never ask one reference layer to control all information.

## Output contract and semantic legend

Before building, write one explicit output contract for every generation unit:

- duration in seconds;
- frame rate and exact frame range;
- aspect ratio and pixel resolution;
- whether it is a continuous take, a loop, or one range from a longer shared timeline;
- required first-frame state and required final-frame state.

Keep these settings identical in the Blender scene, whitebox render, audit frames, and final-generation handoff. Do not silently reinterpret a 16:9 previs as a 2.39:1 production clip or change the frame rate after timing has been approved.

Create a small semantic legend whenever more than one visible role exists. Assign each proxy a stable color and name, then map it to an asset or role, for example `yellow / CHARACTER_A / character asset 01`. Use separate entries for foreground crowd, background crowd, creature, vehicle, and critical props. Colors are identifiers, not appearance instructions; final asset references control the real colors and design.

## Build method

### 1. Lock coordinates and scale

Choose a stable world origin, floor height, units in meters, screen direction, and named zones. Represent geometry that controls blocking OR composition: floors, walls, doors, stairs, platforms, rails, vehicles, large props, hazards, exits, foreground framing masses, skyline profiles and depth layers. Even non-contact geometry matters when it controls parallax, scale or silhouette.

Use real approximate dimensions. Do not decorate or texture the whitebox.

### 2. Match proxy detail to the information being controlled

- `Level A — layout/camera`: blocks, capsules, cylinders or simple silhouettes for architecture, distant crowd positions, occupied volume, spacing, camera passage and depth. Give human stand-ins credible height/width and a facing marker when needed. They prove layout only, not gait, pose or performance.
- `Level B — pose/silhouette`: readable articulated head, torso, upper/lower arms, hands, upper/lower legs and feet for foreground people, silhouette-driven composition, facing, walking gait, crouching, aiming, reaching, flying or bracing. A non-rigged posed low-poly mannequin is sufficient for a held pose; animate joints when the pose changes.
- `Level C — contact`: articulated/rigged proxies with explicit palm, foot, wing-root and prop contact targets for grappling, falls, weapon handling, handoffs, rescue carries, cable force or mechanism operation. Model fingers only if grip shape affects the visible action; no final skin, clothes or anatomy sculpting is required.

Choose levels per object AND shot, including hybrids such as gray block buildings + Level B foreground actors + Level A distant crowd + Level C hands at a rescue contact. Simplify an object's shape only while the target camera can still read every required fact. An over-the-shoulder composition needs a head/shoulder silhouette even if there is no contact. No cylinder may substitute for the bent spine, knees or reaching arms that define a rescue or dive. When subject scale changes during a shot, ensure the proxy stays readable at the closest relevant view.

### 3. Choose the build order by mode

- `staging/action`: establish shared coordinates and route nodes -> animate actor poses and required contacts -> inspect with a neutral verification camera -> refine the production camera. Mark starts, approach/contact, turns, exits, threat/safe lanes and prop positions as relevant. Declare framing intent early, but never hide failed action with camera movement.
- `composition`: state the framing goal -> block necessary geometry and subject silhouettes -> set camera height/lens/position -> compare useful compositions -> animate camera/aim or hold the designed frame -> inspect. Do not invent a fight, contact event or actor route merely to satisfy an action template.
- `mixed`: establish geography and composition intent together -> prove actor routes and interactions -> refine independent camera and aim paths -> check both composition and contact in the rendered shot.

The composition pass records subject prominence and screen position, foreground/midground/background, headroom/look room, negative space, camera height and perspective, occluders, reveal timing and the ending frame. The rule of thirds is an option, not a required aesthetic. Symmetry, asymmetry, compressed depth or a static wide shot are valid when motivated.

### 4. Key the action in time

For action units, define an occupied first frame, trigger, preparation, contact, reaction, visible result, and clean exit handle. For staging/composition units, define the initial composition, required hold/reveal or repositioning, and final composition; mark irrelevant contact fields N/A.

Use exact frame ranges at the chosen frame rate. A body cannot react before contact. Props cannot teleport. Preserve mass, traction, reach, joint limits, cable length, and fall direction.

### 5. Design one motivated camera path

The camera must serve the declared composition, reveal or action. State its start, target, path or fixed position, height, lens or field of view, and end state.

For curved, long, looping, or reveal shots, animate the camera position and its look-at target as separate controllable paths. Shape the camera route for travel and parallax; shape the target route for eyeline, reveal timing, and framing. Add only restrained low-frequency handheld drift after both paths are approved. A deliberate locked-off camera or timed hold is valid; distinguish intended stillness from accidental stalls in a moving-camera plan.

Avoid unintended frozen openings, redundant views, unmotivated orbits, random zooms, camera teleportation, and moves that cross the action axis without a motivated reset. A designed static composition needs no added motion to pass. Ensure the next segment can inherit the outgoing screen direction and subject positions.

### 6. Preserve continuity across clips

When one scene is split across multiple generated videos, animate it in one Blender scene and one continuous timeline. Export the required ranges as separate whitebox clips. Do not rebuild each clip from unrelated coordinates.

Carry forward character position, body orientation, prop ownership, injury state, mechanism state, and camera side.

## Deliverables

Unless the user requests a different scope, create:

- a versioned `.blend` source file;
- a playable whitebox render matching the production clip's duration, aspect ratio, and frame rate;
- start, middle, end, and mode-relevant audit frames (critical contacts for action; composition/reveal/occlusion moments for camera or staging);
- a short map of occupied space, relevant actor nodes, camera/aim path or fixed pose, and critical prop states;
- a handoff note mapping the whitebox clip to the final video prompt and numbered asset references.

For a model-generation handoff, package the references by function instead of presenting them as interchangeable images:

- the whitebox video controls camera, framing, route, event order, action timing, and occlusion;
- the first-frame image, when used, controls the opening composition and visual starting state;
- numbered character, environment, creature, vehicle, and prop images control appearance;
- the text prompt supplies the action verbs, performance, physical constraints, lighting behavior, effects, sound, and visible ending.

When a styled first frame is needed, extract the actual approved whitebox first frame and use it as the layout reference for image generation. Do not create an unrelated beauty frame whose geometry conflicts with the whitebox.

Whitebox exports are silent by default. Route arrows, camera paths, labels and split-screen checks belong in a separate review view; omit them from the model-facing clip unless explicitly needed and explained. Stable role colors may remain.

The render video is the model-facing reference. Keep the Blender project local for revision. Do not claim that a `.blend` file alone is a usable video-model reference.

## Prompt handoff

After approval, revise the production prompt from the whitebox evidence:

- name objects and roles briefly;
- write the verb chain and visible result precisely;
- preserve the whitebox route, contact order, camera path, and duration;
- attach character and environment references for appearance;
- state that the whitebox controls motion and blocking rather than identity or texture.

Include the semantic legend in the prompt handoff: identify which named or colored proxy each numbered reference replaces. Do not rely on upload order alone, especially in multi-character, crowd, or creature shots.

Do not make the prompt invent a second blocking plan. If the prompt and whitebox conflict, stop and reconcile them before generation.

## Revision routing

When a result is wrong, revise only the controlling layer:

- spatial, occlusion, contact, route, or camera error: revise the Blender whitebox;
- action wording, acting pressure, or visible-result error: revise the text prompt;
- face, body, wardrobe, creature design, materials, or color error: revise the asset reference;
- cross-clip drift: revise the shared Blender timeline and export ranges.

Change one variable class per iteration. Preserve earlier versions and never overwrite an approved `.blend` file.

If only the final angle, final framing, or end handle fails, revise only the final camera keys and re-export the affected range. Do not rebuild approved blocking or regenerate the entire scene without evidence that the underlying route is wrong.

## Approval gate

Before calling the whitebox final, inspect the actual timeline and rendered evidence. Confirm:

- the first frame matches the declared composition or reveal setup; intended stillness is allowed;
- staging/composition goals are visible through the target lens and framing, including scale, depth, eyelines and occlusion;
- physical actions, when present, have readable cause, contact and result;
- joints and hands are readable at important contacts, when applicable;
- no actor, prop, or camera teleports;
- screen direction and spatial continuity survive internal cuts and clip boundaries;
- camera movement or deliberate stillness matches the framing plan without accidental stalls or redundant repetition;
- the render duration, frame rate, and aspect ratio match the target generation unit;
- the Blender source, render, audit frames, and handoff note agree.

For loops or exact match transitions, verify numerically rather than by eye: compare the first and final camera transform, look-at target, focal length, relevant actor transforms, and prop states. For ordinary clips, compare the required final state against the next clip's starting state with the same fields.

If any item fails, keep the status as draft or review. Do not label it final.

## Mode-specific evidence and status

Before modeling, state `mode`, the shot's visible purpose, output settings, reference roles, object-level proxy choices, state_in/state_out, and a `camera_promise` (the fact or composition the viewer must see). Missing information only blocks the part of the work that depends on it; label assumptions and exploratory layout rather than silently inventing story, abilities or environment.

For action/contact units, follow the detailed [action standard](references/action-previs-standard.md). For composition/staging without interaction, do not require contact sockets, force analysis, a fall/reaction chain or moving actors. Judge the rendered composition and temporal plan instead. Simple proxies are valid when they establish the declared layout/camera information; translating two blocks cannot pass as a performed fight or rescue.

Use `DRAFT`, `REVIEW`, or `READY_FOR_PROMPT`. A successful Blender run alone does not prove that framing, movement or interaction communicates the shot. Inspect actual rendered evidence for the selected mode. Whitebox does not prove final materials, lighting, facial performance or generation-model reliability.
