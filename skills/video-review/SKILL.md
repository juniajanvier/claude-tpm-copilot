---
name: "video-review"
description: "Watch a video frame by frame with its transcript and give producer-style notes on delivery, framing, light, sound, captions and pacing, with timestamps and a Post / Fix / Reshoot verdict."
---

# Video review

Use when asked to review, check, watch, critique or pick between takes, or for a pre-post QA pass on an edit. The goal is to actually look at the picture and listen to the words, not just read a transcript.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{CREATOR_NAME}}` | Person on camera |
| `{{CREATOR_PERSONA}}` | One line on how they should come across (e.g. "polished, warm, credible educator") |
| `{{GESTURE_CUES}}` | Gesture cue words used in scripts (e.g. COUNT, PALMS, WEIGH) |
| `{{REQUIRED_END_CARD}}` | Compliance text required on certain pieces (e.g. brokerage, license jurisdiction, Equal Housing Opportunity) |
| `{{SELF_CHECKED_LANGUAGES}}` | Caption languages the creator checks personally |
| `{{MINOR_LOCATIONS}}` | Locations where minors may appear and releases are required |

## 1. Get the file

Prefer the original over a screen recording. Copy it into a fresh folder and never edit the original. Check it with ffprobe: duration, resolution, fps, rotation, audio streams.

## 2. Build what you'll look at

Use ffmpeg. Keep images small enough to read many of them.
- **Overview contact sheet:** one frame every 2 seconds (every 1 second for clips under 20 seconds, every 4 for long talks), scaled to 320 px wide, tiled 5 wide. `ffmpeg -i in -vf "fps=1/2,scale=320:-1,tile=5x4" sheet_%02d.jpg`. Burn in timestamps with `drawtext=text='%{pts\:hms}'` so every note can cite a time.
- **Cut and scene frames:** `select='gt(scene,0.3)',showinfo` finds every cut. Grab the frame before and after each one.
- **Close looks:** full-resolution frames at the hook (0 to 3 seconds), at every caption change, at the last second, and at anything suspicious. A face at 1080p is where focus, skin tone and eyeline get judged.
- **Frame by frame:** for the first 3 seconds, and around any cut or gesture that matters, extract every frame (`-vf fps=30` over that window) and look at them in order. That catches a blink on the first frame, a late cut or a lip-sync slip.
- **Audio:** transcribe with timestamps (sherpa-onnx whisper). Also run `ebur128` for loudness (about -14 LUFS integrated for Reels), `silencedetect=n=-35dB:d=0.6` for dead air, and `astats` for clipping.

Read every sheet, then the close frames.

## 3. Review against the standard

`{{CREATOR_NAME}}` should read as `{{CREATOR_PERSONA}}`.
- **Hook (0 to 3 s):** text on screen in the first second, eyes in the lens, energy up, no dead frame or slate left in. Would a stranger stop scrolling?
- **Delivery:** eye contact with the lens rather than reading, natural pace, gestures that match the cue (`{{GESTURE_CUES}}`), smile where the script smiles, no trailing "um" or a glance at the screen right before a cut.
- **Framing:** chest-up, eyes on the top third. Face inside the Reels safe zone, clear of the top 250 px, the bottom 400 px and the right 120 px. Nothing distracting at the edges. Horizontal for application videos, vertical for Reels.
- **Light and skin:** skin tones read rich and true, not gray. No blown highlights, no hot spot, no mixed color temperature, no exposure pumping on a white wall.
- **Sound:** lav audio, no echo, no clipping, no rustle from jewelry or fabric, consistent level between cuts.
- **Edit:** jump cuts every 2 to 4 seconds on talking heads, a pattern break around 2 to 4 seconds and again near 7. Captions match the words exactly, especially in `{{SELF_CHECKED_LANGUAGES}}`. Correct end card, with `{{REQUIRED_END_CARD}}` where required.
- **Facts and guardrails:** every number and claim matches the approved script and its verify note. No minors' faces at `{{MINOR_LOCATIONS}}` without releases. No employer-internal details. Fair housing language describes homes, never who a home is for. Political pieces describe outcomes only.
- **Application videos** (conference or speaker submissions): one continuous take, no cuts, within the length limit, slate and walk-back trimmed. Judge presence above all.

## 4. What to hand back

Open with a verdict line: **Post it**, **Fix and post** or **Reshoot**. Then:
- **What works:** 2 or 3 specifics with timestamps.
- **Fixes:** ordered by impact. Each gets a timestamp, the problem and the fix (e.g. "0:07 eyes drop to the prompter before the cut, so trim 6 frames earlier").
- **Captions and facts check:** any mismatch between the words, the captions and the script.
- **Pick of takes:** when comparing takes, a side-by-side of the hook frames and which one wins and why.

Attach the contact sheet or key frames when a picture makes the note clearer. Tone of a trusted producer: direct, specific and kind.

## Limits to say out loud

The review comes from sampled frames plus the full audio. Very fast motion between sampled frames can be missed, so say which windows were checked frame by frame. Non-English captions need a fluent human ear. Nothing gets posted or sent from this skill.
