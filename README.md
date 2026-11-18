# Starlit — Bring Back the Stars

**The stars fell into your room. Pick them up. Put the sky back.**

A mixed-reality game for Meta Quest, built with IWSDK (TypeScript + ECS).
One clear idea, built to be judged in 90 seconds: your own room is the
game board, your hands are the controller, and every constellation you
restore visibly brings a band of stars back to the sky above you.

## Why this one can win

- **MR-first, not VR-with-a-garden.** Passthrough is the game: fallen
  stars scatter all over the player's real room — low, mid and high —
  so you turn, reach, crouch and walk. There is no locomotion system;
  your legs are the locomotion.
- **Scene understanding, used honestly.** When the headset has mapped
  the room, each fallen star lowers itself onto the real surface
  beneath it — your table, your shelf, your floor. Where no room map
  exists (VR, emulator), the stars hover where they fell. Progressive
  enhancement, never a blocker.
- **A session arc with a money shot.** Three constellations — The Seed,
  The Herald (colour-matching), The Heart (colour + drifting rings) —
  and a finale: a triple light pulse, a burst over the frame, and the
  full sky faded back in overhead, in your actual room.
- **Hands only.** Pinch to pick up a star (IWSDK GrabSystem), carry it,
  release it over its ring. A ghost guide teaches the loop in the first
  ten seconds; a hint returns after 20 idle seconds.
- **Complete, not a demo.** Scoring with combos, star ratings, best
  times, undo, big-targets accessibility mode, generative ambient audio
  (no audio files), persistent progress, and a new shuffled night after
  every finale.

## How to play

1. Open the page in Quest Browser, tap **Enter XR** on the panel.
2. Look around: fallen stars (glowing gems) are scattered around your
   room; the golden ring on the floor marks home base under the frame.
3. Pinch a star to pick it up. Carry it to the glowing frame and release
   it over a ring. From The Herald on, colours must match.
4. Complete all three constellations to bring the sky back.

Panel: Next / Replay Constellation, Undo, Sound, Big Targets.
Keys (desktop testing): `N` next · `P` previous · `R` replay · `U` undo · `M` mute.
URL: `?level=2` starts at The Herald, `?level=3` at The Heart.

## Tech notes

- `iwsdk.config.json`: XR mode `ar`, hand tracking + grabbing on,
  scene understanding on, locomotion off.
- One game system (`src/starlit.ts`) on two ECS components
  (`FallenStar`, `FrameSlot`). All visuals are procedural — zero
  external assets, zero licensing risk. Audio is generated Web Audio.
- Saves in `localStorage` (`starlit-save-v1`): per-constellation stars
  and best times, total score, skies restored, settings. The scatter
  seed derives from the completed-nights count, so every replayed
  night hides the stars somewhere new.
- The VR fallback is the same build: with no passthrough, the night
  dome shows and the returning-sky dome reads as the ceiling of stars.

## Verified (2026-11-17, IWSDK emulator, Quest 3 profile)

- Typecheck clean; production build passes (`dist/` ≈ 3.6 MB).
- Scene render valid; runtime console clean.
- Session starts as **immersive-ar**; hand input mode works.
- Full first constellation played end-to-end with scripted hands:
  stars grabbed from three different room positions (front-low,
  back-right, back-left-high), carried to the frame, placed —
  banner tracked 1/3 → completion: **"✦ The Seed restored"**, closed
  constellation lines, score and panel totals updated.
- Colour-match and undo code paths are shared with the Firefly
  Constellations build, where both were emulator-verified.

## Still to do before submitting

1. Deploy `dist/` to a public HTTPS host and open it once in a real
   Quest Browser.
2. One physical-Quest session: pinch comfort at the low scatter tier,
   reach to the high tier, tracking loss mid-carry.
3. Record the demo video (see `PITCH.md` — the script is written).
4. Create the Meta developer team (needs the public org name) if the
   competition requires store distribution.
