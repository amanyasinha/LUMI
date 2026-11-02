# Tinkerly: Product Plan (v2)

*Working draft, updated 1 Nov 2026. Name status: Tinkerly is the chosen name. A web search found no product with that exact name, but trademark and domain checks are still required (Section 12).*

---

## 1. Vision

Tinkerly is a friendly, privacy-first AI assistant for your laptop (phone later). It **watches your device's health, teaches you how to do things (including inside other apps), keeps your files organized, and does chores for you**, while you only approve the important steps.

**One-line pitch:** *Monitoring tells you what's wrong, teaching shows you how to fix it, and the agent fixes it for you, all under controls that make it safe to trust.*

**Realistic promise:** "Handles your everyday device chores and teaches you the rest." Not "does anything."

**Possible tagline:** "Your device's friendly fixer-upper."

---

## 2. Features at a Glance

1. **Device monitoring:** CPU, RAM, disk, battery, network, processes; learns what is normal for your device.
2. **Smart alerts and predictions:** catches problems early; warns before the battery dies or the disk fills.
3. **Ask-anything chat:** answers questions about your device in plain language using real data.
4. **Teaching mode:** general tutor plus personal tutor, learning paths, pointing cursor, hints, fading help, progress tracking, lessons that become automations.
5. **File sorting:** downloads go to Notes, Certificates, or custom folders; suggest mode, Undo, move log; never deletes.
6. **AI agent:** plans and performs tasks (cleanup, settings, email, forms) and asks approval on important steps.
7. **Autonomy levels:** Guide, Ask first, Trusted tasks, Full auto. Everyone starts at "Ask first."
8. **Safety and trust:** confirmation for irreversible actions, action log with Undo, kill switch, "AI is acting" indicator, prompt-injection defenses.
9. **Privacy-first AI:** local where possible, cloud only for hard questions, with a log of what leaves.
10. **Memory and reach:** learns habits, voice, Indian languages, laptop first, Android companion later.

---

## 3. Detailed Feature List

### Monitoring
- System health tracking (CPU, RAM, disk, battery, temperature, network, processes, logs)
- Private local history of normal behavior
- Anomaly detection
- Predictions for battery, disk, and slowdowns

### Assistant
- Ask-anything chat from real device data
- Proactive alerts before you ask
- Voice in and out
- Screen awareness on hotkey only, with no background recording
- Floating overlay or tray app

### Teaching (see Section 5)
- Lessons triggered by real events on your device
- "Why" explanations using your own data
- Goal-based learning paths ("teach me to model a mug")
- Pointing cursor, highlights, arrows, shortcut tips
- Show, then hand over
- Verification of your actual work or device state
- Stuck detection: hint, bigger hint, demo
- Help that fades out as you improve
- App-specific tutors via add-ons (Blender, VS Code, Excel, Photoshop)
- Skill progress tracking and spaced review
- Turn a learned lesson into an automation
- Multilingual teaching, including Indian languages

### File management
- Smart download sorting into Notes and Certificates
- Suggest mode, Undo, move log; never deletes
- Custom folders described in plain language

### Agent (see Section 6)
- Task planner
- Action executor (clicks, typing, drags, files, app APIs)
- Self-checking loop with retries
- Autonomy levels
- Mandatory confirmation for irreversible actions
- Device-chore skills (free disk space, clear cache, close heavy apps, change settings)
- Workflow skills (email, forms, browsing)

### Safety and trust (see Section 7)
- Action log with Undo
- Kill switch and pause button
- "AI is acting now" indicator
- Prompt-injection defenses
- Whitelisted actions and sandboxing
- No capture of password fields or private windows
- Secure API proxy

### Intelligence and reach
- Local-first AI
- Memory and personalization
- Laptop first; Android companion later

---

## 4. File Sorting Pipeline

Detect new file → wait for download to finish (ignore `.crdownload`, `.part`, `.tmp`) → classify (file name rules, then content check, then AI fallback) → move → notify with Undo → log.

Start in **suggest mode** (ask before moving). Switch to auto-move once accuracy is proven. Never delete; only move and log.

---

## 5. Teaching Approach

### How it differs from Clicky
Clicky (open-source "AI teacher next to your cursor," macOS original by Farza Majeed, with a community Windows port) teaches by pointing at your screen when you ask. Tinkerly teaches differently because it also knows your device's real data and can follow a learning path.

| | Clicky | Tinkerly |
|---|---|---|
| Starts when | You ask | A real event happens, or you set a goal |
| Understands your situation from | Screenshot | Screenshot plus live device data and app add-ons |
| Teaching style | Point and explain | Explain why, demonstrate, then you do it |
| Knows you did it right by | Trusting you | Checking the actual device or app state |
| Remembers you | No | Tracks what you have learned |
| After teaching | Nothing | Offers to do it for you next time |

### Six teaching methods
1. **Learn from your own real problems:** lessons come from events on your device (disk full, battery drain), using your own data.
2. **Explain the "why" with your data:** "RAM was 40% this morning, now 92%. These three tabs cause most of it."
3. **Show, then hand over:** it demonstrates once, then says "your turn" and verifies the result.
4. **Fade the help out:** guide every click, then hints, then nothing.
5. **Turn lessons into automations:** "Want me to handle this next time?" Learning feeds the agent.
6. **Skill progress and spaced review:** private list of learned skills with short friendly refreshers.

### General tutor vs. personal tutor
| Question | General tutor (no personal data) | Personal tutor (with your data) |
|---|---|---|
| "What is a modifier in Blender?" | Concept explained, pointer to the panel | Shows which modifiers are on your mug |
| "What is RAM?" | General explanation | "Your RAM is at 92% right now, here is why" |
| "How do I make a pivot table?" | Step-by-step guide | Checks your sheet and spots the mistake |

- **General tutor** uses the AI's knowledge, hotkey-only screen capture, official docs, and web search. It is useful from day one.
- **Personal tutor** adds device metrics and app add-ons so it can verify your work, spot mistakes, and track progress. This is the premium, hard-to-copy layer.
- General answers can be wrong, so ground them in official docs, show sources, and say "not sure" when needed.

### Example: learning Blender ("teach me to model a mug")
1. You state a goal; Tinkerly builds a short path (cylinder, extrude, handle, smooth).
2. It detects your Blender version so menus and shortcuts match.
3. The cursor flies to *Add → Mesh → Cylinder*, with a card saying what and why, plus the shortcut.
4. A small Blender add-on (Python) reads the actual scene, so it can confirm "extruded, nice" or "I do not see the extrusion yet."
5. If you are stuck (repeated attempts or long idle time), it offers a hint, then a bigger hint, then a demo.
6. It explains problems using your scene ("12 segments is why the edges look jagged; try 32").
7. Help fades in the next lesson (a bowl).
8. After repetition, it offers to automate the setup.

**Limits:** verification only works in apps that expose their state; each app needs its own add-on (start with Blender, VS Code, Excel, Photoshop); add-ons are opt-in and local.

### Build stages for teaching
1. MVP: event-based lessons from metrics shown as short step cards (no voice or cursor needed)
2. "Show, then hand over" with device-state verification
3. Fade-out scaffolding and the skill list
4. Pointing cursor and voice
5. "Turn this lesson into an automation" once the agent exists

---

## 6. The Agent

### Loop
See (screen or app structure) → plan → act → check → repeat until done.

### Preferred order of methods
| Order | Method | Example |
|---|---|---|
| 1 | App API or script | Move a Blender object with Python |
| 2 | Keyboard shortcut or menu command | Cut and paste, "move to" command |
| 3 | UI element action using accessibility info | Click the "Move" button |
| 4 | Mouse drag on screen coordinates | Last resort |

**Example: dragging a block.** It can be done by controlling the mouse (press, move, release, then check the result), but dragging is fragile (exact pixels, timing, layout changes). The agent should look for an API, shortcut, or UI-element action first. When teaching, the cursor shows the drag path and the user does it. When doing, the agent drags and verifies the result.

### Autonomy levels
| Level | What it does | Your role |
|---|---|---|
| 1. Guide | Points and explains | You do the clicks |
| 2. Ask first | Does the task, asks before each important step | You tap Approve |
| 3. Trusted tasks | Runs routine tasks alone | You review a log |
| 4. Full auto | Handles whole workflows | You are notified at the end |

**Rules**
- Everyone starts at Level 2.
- A task moves up only after many successful runs; a failure or an undo drops it back.
- Users set trust **per task** (for example, "always let it sort my downloads"), not one global switch.
- **Allowed without asking (once trusted):** reversible in-app actions, sorting downloads, clearing cache, closing a runaway process.
- **Always asks (cannot be switched off):** sending, paying, deleting, submitting forms, moving files outside your folders, changing system settings.

### What the agent can and cannot do
**Does well**
- Tasks where the app exposes controls (API, script, shortcuts, accessible buttons)
- Repetitive device chores
- Multi-step work in common software with checks after each step
- Reversible tasks

**Struggles with**
- Games, custom canvases, and apps with no exposed controls (screenshot guessing is slow and error-prone)
- Judgment or taste tasks ("make this look good")
- Long open-ended workflows where errors pile up
- Interfaces that change between runs

**Refuses or hands back to the user**
- Entering passwords, solving CAPTCHAs, handling two-factor codes
- Payments and transfers
- Permanent deletion
- Sending messages or submitting forms without confirmation
- Changing security or system settings
- Anything illegal, or acting on someone else's account or device without permission

**Marketing rule:** do not promise "does anything." Say "handles your everyday chores and asks when unsure," and have the app say "I cannot do that reliably" when true.

---

## 7. Safety and Trust

| Feature | Purpose |
|---|---|
| Action log with Undo | See and reverse everything the agent did |
| Kill switch and pause button | Stop it instantly |
| "AI is acting now" indicator | You always know when it is working |
| Check after every step, honest failure reports | No silent mistakes |
| Hard stop on surprises | Unexpected popups, login pages, or on-screen text that looks like instructions to the AI |
| Prompt-injection defenses | Screen and web content is data, never instructions |
| Whitelisted actions, sandboxing for risky steps | It can only do approved things |
| Secure API proxy | No API keys in the app |

---

## 8. Privacy and Data Handling

**Stays on the device**
- Monitoring data and history (local SQLite, not uploaded by default)
- File-sorting rules and text extraction
- Routine AI work via a small local model
- Memory and skill progress (local, encrypted)

**May leave the device, with limits**
- Hard questions: only the minimum needed (a short snippet, not the whole screen or file) goes to a cloud model
- Screenshots: only on hotkey, with no background recording
- Filtering before sending: password fields, private or incognito windows, banking pages, and detected personal data (such as ID numbers) are blurred or blocked

**User controls**
- Visible pause button for all monitoring and capture
- Per-app block list (banking apps, password managers)
- "What was sent" log showing what went to the cloud and when
- One-tap "delete my data" for history, memory, and logs
- Offline mode using only the local model
- Plain-language explanations when asking for screen recording, accessibility, and microphone permissions

**Honesty rules**
- Do not claim "100% private" or "nothing ever leaves your device" unless literally true.
- State exactly what leaves and when.
- Check cloud providers' data-handling terms and describe them accurately.
- Write a short plain-language privacy policy before launch.

**Legal:** rules differ by country. India's Digital Personal Data Protection Act and the EU's GDPR may apply. Get proper legal advice before selling, especially on consent and retention. (This plan is not legal advice.)

---

## 9. Architecture

| Layer | Role | Suggested tech |
|---|---|---|
| Collector | Metrics, events, file-system changes | `psutil`, `watchdog`, native OS APIs |
| Storage | Rolling local history | SQLite (encrypted) |
| Detector | Decides what is worth flagging | Statistical thresholds, Isolation Forest |
| Brain | Explains, plans, classifies ambiguous files | Small local model plus cloud LLM fallback |
| Tutor engine | Learning paths, verification, progress | App add-ons, official docs retrieval |
| Agent | See, plan, act, check loop | Tool-calling LLM with whitelisted tools |
| Action layer | Executes approved actions with confirmation | Whitelisted tools, sandbox |
| Interface | Voice, overlay, teaching cursor | Tray/menu bar app, speech-to-text, text-to-speech |

---

## 10. Competitive Landscape

No single product found combines all of the above, but each piece exists.

- **File sorting (crowded):** MyQuickMac Lite, File Sortify, Files Magic AI, Foldora, AI File Organizer Pro, SortIt, DownloadPilot, Sparkle, Sortio, Sorty.
- **AI system monitoring (thinner):** Mnara (macOS), PC Workman (open source), SenseGuard AI, Dell SupportAssist (business).
- **Screen-aware teaching assistants:** Clicky (macOS plus a community Windows port, with an optional proactive tutor mode), Cluely, Microsoft Copilot.
- **Computer-use agents:** large AI companies already ship agents that operate browsers and desktops. A general "does everything" agent competes directly with them.
- **Platform giants:** Google, Microsoft, and Apple keep adding built-in assistants and AI cursors.
- **Name neighbors:** several AI products use "Tinker" (Shopify's Tinker app, an AI-lab Tinker for model customization, TinkerPilot, Tinkerwell). This is a trademark-similarity risk for "Tinkerly."

| Capability | Already covered? |
|---|---|
| Download sorting | Yes, heavily (commodity) |
| AI system monitoring | Partly |
| Screen-aware voice teaching | Yes |
| Safe device actions with approvals | Weakly |
| Event-driven, verified, app-aware teaching that feeds an agent, local-first, with memory | Not found |

---

## 11. Positioning and Roadmap

**Positioning**
- Pitch as "an assistant that handles your device chores and teaches you the rest," not "an AI that does everything."
- Lead with trust: local-first, undo for everything, visible kill switch, hotkey-only capture, a log of what leaves the device.
- Focus on device health, file management, and app-aware teaching.
- Pick one first audience (students fit: notes, certificates, learning software like Blender), then expand.
- Do not compete on file sorting alone; bundle it.

**Roadmap**
| Phase | Scope |
|---|---|
| MVP | Monitoring, local history, ask-anything chat, local-first AI |
| 2 | Anomaly detection, predictions, proactive alerts |
| 3 | Download sorter (suggest mode, undo, move log) |
| 4 | Event-based lesson cards, then voice, hotkey screen capture, pointing cursor, overlay |
| 5 | Agent loop on one narrow task (for example, "free up disk space safely") with approvals, log, kill switch |
| 6 | Memory, custom folders, skill tracking, lessons-to-automations |
| 7 | App add-ons (Blender, VS Code, Excel, Photoshop) and broader workflow skills |
| 8 | Android companion |

**Test plan:** after MVP and Phase 3, show it to 10 to 20 target users before building the agent.

---

## 12. Risks and Open Items

**Safety and security**
- Agents misclick and misread; irreversible actions always need confirmation.
- Prompt injection from web pages or documents is a real attack path.
- A full-control agent is a large attack surface; keep actions whitelisted and logged.
- Build the safety layer alongside the agent, not after it.

**Reliability**
- A 90% success rate is not enough for tasks like emailing; launch with a small set of very reliable tasks and add skills one at a time.

**Privacy and legal**
- Screen capture is sensitive; get legal advice on privacy and data handling per market. Monitor only the user's own devices.

**Business**
- Big platforms may build similar features natively.
- Each app tutor needs its own add-on (real engineering work).

**Name checks still to do**
- [ ] IP India trademark search for "Tinkerly" (software and AI classes); US database if selling there
- [ ] Domains: tinkerly.com, .app, .ai
- [ ] Social handles: Instagram, X, GitHub
- [ ] App Store and Google Play search
- [ ] Consider a trademark attorney, given the similar "Tinker" AI products

---

## 13. Next Steps

1. Choose first target audience and operating system.
2. Build the MVP (metrics collector plus local chat) and test on your own laptop.
3. Add the download sorter and demo it to 10 to 20 potential users.
4. Complete the name checklist in Section 12.
5. Prototype event-based lesson cards.
6. Prototype the agent loop on one narrow task with approvals.
7. Write the privacy policy and get legal review.
8. Recheck the competitive landscape before launch; it changes fast.

---

## Sources checked

- Clicky: GitHub (farzaa/clicky and a community Windows port), Product Hunt, AIPure, SourcePulse
- File organizers: App Store listings, Product Hunt, Hunted, AlternativeTo
- System monitoring: AI Indigo (Mnara review), HackerNoon (PC Workman), lablab.ai (SenseGuard AI), Dell
- Name research: Shopify (Tinker), Yahoo Tech (AI-lab Tinker), TinkerPilot docs
