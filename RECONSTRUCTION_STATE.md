# Portfolio reconstruction state

Canonical project: `C:/Users/阳逍/Desktop/作品集网页`
Stack: Vite + TypeScript + Three.js + GSAP + Howler (already installed).
Last clean checkpoint before audio integration: `2a0f9c8`.

## Shared-rail entrance — CURRENT (2026-10-03)

Supersedes both the staggered parking and serial-fall experiments below.
Live Omnicom inspection confirmed two overlapping groups: an outgoing array,
then a spaced helical procession driven by rail Y and group Y rotation. Cards
do not fly individually into slots. The user requests the opposite direction:
from above downward, ending in the existing compact portfolio helix.

Implemented independently in src/config/transition.ts and SpiralScene.ts:
21 outgoing array meshes + 21 rail meshes, sharing the same project textures and
plane geometry. The outgoing rig continues its scatter; a single unwrapped
phase drives rotation and downward translation of every incoming card. No
per-card delay, waiting, or individual landing. Quadratic pitch decay starts
with a loose procession and approaches the unchanged browsing spacing.
Unwrapped motion avoids a visible recycle jump during the entrance.

SPIRAL_ENTRY tunes duration (2.4 s + 5.6 s), exit overlap, lead steps and pitch.
Opacity ramps on the incoming rail complete offscreen. Outgoing cards finish
hidden; their extra materials are disposed together with the scene. Hover and
selection continue to target only interactive rail meshes.

Validation: test-entry-cascade.mjs now checks shared spacing, finite poses,
monotonic downward motion, deterministic reversal, outgoing disappearance and
exact final geometry. Tests and production build PASS (existing chunk warning).
Chrome: frames .60-.90 inspected; first incoming cards appear while the outgoing
array clears. Handoff to SpiralCard.update has zero position delta. Manual
reverse input interrupts from the current frame. Captures in Temp:
rail-loose-074.png, rail-loose-081.png. Visual timing still subject to user review.
Pre-change backup: Temp/portfolio-rail-before-eafc83257bcd42a6870677e48be3fd0d.
No original production code imported; unrelated page, audio and orb unchanged.

## Staggered scatter-to-spiral entrance — SUPERSEDED (2026-10-03)

User-requested motion change, authored directly without Antigravity or reference
runtime code. Supersedes the previous protected entrance timing/assembly only.
Stages 0-.58 and interactive spiral geometry stay unchanged. The same 21 meshes
leave their terminal scatter poses at staggered times in final wrapped helix
order, follow elevated cubic paths, then descend into their own final slots.
No group-wide drop, opacity swap, texture replacement, or second scene.

Tuning: SPIRAL_ENTRY in src/config/transition.ts; 2.4 s array/scatter followed
by 4.8 s cascade, stagger window .62, crest minimum 4.0, drop height 3.2.
SpiralScene.playEntrance owns the two-part GSAP timeline. Reduced-motion goes
straight to the final state. Manual interruption seeds the target from the
currently visible progress before applying wheel/touch input.

Checks: scripts/test-entry-cascade.mjs verifies all 21 distinct landing times,
finite poses, descending final approach, exact helix landing, opacity continuity,
stage boundaries, and deterministic reverse seeking. Typecheck/build PASS;
existing large-chunk warning remains. Desktop intermediate renders inspected:
Temp/entry-cascade-middle.png and Temp/entry-cascade-late.png. Runtime timeline
seeking confirms mesh identities stay unchanged and controls resume at progress 1.
This is a requested variation, not a claim of matching the reference animation.
Pre-edit source backup:
C:/Users/阳逍/AppData/Local/Temp/portfolio-entry-before-6f18bbbccca047a5bef9f5496e5cb9b6

## Audio integration (2026-10-02)

Reference: https://pacomepertant.com/
Confirmed: ambient loop 0.30; hover 1.00; click 0.50; spiral/list 0.40;
project opening 0.50; menu close 0.70; home/about navigation 0.25; orb reactions 0.20.
Tick 0.20 belongs to the About pointer sticker trail, not spiral wheel motion.

Our implementation: `src/core/SiteAudio.ts`; tuning/assets: `src/config/audio.ts`.
Default silent on every boot. Enter-with-sound and the sound button explicitly unlock
browser audio. No-sound entry never starts the environment. Muting stops short effects;
ambient resumes from its paused position. Background tabs stop effects and pause ambient.
Showreel temporarily pauses ambient to avoid masking video audio.

Protected: formed-array/scatter/spiral transition, camera, mesh transforms, scroll logic,
and their timing. No visual animation algorithms changed for this addition.

Local sound assets: `public/sounds/`. Publication rights are unverified; see ASSET-NOTES.md.
Final runtime dependency on reference production bundle: 0.
Build: PASS (`tsc && vite build`, 2026-10-02). Existing >500 KB bundle warning remains.
Chrome runtime checks: all 15 samples decode; sound entry starts click + ambient;
audio context running with nonzero analysed output (RMS 0.0526); no-sound entry
does not play audio; list/spiral, hover, menu open/close, and orb emit the expected
sample/volume. Muting leaves zero playing voices. Showreel pauses ambient and close
resumes it with exactly one loop voice. Existing transition reaches progress 1.
Subjective listening on the user's physical speakers has not been verified.

## Orb material reconstruction (2026-10-03)

Scope: header avatar and shared loader artwork only. Implemented directly by
Codex at the user's request; no Antigravity delegation.

Chrome DevTools MCP evidence on the live reference: the logo is a 75 x 75
Lottie-rendered SVG displayed at 64 x 64 CSS pixels. Its material consists of
two embedded raster layers (319 x 319 and 339 x 339), not a real-time WebGL
sphere. Vector eyes use overlay blending; the smile has a broad light-catching
rim and a narrower dark line. Desktop sphere silhouette is about 62.23 px.

Independent source: src/components/OrbArtwork.ts. Uses editable SVG light
fields in a common 0-100 coordinate system: warm left softbox, lime crest,
cyan right reflection, lower occlusion, asymmetric shadow pocket, faint bottom
rim. No original PNG, Lottie JSON, executable bundle, or remote orb resource
is imported. Colors and expression anchors: src/config/orb.ts.
Removed the small hard glints and eye-dot decals. Kept all controller IDs.
Did not change SiteOrb, its click audio/state machine, camera, scroll, or cards.

Verification: tsc + vite build PASS; existing >500 KB bundle warning remains.
Chrome screenshots inspected at matching 1440 x 900 CSS viewport / DPR 1,
plus a 390 x 844 small-screen viewport (44 px avatar).
Single normal click reached expression 1 after rendering resumed.
Deterministic GSAP completion checks passed sequence 1,2,3,0 with exactly one
visible mouth, seven interrupted rapid clicks settled at 3, hover tag open=1
and closed=0. Async in-page timing tests paused RAF in the diagnostic session;
these are not evidence for measured real-time 300 ms transitions.
Console error/warning check: none. Diff whitespace check: PASS.
Captures: C:/Users/阳逍/AppData/Local/Temp/orb-final-desktop.png,
orb-reference-desktop-matched.png, orb-final-mobile.png,
orb-reference-enlarged.png, orb-local-final-large.png.

Visual status: major light placement and silhouette improved; not pixel-exact.
The original baked material retains finer reflection/texture detail that our
analytic gradient approximation does not reproduce. Do not claim a 100% match.
Changes are in the working tree; original orb source is recoverable from the
previous Git checkpoint. Final original-production-bundle runtime dependency: 0.

## Expression refinement (2026-10-03, supersedes latched reactions)

Live reference click sampling confirmed transient reactions: a straight mouth,
a lower broad smile, and a low round mouth; the avatar returns to its default
smile by the 1500 ms capture. Previously our avatar stayed on the selected
expression indefinitely, with opaque white dot eyes and a specular dot in its
round mouth. This was a significant behavior and appearance mismatch.

Updated OrbArtwork.ts and config/orb.ts with independently drawn mouth shapes,
repositioned reaction eyes/mouths, consistent overlay eyes, and unified lip
highlight painting (no double-bright overlap at corners). Material is unchanged.
SiteOrb.ts now holds reactions for 0.65 s after the 0.30 s transition and then
animates to the resting smile. A new click cancels the old return callback.
Every non-target mouth fades during interruptions; destroy cancels the return.
The return is silent and preserves the existing click sound sequence.

Build PASS. Browser deterministic timeline checks: reactions 1,2,3,0 each show
one mouth and return to 0; interrupted transitions settle without extra mouths;
destroy clears the timer, animation, and DOM. Real-time browser sampling of our
GSAP motion was throttled in the diagnostic session, so precise elapsed timing
is not claimed. Reference/local enlarged expressions were visually inspected.
Evidence in Temp: orb-reference-reaction-options.png,
orb-reference-reaction-timing.png, orb-local-refined-faces.png,
orb-expression-final-page.png. All changes remain independently authored source.

All 15 previous local OGG files differed from the live reference SHA-256 hashes.
Replaced with byte-identical reference samples; original files preserved in Git
checkpoint `2a0f9c8` and `C:/Users/阳逍/AppData/Local/Temp/portfolio-audio-before-20261002`.
