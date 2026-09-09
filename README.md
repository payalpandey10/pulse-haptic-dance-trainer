# Pulse — Haptic Rhythm Trainer

A browser-based rhythm training tool that helps hearing-impaired dancers feel and practice timing to music through vibration and camera-based movement tracking — not just listen to it.

## The Problem

Deaf and hard-of-hearing dancers currently rely on standing near speakers or dancing on vibrating floors to sense music. This works for *feeling that music is happening*, but gives no way to know *how accurately* you're syncing to the beat, and requires specific equipment/rooms. Existing haptic tools (like haptic suits or vibration apps) are built for passively experiencing music at concerts — none are built as a **practice tool with feedback**, the way a hearing dancer might tap their foot and self-correct.

## What This Does

Pulse turns a song's rhythm into vibration and visual pulses, then scores how accurately you sync to it — either by tapping (Trainer mode) or by dancing in front of your camera (Dance mode).

### Trainer Mode
- Load any mp3
- The app analyzes the audio and finds every beat's exact timestamp
- Your phone vibrates (and the screen pulses) on each beat
- Tap along, and get scored: average timing offset (ms) and % of beats matched
- Session history tracks improvement over time

### Dance Mode
- Uses your camera and MediaPipe pose detection to track your wrists in real time
- No tapping needed — dance naturally, and a sharp arm movement is detected as your "hit"
- Same scoring engine compares your movement timing against the real beat

## Tech Stack

- **Frontend:** Vanilla HTML/CSS/JavaScript (no framework) — single self-contained files
- **Audio analysis:** Web Audio API + a custom energy-based beat detection algorithm
- **Haptics:** Vibration API (`navigator.vibrate`) — Android Chrome only, iOS Safari has no support
- **Pose tracking:** [MediaPipe Pose Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) (Google, runs entirely client-side)
- **Hosting:** GitHub Pages (HTTPS required for camera access)

No backend, no database, no external paid APIs — everything runs in-browser. This was a deliberate choice: it works offline-first (aside from initial model load), requires no server costs, and avoids sending any camera data off-device.

## Files

| File | What it is |
|---|---|
| `step3_full_app.html` | The complete, current app — beat detection, Trainer mode, and camera-based Dance mode |
| `haptic_rhythm_trainer.html` | Earlier prototype — beat detection + vibration + tap trainer only |
| `step1_pose_tracker.html` | Isolated test: camera + MediaPipe skeleton overlay |
| `step2_hit_detection.html` | Isolated test: wrist hit-detection tuning (with live debug readout) |

**Use `step3_full_app.html` — that's the current, working version.**

## How to Run It

1. Open `step3_full_app.html` via the hosted GitHub Pages link (camera access requires HTTPS, so opening the file directly won't work for Dance mode):
   ```
   https://payalpandey10.github.io/pulse-haptic-dance-trainer/step3_full_app.html
   ```
2. Upload an mp3 file
3. Click **Analyze beats**
4. Choose **Trainer** (tap along) or **Dance** (enable camera, then move naturally)
5. Click **Play**
6. Your score appears after the song ends or you click Stop

## Possible Future Work

- Backend + database for saving progress across sessions/devices
- Tempo-adaptive beat detection tuning per genre
- Full-body movement tracking (not just wrists) for richer choreography feedback
- Community-contributed song library with pre-analyzed beat maps

## Why This Matters

Existing haptic tools help someone feel that music is happening. This is built to help someone train and measurably improve their timing against it — solo, anywhere, without needing a hearing teacher in the room to say "you're a little late."
