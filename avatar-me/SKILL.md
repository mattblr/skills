---
name: avatar-me
description: Design and build a personal animated avatar family from the logos, colours, and visual assets in a codebase. Use for branded user avatars or an app mascot, including deterministic username variants and signature motion. Produces a standalone component in the project's own stack.
---

# avatar-me

Make an avatar that belongs to this project. Use its existing visual language to find a character, then build an independent component the team can maintain.

## Find the character

Inspect the repository's instructions, framework, UI primitives, logo assets, existing avatars, and colour tokens. Trace the assets actually used by the app; an old export in a folder may not represent the current brand. Reuse existing tools and animation dependencies where they fit.

Identify a few specific traits to carry into the character: perhaps a repeated shape, an asymmetric corner, a cutout, or the way two parts overlap. Keep the approved colours recognisable. A face is optional. Avoid automatically adding eyes, eyebrows, limbs, gradients, or a smile to every logo.

Show two or three small concepts with an idle silhouette and one revealing pose. Use SVG or a local component preview when possible; ASCII is useful for formation and layering. Explain which brand detail each concept uses. Follow the user's existing direction when they have already chosen one. Keep the original logo intact unless changing it is part of the request.

The [Ormitar case study](references/ormitar.md) describes how overlapping characters grew out of a four-dot logo. Read it when layered parts or hidden companions would suit the brand. It is an example, not a template to reproduce.

## Give it a reason to move

Start with a recognisable resting pose and a small set of states that the product needs. Define the trigger, movement, duration, and return pose for each state. Distinguish a user identity from its temporary expression: success or thinking should not generate a new avatar.

Suggest a few signature moves from [motion ideas](references/motion.md), adapted to the discovered geometry. Pick one main gesture. Keep idle motion sparse enough to sit next to text, and use larger reactions for deliberate events. Gaze can follow a nearby pointer with bounded travel; it should settle when the pointer leaves. Touch users need a useful resting character without cursor input.

For overlapping parts, draw the back-to-front order and check both endpoints and the transition between them. Hidden companions must be concealed at rest. Separate transform wrappers for formation, local motion, and facial movement so one does not overwrite another. Keep all poses inside the allotted space unless the host explicitly provides a movement area.

## Build it in the repository

Generate original SVG or other code-native geometry in the project's framework. The result must run without Ormitar, Blobatar, or this skill. Study existing components for conventions; do not copy a private library into a public package or silently add an avatar dependency. Use the project's styling system, including Tailwind where it is established. Keep bespoke keyframes close to the component if the framework needs CSS for them.

Use a stable seed, such as a user ID or username, to select bounded variations in silhouette, colour, proportions, or expression. Choose and document a normalisation rule that fits the app's identity rules. Keep each trait separately seeded so adding one does not change every existing avatar. Rendering the same seed must agree on the server and client; avoid random values, time, or browser state during initial render. Version the identity scheme before changing it after release. Distinct seeds can still produce similar avatars, so do not promise collision-free visual identities.

Expose only useful controls for the chosen design. Typical inputs are a seed, size, state, motion preference, and an accessible label. Keep identity generation local; rendering an avatar should not call an image model or send usernames to an external service.

Respect reduced-motion preferences and an explicit motion-off option. Preserve the useful final pose when animation is disabled. Pause continuous work when hidden or offscreen, clean up observers and listeners, and avoid one global pointer listener per avatar in a large list. Decorative avatars should be hidden from screen readers; meaningful avatars need a name. Communicate application status in text as well as motion.

## Try it where it will live

Build a small preview with a seed input, several identities, state controls, and a still mode. Inspect it at the actual avatar size and at mascot size, against the app's backgrounds. Check clipping, overlaps, small-size legibility, repeated seeds, reduced motion, and pointer behaviour. For repeated SVG instances, keep mask and clip IDs unique without introducing hydration differences.

Run checks appropriate to the implementation, including deterministic identity and state transitions where tests add confidence. Use real browser inspection if available. Report what was inspected and any unverified behaviour. Deliver the component, a usage example, and the reason for its signature gesture. Keep demo copy plain and specific.
