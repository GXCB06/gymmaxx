# GymMaxx — Product Requirements Document (PRD)

> Status: v0.1 draft · Owner: GymMaxx founder · Last updated: 2026-10-22
> Related: [DESIGN.md](DESIGN.md) (UX/UI) · [PROJECT.md](PROJECT.md) (tech, roadmap)

---

## 1. Summary

GymMaxx is a Thai-first mobile app (iOS + Android) that helps men change their physique — whether they want to **lose fat (Shred)** or **gain muscle as a skinny beginner (Bulk)**. The user takes a front photo, gets a score for each upper-body zone, learns the one thing holding them back, and follows a personalised plan of workouts and Thai food. A weekly re-scan shows progress.

**Promise:** "Whatever your starting point, GymMaxx shows you how to change your body — and lets you see it happen."

## 2. Problem

Thai gym beginners ask the same questions and no app answers them well in Thai:

| Pain point (founder's own) | Today's workaround | Gap |
|---|---|---|
| "อุปกรณ์ในยิมใช้ยังไง ได้ muscle อะไรบ้าง" — how do I use this machine, what does it train? | Ask strangers, YouTube | No Thai, equipment-first guide |
| "ทำแบบนี้ถูกมั้ย" — am I doing this right? | Guess, copy others | Demos missing or English-only |
| "ต้องกินกี่ cal ถึงจะ muscle ขึ้น" — how much should I eat? | Online calculators, MyFitnessPal | No Thai food with Thai portions |
| "อยากรู้ว่า muscle พัฒนาไปไกลแค่ไหน" — how far have I progressed? | Mirror selfies | No measurable, visual progress |

### Evidence from competitor research (AbMaxx case study)

- AbMaxx (abs-only scan app) reportedly earns ~$46–55K/month — proof that "scan → score → plan" monetises.
- Its users love: personalisation, being told exactly what to do, the score/bottleneck language.
- Its users complain about: food logging without portion sizes, missing exercise demos, timer stopping mid-workout, weak Apple Health sync, and a misleading "90% off" paywall ("It's a scam").
- No competitor is Thai-first.

## 3. Goals and non-goals

### Goals (v1)
1. Give Thai male beginners a clear answer to "what should I do and eat for my body?"
2. Make progress visible through a weekly physique scan.
3. Reach a sustainable subscription business in Thailand.

### Non-goals (v1)
- Women-specific scan zones and content (planned later).
- Real-time camera form checking.
- Scan-the-machine (camera recognition of gym equipment).
- Social feed, friends, leaderboards.
- AI meal-photo calorie recognition.
- Apple Watch / Wear OS apps.

## 4. Target users

| Persona | Description | Mode | Primary job-to-be-done |
|---|---|---|---|
| **A · Skinny beginner** | 18–25, underweight or slim, new to the gym | Bulk | "Help me get bigger and tell me how much to eat" |
| **B · Losing weight** | 25–35, office worker, belly fat, low confidence | Shred | "Help me lose fat and see my muscles appear" |
| **C · Gym regular** (secondary) | Trains 1+ year | Either | "Track my progress and show me my weak spots" |

Market: Thailand, Thai-speaking, Android-heavy, so both platforms are required at launch.

## 5. Success metrics

Initial targets — to be revisited after beta data.

| Metric | Definition | v1 target |
|---|---|---|
| Onboarding completion | Install → reaches Home | ≥ 70% |
| Time to first score | Open → score shown | ≤ 2 min median |
| Scan rate | Onboarded users who complete a scan within 7 days | ≥ 60% |
| Conversion | Installs → paid or trial start | ≥ 5% |
| Activation | First workout completed within 48 h | ≥ 40% |
| D7 retention | Active on day 7 | ≥ 25% |
| Week-2 re-scan | Scanners who re-scan in week 2 | ≥ 40% |
| Trust | App Store / Play rating | ≥ 4.5★, no "scam" reviews about pricing |

## 6. Scope — features and requirements

Priority: **P0** = required for launch · **P1** = launch if ready, else first update · **P2** = later.

### F1. Onboarding — P0
| ID | Requirement |
|---|---|
| F1.1 | Collect goal (Shred / Bulk / Both), sex, age, height, weight, experience, training location, equipment, days/week, session length, focus areas — one question per screen with a progress bar. |
| F1.2 | Total time from first screen to Home ≤ 2 minutes for a typical user. |
| F1.3 | Calculate daily calorie and protein targets from the answers (Mifflin-St Jeor BMR × activity, ± goal adjustment). |
| F1.4 | Generate the first weekly workout plan from goal, experience, equipment and schedule. |
| F1.5 | Scan step can be skipped ("ไว้ทีหลัง") without blocking the rest of the app. |

**Acceptance:** a new user can reach Home with a plan and calorie target without scanning or paying.

### F2. Body scan — P0
| ID | Requirement |
|---|---|
| F2.1 | Capture **one front photo** with a body-outline overlay, distance check and 3-2-1 timer. |
| F2.2 | Reject unusable photos (no person, body cut off, too dark) with a clear retry message. |
| F2.3 | Return: overall score (0–100), potential score, body-type label, body-fat **range**, and zone scores for chest, shoulders, arms, abs, V-taper, symmetry. |
| F2.4 | Identify the weakest zone and link to "Train it" workouts. |
| F2.5 | Scores are framed by mode: size in Bulk, definition in Shred. |
| F2.6 | Re-scan limited to once per 7 days; countdown shown. |
| F2.7 | Progress view compares any scan with week 1 side by side and shows per-zone deltas. |
| F2.8 | Shareable result card with option to hide or blur the photo. — P1 |
| F2.9 | Scan pack purchase to re-scan early. — P2 |

**Acceptance:** the same user, same pose and lighting, scanned twice within an hour, gets an overall score within ±3 points.

### F3. Personalised plan — P0
| ID | Requirement |
|---|---|
| F3.1 | Weekly plan showing which days train which muscle groups. |
| F3.2 | Uses only exercises the user's equipment supports (gym, home, or both). |
| F3.3 | Prioritises the weakest scanned zone. |
| F3.4 | Shred: strength work + conditioning; Bulk: progressive overload, minimal cardio. |
| F3.5 | Progressive overload suggestions (add weight/reps when targets are hit). — P1 |
| F3.6 | Phases (e.g. 4-week blocks) and challenges (21/30-day). — P1 |

### F4. Workout player & logging — P0
| ID | Requirement |
|---|---|
| F4.1 | Flow: exercise card → log set (kg × reps) → rest timer → next set/exercise → finish summary. |
| F4.2 | Previous session's numbers pre-fill; "same as last time" in one tap. |
| F4.3 | Rest timer continues when the app is backgrounded or the phone is locked, with a notification at the end. |
| F4.4 | Screen stays awake during an active workout. |
| F4.5 | Swap an exercise for another one targeting the same muscle with available equipment. |
| F4.6 | Finish summary: duration, volume, personal records, badge; muscle map updates. |
| F4.7 | Voice coach "Maxx" (Thai male voice): workout start, rep counting, last 3 reps, rest start/10 s left, PR, finish. Mute and rep-count toggles. — P1 |
| F4.8 | Works offline; syncs when back online. |

### F5. Exercise library — P0
| ID | Requirement |
|---|---|
| F5.1 | Every exercise has: demo, Thai + English name, primary/secondary muscles, equipment, level, 3 steps, 2 form cues. |
| F5.2 | **No exercise is shown without a demo.** |
| F5.3 | Browse by muscle (tap body map), by equipment (grid), and search. |
| F5.4 | Exercise detail shows highlighted muscle map and "ตรงกับจุดอ่อนของคุณ" tag when relevant. |
| F5.5 | v1 content: ~150 curated exercises from free-exercise-db (public domain) with 2-frame demo loops, translated to Thai. |
| F5.6 | "Common mistake" section per exercise. — P1 |
| F5.7 | Upgrade demos to licensed GIFs or trainer-reviewed AI clips. — P2 |

### F6. Nutrition — P0
| ID | Requirement |
|---|---|
| F6.1 | Daily calories-left ring plus protein / carbs / fat. |
| F6.2 | Thai food quick-add list (≥ 150 common dishes, 7-Eleven items, drinks). |
| F6.3 | **Portion picker is mandatory**: ½ จาน, 1 จาน, พิเศษ, ทัพพี, ช้อนโต๊ะ, ชิ้น, grams, ml. |
| F6.4 | Add-ons (e.g. +ไข่ดาว, +ข้าวเพิ่ม). |
| F6.5 | Bulk mode: "add 500 kcal easily" suggestions. Shred mode: lighter swaps. — P1 |
| F6.6 | Safe limits: calorie target never below a safe floor; weight-loss rate capped. |
| F6.7 | Barcode scanning. — P2 |

### F7. Home & engagement — P0
| ID | Requirement |
|---|---|
| F7.1 | Home order: streak → today's workout card → calories left → weakest zone → next scan countdown → challenges / Quick Hits. |
| F7.2 | Rest-day variant with a short mobility session. |
| F7.3 | Streaks with a forgiving "streak saver". — P1 |
| F7.4 | Push notifications: training-day reminder, re-scan ready, streak at risk. Max 1 per day. |

### F8. Monetisation — P0
| ID | Requirement |
|---|---|
| F8.1 | Free tier: onboarding, first scan (overall score, body type, potential, body-fat range), full exercise library with demos, workout logger, calorie target, basic food log. |
| F8.2 | Pro: zone breakdown, adaptive plan, weekly re-scans + compare, coach voice, challenges, smart food tips. |
| F8.3 | Paywall appears after the free score; zone breakdown is shown blurred behind it. |
| F8.4 | Prices in ฿ with monthly equivalent. Initial hypothesis: ฿199/month, ฿1,190/year — to be tested. |
| F8.5 | One exit offer, shown once; any "% off" is calculated against a price shown on screen. No fake timers. |
| F8.6 | Restore purchases and clear cancel instructions in Me → Subscription. |

### F9. Profile, settings, integrations — P0
| ID | Requirement |
|---|---|
| F9.1 | Edit body stats, goal/mode, equipment, schedule. |
| F9.2 | Weight log with chart. |
| F9.3 | Language Thai / English; units kg/cm or lb/in. |
| F9.4 | Apple Health (iOS) and Health Connect (Android): write workouts, read/write weight. — P1 |
| F9.5 | Privacy: delete all photos, export data, delete account. |

## 7. Non-functional requirements

| Area | Requirement |
|---|---|
| Platforms | iOS 16+, Android 9+ (API 28+), phones only in v1 |
| Performance | Cold start < 2 s on a mid-range Android; scan result < 10 s |
| Offline | Workout player, library and food log work offline |
| Privacy (PDPA) | Explicit consent for body photos; photos stored on device; server copies deleted after analysis; no photo used for training without opt-in |
| Security | TLS everywhere, auth tokens in secure storage, row-level security on user data |
| Accessibility | WCAG AA contrast, screen-reader labels on scores/charts, dynamic type to 200%, 48 px tap targets |
| Localisation | Thai default, English toggle; correct Thai line breaking |
| Health & safety | Not medical advice disclaimer; safe calorie floor; no extreme-deficit plans; injury-safe beginner progressions |
| Store compliance | Honest subscription disclosure per App Store / Play policies |

## 8. Dependencies

| Dependency | Purpose | Notes |
|---|---|---|
| free-exercise-db | Exercise data + start/end photos | Public domain (Unlicense) |
| Vision AI model (cloud) | Physique zone scoring | Prompted for structured JSON; cost per scan to monitor |
| On-device pose detection | Photo validation, shoulder-to-waist ratio | e.g. MediaPipe Pose |
| Thai food dataset | Nutrition values | Curate from Thai food composition tables; verify licence |
| Thai TTS | Coach Maxx voice clips | Pre-generated, bundled |
| Subscription SDK | iOS + Android purchases | e.g. RevenueCat |

## 9. Risks and mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Scan scores feel random or inconsistent | Users lose trust, churn | Pose guide, consistency test (±3), show ranges, back up with weight/waist/strength |
| Low first score discourages beginners | Churn at aha moment | Potential score, kind labels, scan is optional |
| Copycats | Lost differentiation | Thai content, Thai food, local creator partnership, community |
| Paid-ads dependence | Thin margins | Organic TikTok slideshows; creator equity/rev-share deal |
| AI demo or plan gives unsafe form/advice | Injury, bad reviews | Trainer review of content, conservative beginner plans |
| Body-photo privacy incident | Legal (PDPA) and brand damage | On-device storage, delete after analysis, minimal retention |
| AI scan cost per user | Margin | 1 scan/week limit, small model where possible |

## 10. Release plan

| Phase | Outcome | Exit criteria |
|---|---|---|
| 0 · Validate | TikTok slideshows + waitlist | ≥ 500 waitlist sign-ups or clear winning angle (Bulk vs Shred) |
| 1 · Prototype | Clickable prototype tested with 10 users | 8/10 finish onboarding and log a workout unaided |
| 2 · MVP build | All P0 features | Internal QA pass, scan consistency ±3 |
| 3 · Closed beta | TestFlight + Play closed testing, ~100 users | D7 ≥ 20%, no P0 bugs, pricing test run |
| 4 · Launch (TH) | Public on both stores | Metrics in §5 tracked weekly |

## 11. Open questions

1. Final pricing and whether to offer a free trial in addition to the free score.
2. Which AI approach gives the most consistent scan scores at acceptable cost?
3. Source and licence for the Thai food nutrition dataset.
4. Creator partner: who, and equity vs revenue share?
5. Account required at onboarding, or anonymous until purchase?
6. When to add women's scan zones and content?
