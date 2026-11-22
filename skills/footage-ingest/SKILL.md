---
name: "footage-ingest"
description: "Gather shoot footage from phone, tablet, laptop and voice memos, sync external mic audio, match takes to script codes and build a keeper index. Works on copies only; never deletes originals."
---

# Footage ingest

Use after a content day when the owner says footage is coming, or asks to sort, match, sync or find keepers. Work on copies only. Never delete, move or overwrite originals.

## Placeholders

| Variable | Meaning |
|---|---|
| `{{OWNER_NAME}}` | Creator whose footage this is |
| `{{SHOOT_FOLDER}}` | Root folder for the shoot, e.g. `Studio Day MMDD` |
| `{{SCRIPT_SOURCES}}` | Where script text lives (teleprompter files, a production plan doc) |
| `{{PRODUCTION_PLAN_DOC}}` | Doc with the shoot list, status section and rush list |
| `{{MINOR_LOCATIONS}}` | Locations where minors may appear and releases are required |

## 0. Where the work runs

- **Device shell on the owner's computer:** do everything there, inside connected folders. Install tools once: ffmpeg (brew or winget) and `pip3 install sherpa-onnx numpy`. Stage a file into the cloud workspace only for viewing frames.
- **No device shell:** ask for attachments, or stage files one at a time. Each clip must stay under about 400 MB. A 4K clip longer than 2 minutes won't fit, so ask for a 1080p export.
- **Cloud workspace:** ffmpeg is there. Install the transcriber with `pip install sherpa-onnx numpy`. Get a whisper model from the k2-fsa sherpa-onnx GitHub releases (e.g. `sherpa-onnx-whisper-base.en`).

## 1. Collect into one inbox (the owner does this part)

Ask for everything in `{{SHOOT_FOLDER}}/_INBOX/`, one subfolder per source:
- `phone/`: phone camera clips, transferred by cable or a full-quality wireless transfer. Never multi-select from a cloud photo web UI, which can download at 720p.
- `tablet/`: tablet videos, especially takes where the mic was plugged into the tablet.
- `laptop/`: anything recorded on the laptop.
- `voice-memos/`: voice memo exports (.m4a).

Copy before touching anything. Mirror `_INBOX` into `ALL TAKES/` and work from there.

## 2. Inventory every file

For each file, record path, source folder, duration, creation time (`ffprobe -show_entries format_tags=creation_time:format=duration`), resolution, orientation (rotation tag), whether it has audio, and the audio channel count. Write it all to `_index/inventory.csv`. Flag anything under 3 seconds (an accidental tap), anything with no audio, and any 720p file (a bad export; ask for the original).

## 3. Transcribe

Run the sherpa-onnx whisper transcriber on every file with audio: 16 kHz mono, chunked at about 25 seconds, timestamps kept. Save `_index/transcripts/<file>.txt`. Voice memos and phone videos both get transcripts, because the transcript is how files get paired and matched.

## 4. Pair the mic audio with its video

When the mic recorded separately while the phone filmed, the video's own audio is a scratch track. Pair them:
1. Candidates: audio files whose creation time falls within about 2 minutes of the video's, and whose transcript overlaps it. Match on the first 10 words, and the slate if one was spoken.
2. Find the offset by cross-correlating the audio envelopes: numpy FFT, 8 kHz mono, absolute value, mean removed. A score above about 0.3 is a match. A positive offset means the mic started after the camera.
3. Mux into `SYNCED/`: `ffmpeg -i video -itsoffset <offset> -i mic -map 0:v -map 1:a -c:v copy -c:a aac -shortest out.mov`. Keep the scratch track out.
4. Spot-check each synced file. Pull 3 frames mid-word and compare with the transcript timing. Drift over about 1 frame on a long take means a sample-rate mismatch, so resample the mic with `-af aresample=async=1`.
5. Any video with no mic match keeps its own audio. Mark it `mic=none` in the index.

## 5. Match to script codes

Script text lives in `{{SCRIPT_SOURCES}}`. For each take:
- If a slate was spoken ("TEA one, take two"), use it. It wins over everything else.
- Otherwise, fuzzy-match the transcript against every script's lines (word overlap on the hook and first two lines). Accept the best match only if it clearly beats the runner-up. Otherwise mark it `UNMATCHED`.
- A take where the speaker says "scrap" is never a keeper.
- The keeper is the newest take of a code with no "scrap" in it that runs through the last line. If the newest take is cut short, use the newest complete one.
- Freestyle footage (b-roll) has no code. Tag it `BROLL-<place>-<subject>`, or `FREE-<topic>` from the transcript.

## 6. Name and file the keepers

Copy keepers to `KEEPERS/` as `MMDD_CODE_T#.mov` (e.g. `1119_TEA-01_T2.mov`). Use the synced version when one exists. B-roll goes to `ROLL/`, stills to `STILLS/`, behind-the-scenes clips to `BTS/`. Originals stay in `ALL TAKES/`.

## 7. Report back

Write `_index/keepers.csv` with columns: code, title, keeper file, take, duration, source device, mic (synced / own / none), match method (slate / text), confidence, notes. Then give a short summary:
- Counts: scripts with a keeper, takes that need human eyes (UNMATCHED or low confidence), and files that look broken.
- Scripts on the shoot list with no take at all, compared against `{{PRODUCTION_PLAN_DOC}}`.
- Anything time-sensitive from the plan's rush list.

Update the production plan's status section with what's confirmed shot, replacing its exact lines. Hand keepers to the video-review skill for a quality pass.

## Rules

- Nothing is deleted, ever. Anything to remove goes in `_to_delete/` with a list.
- Don't send or post anything.
- Non-English transcripts from an English model are unreliable. Match those takes by slate or timing, and flag their captions for a fluent human to check.
- Minors may appear at `{{MINOR_LOCATIONS}}`. If a face, name tag or voice appears, flag it, and never put it in KEEPERS without confirmation that a release exists.
