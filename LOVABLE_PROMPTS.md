# GymMaxx — Lovable prompts

Paste **Prompt 1** into a new Lovable project. When it's built and working, send the follow-up prompts one at a time.

> Lovable builds a **web app** (React + Tailwind). These prompts make it mobile-first and installable (PWA) so it feels like an app on a phone — good for testing with users. The native iOS/Android app (Expo) comes later, per PROJECT.md.

---

## Prompt 1 — App shell, design system, all core screens (mock data)

```
Build "GymMaxx", a mobile-first fitness web app for Thai men who want to change their physique — either lose fat (Shred mode) or gain muscle as a skinny beginner (Bulk mode). Core loop: scan upper body → score per muscle zone → find weakest zone → "Train it" workouts + Thai food plan → re-scan weekly.

TECH
- React + TypeScript + Tailwind + shadcn/ui, React Router.
- Mobile-first: content max-width 430px, centered on desktop, full-height screens, bottom tab bar.
- Use local state + mock data for now (no backend yet). Keep data in typed modules under src/data so we can swap to Supabase later.
- All user-facing text in Thai by default via a simple i18n (th.json + en.json) with a TH/EN toggle in the Me tab. Exercise names show Thai + English.

DESIGN SYSTEM (dark only)
- Colors: bg #0B0B0D, surface #16171A, surface-2 #1F2125, border #2A2D32, text #F5F5F7, text-muted #9BA1A8.
- Accent electric blue #3A8BFF (rings, highlights, active tab, links). Filled primary buttons #2563EB with white text (pressed #1D4ED8).
- Score colors: ≥80 #34D399, 60–79 #FBBF24, <60 #F87171. Mode badges: Shred #FF8A3A, Bulk #A78BFA.
- Fonts (Google Fonts): Kanit 600/700 for headings, IBM Plex Sans Thai 400/500/600 for body, Barlow Condensed 700 for big numbers (scores, timers, kcal).
- Radius: cards 20px, buttons 16px, chips full. Min tap target 48px. Primary button full-width 56px tall at the bottom of the screen.
- Icons: lucide-react, 24px, stroke 1.75. No emoji in UI.
- Never use the word "อ้วน". Kind body-type labels: ผอม, ผอมแต่มีพุง, สมส่วน, ทรง V, ไขมันสะสม.

ONBOARDING (one question per screen, progress bar, back button)
1. Welcome: "เปลี่ยนหุ่นให้เห็นผล ไม่ว่าจะเริ่มจากตรงไหน", a front-body muscle map SVG with a few zone score chips, [เริ่มเลย], "มีบัญชีแล้ว? เข้าสู่ระบบ".
2. Goal: cards — ลดไขมัน ให้กล้ามชัด (Shred) / เพิ่มกล้าม เพิ่มน้ำหนัก (Bulk) / ลดไขมันและเพิ่มกล้าม (Both).
3. Body: age, height (cm), weight (kg) steppers; experience: ไม่เคยเลย / เคยบ้าง / เล่นประจำ. Show live daily calorie estimate (Mifflin-St Jeor for men × 1.55; Bulk +300, Shred −400, never below 1,500).
4. Where + equipment: ฟิตเนส / ที่บ้าน / ทั้งสองที่; multi-select equipment (ดัมเบล, บาร์เบล, ม้านั่ง, เคเบิล, เครื่องเวท, บาร์โหน, ยางยืด, ไม่มีอุปกรณ์); days per week 2–6.
5. Scan intro: tips (good light, shirt off, arms relaxed), privacy note "รูปเก็บในเครื่องของคุณ ส่งไปวิเคราะห์แล้วลบทันที", PDPA consent checkbox required to continue, [สแกนเลย] and [ไว้ทีหลัง] (skip goes to Home).
6. Camera: use getUserMedia front camera with a dashed body-outline overlay and 3-2-1 countdown; allow file upload fallback. Then an "analysing" state with a scan-line animation and 4 checklist steps. For now return MOCK results.
7. Free result: animated score ring counting up (e.g. 64), "ศักยภาพ 86", body type, body-fat RANGE (e.g. 12–16%), zone breakdown (อก, ไหล่, แขน, หน้าท้อง, V-Taper, สมมาตร) shown BLURRED with a lock, a goal timeline card ("~12 สัปดาห์ ถึงกล้ามเพิ่ม +4 กก." + bottleneck), CTA to paywall.
8. Paywall: GymMaxx Pro features list; plans yearly ฿1,190 (≈ ฿99/เดือน, "ประหยัด 50%") and monthly ฿199. Closing it shows ONE exit offer: "ลด 42% ปีแรก" ฿1,190 → ฿690, with text explaining the discount is from the yearly price just shown. No fake timers. Both paths lead to Home (mock purchase).

MAIN APP — bottom tabs: แผนฝึก | อาหาร | หน้าแรก (center) | สแกน | ฉัน
- Home: streak pill, "Today's workout" card (name, # exercises, minutes, 3 thumbnails, [▶ เริ่มเลย]), calories-left mini ring, weakest zone card with [ฝึกเลย], next-scan countdown, challenges + Quick Hits row. Rest-day variant.
- Plan: tabs "แผนสัปดาห์นี้" (7-day strip, done/today/rest states, exercise list for selected day, weakest-zone tag) and "คลังท่า" (filter by muscle chips and by equipment, search).
- Exercise detail: demo that loops between start/end photos every ~1s, Thai + English name, chips (level, equipment, target), "ตรงกับจุดอ่อนของคุณ" tag when relevant, muscle map with primary/secondary highlight, 3 numbered steps, ✓ do-this vs ✗ common-mistake cards, [ฝึกท่านี้เลย]. Every exercise MUST have a demo; hide any exercise without images.
- Workout player: elapsed timer, exercise progress segments, demo, coach "Maxx" message bubble that changes by state (ready, mid-sets, resting, last 10 s, exercise done), set rows (set #, previous, kg, reps, ✓). Tapping ✓ starts a 90 s rest timer (+15 s, skip). Base the timer on timestamps so it survives tab switches. "เปลี่ยนท่า" bottom sheet offers alternatives for the same muscle with the user's equipment. Use the Screen Wake Lock API while a workout is active. Finish → Summary.
- Summary: badge pop animation, time / sets / total kg / PRs, PR list, muscles-trained map, streak +1, [กลับหน้าแรก], [แชร์].
- Food: big calorie ring + protein/carbs/fat bars, today's meals, Thai quick-add grid (ข้าวขาหมู, ข้าวกะเพราไก่, ข้าวมันไก่, โจ๊กหมู, ส้มตำไทย, นมจืด + กล้วย, 7-Eleven items…). Tapping a dish opens a portion sheet: ½ จาน / 1 จาน / พิเศษ (×0.5/×1/×1.3) plus add-ons (+ไข่ดาว +90 kcal, +ข้าวเพิ่ม +160 kcal). Portion choice is mandatory. Bulk mode shows "เติมอีก 500 kcal ง่ายๆ" tips; Shred mode shows lighter swaps.
- Scan: header "WEEK n · n SCANS", countdown to next scan (1 scan per 7 days), toggle ความคืบหน้า / รายละเอียด. Breakdown: score ring, body type, body-fat range, 6 zone bars with weakest marked, link to train it. Progress: week 1 vs latest side by side, per-zone deltas, weight and strength deltas, share card (photo can be hidden).
- Me: profile, goal/mode switch (Shred/Bulk changes calorie target, copy, and mode badge color), equipment, language toggle, coach voice on/off, subscription (with clear cancel instructions), privacy (delete all photos).

EXERCISE DATA
Load exercises from the public-domain free-exercise-db:
https://raw.githubusercontent.com/yuhonas/free-exercise-db/main/dist/exercises.json
Images: https://raw.githubusercontent.com/yuhonas/free-exercise-db/main/exercises/{images[i]}
Curate ~150 common gym + bodyweight exercises, map muscles to our zones (chest, shoulders, arms, abs, back, legs) and equipment to our Thai labels, and add Thai names/steps for the first 30 (others fall back to English).

Make every screen polished, consistent, and smooth on a phone. Respect prefers-reduced-motion.
```

---

## Prompt 2 — Accounts and saving data (Supabase)

```
Connect Supabase. Add email + Google sign-in (sign-in is optional until the paywall; onboarding answers are kept locally and saved on sign-up).
Create tables with row-level security so users only see their own rows:
profiles (goal_mode, birth_year, height_cm, experience, location, equipment[], days_per_week, language),
body_logs (date, weight_kg, waist_cm),
scans (created_at, overall, potential, body_type, body_fat_min, body_fat_max, zones jsonb, weakest_zone),
workouts (started_at, finished_at, plan_day, summary jsonb),
workout_sets (workout_id, exercise_id, set_no, weight_kg, reps, is_pr),
food_logs (date, food_name, portion, multiplier, kcal, protein_g, carbs_g, fat_g).
Replace mock data with these tables. Pre-fill each set with the user's previous numbers for that exercise. Compute streaks and PRs from real data. Never store body photos in the database or storage.
```

---

## Prompt 3 — Real body scan (AI)

```
Replace the mock scan with a Supabase Edge Function "scan":
- The app sends one front photo (resized to max 1024px, JPEG) plus goal mode, height and weight.
- The function calls an AI vision model and requires strict JSON: overall (0–100), potential (0–100), body_type (one of: ผอม, ผอมแต่มีพุง, สมส่วน, ทรง V, ไขมันสะสม), body_fat_min, body_fat_max, zones {chest, shoulders, arms, abs, v_taper, symmetry} each 0–100, weakest_zone, and a one-line Thai bottleneck.
- In Bulk mode zone scores emphasise size; in Shred mode, definition.
- Reject unusable photos (no person, body cut off, too dark) with a Thai retry message.
- Delete the photo immediately after analysis; keep only the scores. Store the API key in Supabase secrets.
- Enforce 1 scan per 7 days server-side; the client shows the countdown.
```

---

## Prompt 4 — Payments (web)

```
Add Stripe subscriptions for GymMaxx Pro: monthly ฿199 and yearly ฿1,190 in THB, plus the one-time first-year offer ฿690. Gate Pro features (zone breakdown, adaptive plan, weekly re-scans + compare, coach voice, challenges, smart food tips). Free users keep: onboarding, first scan overall score + body type + potential, full exercise library with demos, workout logger, calorie target, basic food log. Add Manage subscription / cancel in Me → Subscription.
```

---

## Prompt 5 — Feels like a real app

```
Make GymMaxx an installable PWA (manifest, icons, splash, offline cache for the exercise library and workout player). Add web push reminders: training day, scan ready, streak at risk (max 1 per day, user can turn each off). Add coach Maxx voice using pre-recorded Thai audio clips (placeholders for now) for: workout start, last 3 reps, rest start, 10 s left, new PR, finish — with mute and rep-count toggles. Add haptic feedback (navigator.vibrate) on set complete and workout finish where supported.
```
