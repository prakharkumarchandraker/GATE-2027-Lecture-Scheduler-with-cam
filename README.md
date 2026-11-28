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
| 7:00 – 7:30 | Wake up · Thyro (Levothyroxine) · fresh up + AM |
| 7:30 – 9:40 | Gym (travel 20 · warm-up 15 · exercise 50 · cardio 15 + shake · back 30 incl. chicken + curd) |
| 9:40 – 10:20 | Bath + breakfast · Med2 at 10:30 (Addwise OD 18 · Vortioxetine 10) |
| 10:20 – 22:30 | Study, with lunch 14:00 (all 300 g chicken · Addwise OD 18) and dinner 20:00 (rice + dal) |
| 21:30 | Med4 (Omega 3 · Magdep CM · Vortioxetine 10 · Rozavel 10) |
| 22:30 – 23:00 | Wind down · isabgol + milk · pack gym bag · lights out 23:00 |

- Study is one block per gap (no 10-min breaks): 10:20–14:00, 14:30–20:00, 20:30–22:30 = 11h10. Max study per day is in Settings.
- Woke too late for the 7:30 gym? Gym moves to just before lunch, or a 40-min home workout if that doesn't fit either.
- "I'm up — build my day" re-plans from the time you tap it. "Perfect day" keeps the ideal timetable and fills lectures from right now.
- "Make today off": no gym, 2h light study.
All times and durations are editable in Settings (Morning gym start 00:00 = gym before lunch instead).

## Changes 27 Nov 2026
- **Swap fix**: once the lecture you swapped in is ticked, the original lecture comes back today (e.g. swap Maths Lec 1 for a C lecture → tick C → Maths Lec 1 shows, not Lec 2).
- **Lecture order ↑ ↓**: every not-done lecture in today's plan has ↑ ↓ to do it earlier or later (e.g. C before Maths). Reset from *Today's changes*.
- **Top bar: Timetable · Diet · Skincare** buttons. Timetable shows the whole ideal day with the section you're in right now highlighted (NOW) and time left.
- **New meds** (Beta gone, Addwise split): 7:00 Thyro · 10:30 Addwise OD 18 + Vortioxetine 10 · 14:00 Addwise OD 18 (with lunch) · 21:30 Omega 3, Magdep CM, Vortioxetine 10, Rozavel 10.
- **New skincare** (25 Nov sheet): Derma Co Kojic face wash (then Dot & Key Mango, then Plum) · Chemist at Play for neck + body (then Dove) · Vaseline Gluta-Hya SPF 50 all over after bath · Re'equil SPF on face · night ends with lip balm (no Noswet).
- Study time checked against the timetable: 10:20–14:00 + 14:30–20:00 + 20:30–22:30 = 11h10.

## Changes 22 Nov 2026
- **Perfect day ⇄ I'm up**: after picking one, the Today tab has *Switch to Perfect day* / *Switch to I'm up — re-plan from now* and *Start over* (pick again). Ticks stay.
- **Study vs non-study colours**: study blocks blue, everything else beige, skipped slots grey.
- Every non-study block: **Skip** (asks what you'll do there instead, editable) or **Make this study** (that time is added to today's study). Reminders (meds, snack, shopping) have a small *skip*. All undoable from the timeline or the *Today's changes* card.
- **Lecture swap**: *swap ⇄* on any lecture → pick any other lecture (any subject) to watch today instead, or just move it to a later day. The swapped-out lecture comes back from tomorrow in its normal place.
- **Study only** button: shows only the study timetable. **Hide…** lets you hide any part of the Today tab (separate lists for normal and Study-only view), incl. the floating Now box.
- Floating Now box has an ✕ (bring back: Settings → Reminders). Water reminder: *Skip this one* and *No water reminders today*.
- Courses tab: **Apply recommended GATE order** (A: C → DS → Algo → OS → DBMS → TOC → CD · B: DLD → CO → CN · side: DMS sets/logic first + Aptitude · maths: LA, Prob, Calculus), plus tags per subject (marks/hour, length) and prerequisite warnings.

## Focus mode
Top bar → **Focus**: full-screen dark screen with a big clock, what the timetable says right now (with time left), the current lecture with a ✓ button, any med or meal due now, and what's next. Screen stays awake. Esc or ✕ Exit to leave.

## Reminders (Settings → Reminders)
- **Water**: full-screen reminder with sound every N minutes (0 = off), from wake-up to wind-down. "Drank a glass" adds to the water count; "Snooze" asks again in 5 min.
- **Timetable alarm**: the moment each item starts (study, meals, gym, meds, e.g. 19:30 Dinner) → full-screen alert with a loud sound, repeating every 8 s until you tap OK.
- **Now box**: floating on every tab — clock, what the timetable says now and how long is left, the next item, and the first unticked lecture with a ✓ button. ▾ shrinks it.
- Test buttons for both alerts. Optional phone / desktop notifications.
- Works while Day OS is open in a tab or window. A locked phone can hold sounds back.

## Live — YouTube study stream (OBS)

Live tab = the remote. OBS overlay = this site with `?live=<sync code>` (Live tab → Connect to OBS → Copy). Browser Source, 1920 × 1080, above the camera.

- **Start studying** once. Then the timetable runs it: lunch and dinner come up on stream at their times (full screen or card), with a sound, even if the phone is asleep.
- The break stays until you tap **Resume studying**. Late → red **overtime**; early → green **time saved**.
- **Today's log** (Live tab) lists every study stretch and break with times; the stream card shows studied time, breaks (count · time) and saved / over.
- Stream shows **one lecture at a time** (subject + lecture). Tick it here or anywhere in Day OS → the next one shows.
- Style, position, size, colour, accent, background (also used by the full-screen break), break screen, sound and every item are in Live → How it looks on stream. Live preview at the top of the tab.
- Exams: GATE and BITS from Settings, plus any you add on the Live tab.
- The overlay only reads, and shows study info only — never meds, food, skincare or body data.
