# Day OS

One app for meds, food, gym, study (GATE/BITS lectures + revision) and skincare.
You tap **"I'm up — build my day"**. It asks what's already done, then plans the rest of the day up to lights out (23:00).

## Put it online (GitHub Pages)
1. Create a new repo, e.g. `day-os`.
2. Upload these 5 files to the repo root: `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`.
3. Settings → Pages → Source: `main` branch, `/ (root)` → Save.
4. Open `https://<username>.github.io/day-os/` in Chrome on the phone → ⋮ → **Add to Home screen**.

## Sync between phone and laptop
- The first device creates a private sync code by itself (Settings → Sync).
- On the second device: Settings → Sync → **Use a different code** → type the code once.
- Keep the code safe. A new phone just needs the same code.

### Firebase rule (one-time, only if Settings shows "Sync blocked")
Firebase console → project `gate-2027-d5fbf` → Realtime Database → Rules:

```json
{
  "rules": {
    "plans": {
      "$id": { ".read": true, ".write": true }
    }
  }
}
```
Nobody can list all plans; a plan can only be opened with its exact code.

## Rules the planner follows
Ideal day (from Daily_Timetable.docx):

| Time | What |
|---|---|
| 5:30 – 6:00 | Wake up · Thyroid tablet · fresh up + AM |
| 6:00 – 7:50 | Gym (travel 20 · warm-up 7 · exercise 50 · cardio 10 + shake · back 7:50) |
| 7:50 – 8:30 | Bath + breakfast (morning meds) |
| 8:30 – 22:00 | Study, with lunch 13:30 (afternoon meds) and dinner 19:30 |
| 19:15 | Wed & Sat only: buy chicken + curd |
| 21:00 | Night meds |
| 22:00 – 22:30 | Wind down · isabgol + milk · pack gym bag |

- Study is one block per gap (no 10-min breaks): 8:30–13:30, 14:00–19:30, 20:00–22:00 = 12h30. Max study per day is in Settings.
- Woke too late for the 6:00 gym? Gym moves to just before lunch, or a 40-min home workout if that doesn't fit either.
- "I'm up — build my day" re-plans from the time you tap it. "Perfect day" keeps the ideal timetable and fills lectures from right now.
- "Make today off": no gym, 2h light study.
All times and durations are editable in Settings (Morning gym start 00:00 = gym before lunch instead).

## Live — YouTube study stream (OBS)

Live tab = the remote. OBS overlay = this site with `?live=<sync code>` (Live tab → Connect to OBS → Copy). Browser Source, 1920 × 1080, above the camera.

- **Start studying** once. Then the timetable runs it: lunch and dinner come up on stream at their times (full screen or card), with a sound, even if the phone is asleep.
- The break stays until you tap **Resume studying**. Late → red **overtime**; early → green **time saved**.
- Stream shows **one lecture at a time** (subject + lecture). Tick it here or anywhere in Day OS → the next one shows.
- Style, position, size, colour, accent, background, break screen, sound and every item are in Live → How it looks on stream. Live preview at the top of the tab.
- Exams: GATE and BITS from Settings, plus any you add on the Live tab.
- The overlay only reads, and shows study info only — never meds, food, skincare or body data.
