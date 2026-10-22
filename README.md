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
- Thyroid tablet first, no food for 60 min.
- Breakfast only if food is allowed by 11:00. Morning meds ride on breakfast, else on lunch, else on dinner.
- Lunch 13:30, never after 14:30. Dinner 19:30. Lights out 23:00.
- Outside gym (90 min with travel) always before lunch. If it can't fit before 14:30 lunch → 40 min home workout, 2h after a meal.
- Everything else is study, in 90-min blocks with 10-min breaks: revision first, then lectures. A long lecture can stop mid-way; the rest continues tomorrow.
- "Make today off": no gym, 2h light study.
All times and durations are editable in Settings.
