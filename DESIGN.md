# GymMaxx — Design (UX/UI)

> Status: v0.1 draft · Platform: iOS + Android (one codebase) · Language: Thai first, English second

This document is the design source of truth for GymMaxx: who it is for, how users move through it, what every core screen does, and the visual system it is built with.

---

## 0. Decisions (v1)

| Topic | Decision |
|---|---|
| Visual style | **Dark premium** — black background, bold big numbers, one bright accent |
| Accent colour | **Electric blue** `#3A8BFF` |
| Main audience | **Mostly men** (Thai, beginners + gym-goers). Women's scan zones possible in a later version |
| Coach | **Voice coach "Maxx"** — Thai male voice, counts reps, can be muted |
| Home screen | **Today's workout first**, then streak, calories left, weakest zone |
| Paywall | **After the free score** — overall score + body type free, breakdown blurred |
| Body scan | **Front photo only** |
| Language | **Thai default + English toggle**; exercise names shown in both |

## 1. Product in one line

**"Whatever your starting point, GymMaxx shows you how to change your body — and lets you see it happen."**

GymMaxx is a Thai-first physique app. The user scans the upper body, gets a score per muscle zone, learns the one thing holding them back, and follows a plan (workouts + Thai food) built to fix it. A weekly re-scan shows progress.

## 2. Design principles

1. **One loop, always visible.** Scan → score → weakest zone → *Train it* → re-scan. Every screen points to the next action.
2. **Thai first.** Thai copy, Thai food with Thai portions, Thai-speaking coach. English is a toggle, not the default.
3. **Beginner clarity.** Every exercise answers three questions: *what muscle, what equipment, how to do it* — with a demo. No exercise ships without a demo.
4. **Progress vs. yourself, never vs. others.** No rankings, no shaming words. A low score is shown next to a *potential* score.
5. **Two goals, one app.** *Shred* (lose fat) and *Bulk* (gain muscle, for skinny users) share the same screens but change targets, wording and accent colour.
6. **Honest by default.** Discounts are calculated against prices the user has seen. Body-fat is a range. Photos are private.
7. **Works mid-workout.** Big tap targets, screen stays awake, timer keeps running in the background and on the lock screen.

## 3. Who it is for

| | **A · "Bulk" — skinny beginner** | **B · "Shred" — losing weight** | **C · Gym regular** (secondary) |
|---|---|---|---|
| Example | University student, 20, 175 cm / 56 kg | Office worker, 29, 170 cm / 84 kg | Trains 3–4×/week for 1+ year |
| Wants | Bigger shoulders, chest, arms | Lose the belly, see abs/arms | Track progress, break plateaus |
| Pain points | "ต้องกินกี่ cal ถึงจะ muscle ขึ้น", can't eat enough, scared of the gym | Slow scale, no idea what to eat, embarrassed to start | Bored of logging in Notes, no visual progress |
| Biggest fear | Looking clueless at a machine | Being judged for their body | Wasting time |
| Design response | Equipment guide, eat-more food tips, size-focused score | Optional/private scan, definition-focused score, kind copy | Fast logging, strength charts, physique score |

## 4. Core loop

```mermaid
flowchart LR
    S[สแกน<br/>Scan upper body] --> R[คะแนน + จุดอ่อน<br/>Score & weakest zone]
    R --> T[ฝึกจุดนี้<br/>Train it]
    T --> W[เวิร์คเอาต์ + อาหาร<br/>Workouts + food]
    W --> P[ความคืบหน้า<br/>Streak, muscle map]
    P -->|7 days later| S
```

Re-scan is limited to **once every 7 days** (countdown on the Scan tab). This creates a weekly ritual and keeps comparisons meaningful.

## 5. User journey

| Stage | User is thinking | Touchpoint | Feeling | Risk | Design response |
|---|---|---|---|---|---|
| **1. Discover** | "สแกนกล้ามได้กี่คะแนนนะ?" | TikTok slideshow / creator | Curious | Ad feels fake | Real Thai before/afters, honest claims |
| **2. Install & open** | "Is this another English app?" | Store page, splash | Unsure | Bounce | Thai screenshots, Thai first screen |
| **3. Onboarding** | "Get to the point" | 10–12 quick questions | Engaged → impatient | Too long (AbMaxx review: "took a while") | Progress bar, one tap per screen, ~90 seconds total |
| **4. First scan (aha)** | "What's my score?" | Camera + result | Excited / nervous | Low score → quits, body shame | Scan is optional; show *potential* next to score; kind body-type labels |
| **5. Paywall** | "Is this worth it?" | Paywall + one exit offer | Sceptical | Fake discount → "scam" review | Price in ฿ with monthly equivalent, honest %, free tier still useful |
| **6. First workout** | "How do I use this machine?" | Workout player | Unsure → proud | Confusion, timer stops | Demo on every move, background timer, finish badge |
| **7. Week 1** | "Am I doing enough?" | Home, food log, streak | Motivated | Food logging friction | Thai quick-add with portions, daily target ring |
| **8. Week 2 re-scan** | "Did anything change?" | Compare view | Proud (or flat) | No visible change → churn | Show strength, waist and weight wins too, not only the photo score |
| **9. Month 1+** | "I'm actually changing" | Share card, phases | Confident | Plateau, boredom | New phase, new challenge, share card |

## 6. Onboarding

Target: **under 2 minutes to first score.** One question per screen, a progress bar, back button always available. Each answer visibly personalises something later ("เราจะใช้ข้อมูลนี้คำนวณแคลอรี่ของคุณ").

```mermaid
flowchart TD
    A[1 Welcome] --> B[2 Goal: Shred / Bulk / Both]
    B --> C[3 Sex + age]
    C --> D[4 Height + weight]
    D --> E[5 Experience level]
    E --> F[6 Where you train + equipment]
    F --> G[7 Days per week + session length]
    G --> H[8 Focus areas]
    H --> I[9 Building your plan...]
    I --> J{10 Scan now?}
    J -->|Yes| K[11 Privacy + pose guide]
    K --> L[12 Camera with pose outline]
    L --> M[13 Analysing]
    M --> N[14 Result: score, type, potential]
    J -->|Later| O[14b Plan preview without score]
    N --> P[15 Goal timeline]
    O --> P
    P --> Q[16 Paywall]
    Q -->|Close| R[17 One honest exit offer]
    Q --> S[18 Notifications permission]
    R --> S
    S --> T[Home]
```

| # | Screen | Content / copy (TH) | Notes |
|---|---|---|---|
| 1 | Welcome | "เปลี่ยนหุ่นให้เห็นผล ไม่ว่าจะเริ่มจากตรงไหน" · [เริ่มเลย] · Sign in | Short looping clip of a Thai body transformation |
| 2 | Goal | "เป้าหมายของคุณคืออะไร?" · **ลดไขมัน ให้กล้ามชัด** (Shred) · **เพิ่มกล้าม เพิ่มน้ำหนัก** (Bulk) · **ลดไขมันและเพิ่มกล้ามไปพร้อมกัน** (Both) | Sets mode + accent colour for the whole app |
| 3 | Sex + age | Two pickers | Needed for calorie maths |
| 4 | Height + weight | Wheel pickers, cm / kg | |
| 5 | Experience | "เคยเล่นเวทมาก่อนไหม?" · ไม่เคยเลย · เคยบ้าง (ไม่ถึง 6 เดือน) · เล่นประจำ | Controls exercise difficulty |
| 6 | Where + equipment | ฟิตเนส / ที่บ้าน / ทั้งสองที่ → equipment checklist with icons (dumbbells, bench, cable, machines, pull-up bar, bands, none) | Feeds the "do with what we have" filter |
| 7 | Schedule | Days per week (2–6) · minutes per session (20 / 40 / 60) | |
| 8 | Focus areas | Tap zones on a body map: อก, ไหล่, แขน, หน้าท้อง, หลัง, ขา | Multi-select |
| 9 | Building plan | Animated checklist: "คำนวณแคลอรี่ ✓ เลือกท่าที่เหมาะกับอุปกรณ์ ✓ ..." | 3–4 s, builds anticipation |
| 10 | Scan prompt | "สแกนร่างกายเพื่อดูจุดแข็งและจุดที่ต้องพัฒนา" · [สแกนเลย] · [ไว้ทีหลัง] | **Skip is a first-class option** |
| 11 | Privacy + pose | "รูปของคุณจะถูกเก็บไว้ในเครื่องของคุณ ส่งไปวิเคราะห์แล้วลบทันที" · pose tips: same light, shirt off, arms relaxed at sides | PDPA consent checkbox |
| 12 | Camera | **One front photo**: body outline overlay (head to hips), distance indicator, 3-2-1 timer, retake button | Mirror selfie or propped phone both work |
| 13 | Analysing | Scanning line animation over the photo, zones lighting up | 3–5 s |
| 14 | Result (free) | Overall score (count-up) · body type label · potential score · body-fat range · zone breakdown **blurred** | The aha moment |
| 15 | Timeline | "~10 สัปดาห์ ถึงเป้าหมาย" + bottleneck (Shred: body fat · Bulk: calories eaten) | Personal, specific, motivating |
| 16 | Paywall | See §9 | |
| 17 | Exit offer | Shown once, honest % vs. the price on screen 16 | |
| 18 | Notifications | "ให้เราเตือนวันฝึกและวันสแกนไหม?" | Ask after value is shown |

## 7. Information architecture

Five tabs. Home sits in the centre.

| แผนฝึก (Plan) | อาหาร (Food) | **หน้าแรก (Home)** | สแกน (Scan) | ฉัน (Me) |
|---|---|---|---|---|
| This week's plan | Calories left ring | Today's workout card | Latest result | Profile + goal |
| Workout player | Protein / carbs / fat | Streak | Breakdown / Progress toggle | Body stats, weight log |
| Exercise library | Meals today | Calories left (mini) | Weekly re-scan countdown | Apple Health / Health Connect |
| Browse by muscle | Thai quick-add | Weakest zone + "Train it" | Compare week 1 vs now | Units, language, mode, coach voice |
| Browse by equipment | Eat-more tips (Bulk) | Challenges + Quick Hits (below the fold) | Share card | Subscription, privacy, delete data |

### Home layout (top to bottom)

```
🔥 12 วันติด                          (avatar)
┌──────────────────────────────────────┐
│ วันนี้: อก + ไหล่                      │
│ 6 ท่า · 40 นาที · ยิม                  │
│ [ ▶ เริ่มเลย ]          (blue, full)  │
└──────────────────────────────────────┘
อาหาร: เหลือ 1,240 kcal · โปรตีน 92/140 g
จุดอ่อน: ไหล่ 55 → [ฝึกเลย]
สแกนครั้งถัดไป: 3 วัน
── Challenges · Quick Hits ──
```

On rest days the workout card becomes "วันพัก" with a 10-minute mobility Quick Hit and the food card moves to the top.

## 8. Key flows

### 8.1 Workout (the user's own flow, refined)

```mermaid
flowchart LR
    A[Today's workout] --> B[Exercise card<br/>demo · muscle · equipment]
    B --> C[Log set<br/>kg × reps]
    C --> D[Rest timer<br/>runs in background]
    D -->|more sets| C
    D -->|next exercise| B
    B -.->|machine busy| X[Swap: same muscle,<br/>other equipment]
    X --> B
    D -->|done| E[Summary<br/>volume · PRs · badge]
    E --> F[Muscle map updates]
```

- Coach "Maxx" counts reps and announces rest in Thai (voice can be muted).
- Previous session's numbers pre-fill each set; one tap = "same as last time".
- Screen stays awake; rest timer shows on the lock screen and as a notification.
- **Swap** keeps the target muscle and offers alternatives with the user's equipment.

### 8.2 Exercise lookup — answering the three beginner questions

| Question | Entry point | Result |
|---|---|---|
| "อยากได้กล้ามตัวนี้ ต้องทำท่าอะไร?" | Library → tap a muscle on the body map | Exercises for that muscle, filtered by the user's equipment |
| "อุปกรณ์นี้ทำท่าอะไรได้บ้าง?" | Library → Equipment grid | Exercises for that machine + which muscles they hit |
| "ท่านี้ได้กล้ามส่วนไหน?" | Any exercise card | Highlighted muscle map (primary / secondary) |

**Exercise card anatomy:** demo loop → name (TH + EN) → chips (level · equipment · target zone) → "ตรงกับจุดอ่อนของคุณ" tag when relevant → 3 numbered steps → 2 form cues → common mistake → muscle map → [เพิ่มในเวิร์คเอาต์].

### 8.3 Food log (Thai portions)

```mermaid
flowchart LR
    A[+ Add] --> B[Search or Thai quick-add]
    B --> C[Pick portion<br/>½ จาน · 1 จาน · พิเศษ · grams]
    C --> D[Extras<br/>+ไข่ดาว +ข้าวเพิ่ม]
    D --> E[Ring updates]
```

- Portion picker is mandatory and fast (the #1 AbMaxx complaint was "it assumes I ate the whole thing").
- Units: จาน, ถ้วย, ทัพพี, ช้อนโต๊ะ, ชิ้น, grams, ml.
- **Bulk mode** shows "เติมอีก 600 kcal ง่ายๆ" suggestions (e.g. นมจืด + กล้วย, ข้าวมันไก่ + ไข่).
- **Shred mode** shows lighter swaps (e.g. ข้าวกะเพรา → ขอข้าวครึ่งเดียว).

### 8.4 Scan result (front photo)

```
WEEK 1 · 1 SCAN                     ⏱ 6d 23h
สแกนร่างกาย         [ ความคืบหน้า | รายละเอียด ]
                  ( photo in blue ring )
                         64
               คะแนนรวม · ศักยภาพ 86
      ┌────────────────┬────────────────┐
      │ ผอมแต่มีพุง      │ ไขมัน 18–22%    │
      └────────────────┴────────────────┘
  อก (Chest)        62    ไหล่ (Shoulders) ● 55
  แขน (Arms)        60    หน้าท้อง (Abs)     58
  V-Taper          57    สมมาตร (Symmetry)  81
            [ ฝึกจุดอ่อน: ไหล่ → ]
```

Zones scored from the front photo: **chest, shoulders, arms, abs, V-taper** (shoulder-to-waist ratio) and **symmetry**. Back muscles are trained in the plan but not scored in v1. In Bulk mode the zone scores emphasise size; in Shred mode, definition. Free users see the overall score, body type, potential and body-fat range; zone scores are blurred until Pro.

### 8.5 Weekly re-scan

Countdown ends → push notification → same pose outline as week 1 (ghost overlay of last photo) → result with deltas per zone (▲ +3) → Progress tab shows week 1 vs now side by side → optional share card (photo can be blurred or hidden; scores only).

## 9. Paywall & pricing UX

| Free | Pro |
|---|---|
| First scan: overall score, body type, potential | Full zone breakdown + weakest zone |
| Exercise library **with all demos** | Personalised weekly plan that adapts |
| Workout logger + timer | Weekly re-scan + compare + share cards |
| Calorie & protein target, basic food log | Coach voice, challenges, Thai eat-more / swap tips |

Rules:
- Prices in **฿** with the monthly equivalent ("≈ ฿99/เดือน").
- Any "% off" is calculated against a price shown on the same or previous screen.
- One exit offer, once. No fake countdowns.
- Cancel instructions are one tap away in Me → Subscription.
- Prices are hypotheses to test (e.g. ฿199/month, ฿1,190/year).

## 10. Visual design system

### 10.1 Direction

Dark, premium, energetic — the "maxxing" look users expect. Electric blue is the single action colour. Because AbMaxx also uses blue, GymMaxx sets itself apart through Thai copy, Thai male models at mixed fitness levels (not only shredded), rounded shapes and the Kanit display font.

### 10.2 Colour tokens (dark theme, v1 is dark-only)

```css
:root {
  /* surfaces */
  --bg:            #0B0B0D;
  --surface-1:     #16171A;
  --surface-2:     #1F2125;
  --border:        #2A2D32;

  /* text */
  --text:          #F5F5F7;
  --text-muted:    #9BA1A8;
  --text-faint:    #63686F;

  /* brand / actions */
  --accent:        #3A8BFF;  /* electric blue — links, active tab, rings, highlights on dark */
  --primary:       #2563EB;  /* button fill (deeper blue so white text passes AA) */
  --on-primary:    #FFFFFF;
  --primary-press: #1D4ED8;

  /* goal modes (badges and timeline only, never buttons) */
  --mode-shred:    #FF8A3A;  /* orange — Shred */
  --mode-bulk:     #A78BFA;  /* violet — Bulk */

  /* score scale */
  --score-high:    #34D399;  /* ≥ 80 */
  --score-mid:     #FBBF24;  /* 60–79 */
  --score-low:     #F87171;  /* < 60, also "weakest zone" dot */
}
```

Text on `--bg` and `--surface-1` must meet WCAG AA (4.5:1). `#3A8BFF` on `--bg` passes (≈ 5.9:1), but white text on `#3A8BFF` does not (≈ 3.3:1) — so filled buttons use `--primary` `#2563EB` (≈ 5.2:1 with white). Score colour is never the only signal — always paired with the number.

### 10.3 Typography

| Role | Font | Size / weight |
|---|---|---|
| Display (screen titles, marketing) | **Kanit** | 32–40 / 700, uppercase for Latin |
| Big numbers (scores, timers, kcal) | **Barlow Condensed** | 56–96 / 700, tabular numerals |
| Headings | Kanit | 20–24 / 600 |
| Body | **IBM Plex Sans Thai** | 15–17 / 400, line-height 1.6 |
| Labels / chips | IBM Plex Sans Thai | 12–13 / 500, letter-spacing +2% |

All three are free Google Fonts with full Thai support (Barlow is Latin, used only for numerals). Thai has no spaces between words — use proper Thai line breaking and never truncate Thai mid-word.

### 10.4 Layout & shape

- 4-pt spacing grid; screen padding 20; card padding 16.
- Radius: chips 999, buttons 16, cards 20, sheets 28.
- Minimum tap target 48×48 (sweaty hands mid-workout).
- Primary button full-width, bottom of screen, within thumb reach.

### 10.5 Core components

Button (primary / secondary / ghost) · Chip · Card · Score ring · Zone score bar · Muscle map (front/back SVG, primary/secondary highlight) · Exercise card · Set row (kg × reps, ✓) · Rest timer · Macro ring · Food item + portion picker · Streak flame · Badge · Countdown pill · Paywall plan card · Bottom sheet · Toast.

### 10.6 Motion & feedback

- Score count-up (0 → score, 1.2 s, ease-out) with a soft haptic at the end.
- Scan line sweep + zones lighting up in sequence.
- Set completed: check + light haptic. Workout finished: badge pop + success haptic.
- Respect the OS "reduce motion" setting.

### 10.7 Imagery

- Exercise demos: free-exercise-db start/end photos as a looping 2-frame animation for v1; licensed GIFs or reviewed AI clips later (see research notes).
- Avoid only shredded models. Show a range of Thai male bodies — skinny, skinny-fat, overweight beginners — not only athletes.
- Icons: one consistent outline set (e.g. Lucide or Phosphor), 24 px, 1.75 stroke.

## 11. Voice & copy

Tone: a friendly gym buddy — casual Thai (เป็นกันเอง), encouraging, never preachy or shaming.

| Avoid | Use |
|---|---|
| อ้วน (fat) | ไขมันสะสม / มีไขมันมากกว่าเป้าหมาย |
| คะแนนต่ำ (low score) | ยังมีพื้นที่ให้พัฒนาอีกเยอะ |
| You failed your streak | ไม่เป็นไร เริ่มใหม่วันนี้ได้เลย |

Body-type labels: **ผอม** (Skinny) · **ผอมแต่มีพุง** (Skinny-fat) · **สมส่วน** (Lean) · **ทรง V** (V-Shape) · **ไขมันสะสม** (Higher body fat).

### Coach "Maxx"

- Thai male voice (pre-generated TTS clips, so it works offline); English voice when the app language is English.
- Personality: big-brother gym buddy — warm, upbeat, uses the user's nickname, never yells or insults.
- Speaks at: workout start, each rep count (optional), last 3 reps, rest start / 10 s left, new PR, workout finished.
- Settings: voice on / off, rep counting on / off, volume ducks music instead of stopping it.

Sample lines: "พร้อมยัง? เดี๋ยวนับให้ทุกครั้ง" · "อีก 3 ครั้ง!" · "พัก 90 วินาที ดื่มน้ำก่อน" · "เหลือ 10 วิ เตรียมตัว" · "สถิติใหม่! เก่งมาก" · "จุดอ่อนวันนี้คือไหล่ ไปลุยกัน".

## 12. Accessibility, localisation, privacy

- Thai ↔ English toggle; dynamic type up to 200% without clipping.
- Units: kg/cm default; lb/in optional.
- VoiceOver / TalkBack labels on every score and chart.
- Body photos: stored on device; sent for analysis over TLS and deleted server-side after scoring; explicit PDPA consent; "Delete all my photos" in Me → Privacy.
- Calorie targets have a safe floor and a max weekly loss rate; no extreme-deficit plans.

## 13. What to measure

| Stage | Metric |
|---|---|
| Onboarding | Completion rate, time to first score |
| Scan | % who scan in onboarding, % who skip and scan later |
| Paywall | Trial start / purchase rate, exit-offer take rate, refund rate |
| Activation | % completing first workout within 48 h |
| Retention | D1 / D7 / D30, week-2 re-scan rate |
| Nutrition | Days with ≥ 2 meals logged per week |

## 14. Next steps

1. Low-fi wireframes of the 18 onboarding screens + 5 tabs.
2. Clickable prototype (Thai) of: onboarding → scan result → home → workout player → food log.
3. Test with 5 Bulk and 5 Shred Thai beginners: can they finish onboarding, understand their score, and log a workout without help?
4. Iterate, then build in React Native (Expo).
