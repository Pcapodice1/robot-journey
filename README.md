# Non-Engineer Builds Home Robot Apps
## A Journey Plan — from *Runaway Robot* to Running Robots

**Owner:** Phil Capodice | **Started:** July 2026 | **Horizon:** 24-30 months to first commercial revenue

---

## The Thesis (why this works)

1. **Software eats robotics.** The humanoid hardware race will produce winners and losers, but app-layer skills (VLA models, simulation, ROS 2) transfer across all of them. Robot software is projected to be a ~$48B market by 2032.
2. **Home is the underserved lane.** Enterprise gets all the integrator attention. Early home-robot owners (1X NEO wave, Unitree hobbyists) will have almost no third-party app ecosystem and will be hungry for customization.
3. **Sovereignty is the differentiator.** Most home robots ship cloud-tethered. "Your robot, your data, local brain" is a defensible positioning that matches your macro thesis on physical assets and AI commoditization.
4. **The non-engineer angle is the brand.** Nobody needs another PhD demo channel. "If Phil can do it, I can do it" is the audience hook, and the audience becomes beta testers, then customers.

**North Star:** By late 2028, a small portfolio of paid home-robot software products (task packs, local-brain kits, or customization services) with an audience-driven sales channel.

---

## Stage 0 — Simulation Foundation (Jul-Oct 2026)
*"Make a robot move without owning one"*

**Goal:** Working sim environment on the Mac Mini, core vocabulary, first 8-10 YouTube episodes.

**Equipment/software (current budget-friendly):**
- Mac Mini M4/16GB (have) + 1TB external USB-C NVMe SSD (~$70) — models and sim assets live here
- Miniconda + MuJoCo (native Apple Silicon) — primary physics sim, load the humanoid/G1 models
- LeRobot (Hugging Face) — policy training/inference framework; the transferable skill
- Genesis sim — Mac-friendly alternative worth an episode
- Ollama + a 7-8B quantized model (Llama 3.1 8B or Qwen 2.5 7B) — the "local robot brain" demo
- Cloud GPU by the hour (RunPod/Lambda, ~$0.50-1/hr) for anything NVIDIA-only; budget ~$30/mo

**Milestones (each one is an episode):**
1. Humanoid model standing/flopping in MuJoCo — episode 1 cold open
2. Teleoperate sim robot with a game controller
3. Run a pretrained LeRobot policy (pick-and-place)
4. Build a home scene (kitchen, laundry basket) and script a task
5. Wire Ollama to the sim: talk to your robot, it acts — the sovereign-brain demo

**Exit criteria:** You can explain and demo the perception → policy → action loop without notes.

---

## Stage 1 — Real Hardware, Small (Oct 2026-Feb 2027)
*"A robot arm on the kitchen table"*

**Goal:** Bridge sim-to-real with cheap hardware; grow the channel; start the market-watch habit.

**Equipment:**
- LeRobot SO-101 arm kit (~$110-350 depending on config) — the community-standard starter arm
- Webcam(s) for imitation learning data collection
- Optional: second SO-101 for leader-follower teleoperation (the classic LeRobot setup)

**Milestones:**
1. Assemble the arm on camera ("non-engineer builds a robot arm" — high-CTR episode)
2. Teleoperate and record demonstration datasets
3. Train your first imitation-learning policy on real hardware (cloud GPU fine)
4. A genuinely useful micro-task: sorting guitar picks, loading a dishwasher rack section, folding a washcloth
5. Publish your first repo publicly (see Organization section)

**Exit criteria:** One real-hardware task that makes a stranger say "wait, you built that?"

---

## Stage 2 — Scale Up (Mar 2027-Sep 2027)
*"Full humanoid stack + developer-program positioning"*

**Goal:** Serious compute, Isaac ecosystem, and a seat at the table when home platforms open up.

**Equipment (the March budget window):**
- RTX rig: 4070 Ti Super-class or better, 32-64GB RAM, Ubuntu 22.04 dual-boot (~$1,800-2,500)
- Isaac Sim + Isaac Lab — photorealistic humanoid sim, G1 models included
- Keep the Mac Mini as the "sovereign brain" server (Ollama) — a two-machine story plays great on camera

**Positioning moves:**
- Join 1X NEO developer waitlist/program the moment it exists; same for Figure, Tesla if they open consumer APIs
- Become visibly active in LeRobot Discord/forums — answer beginner questions (you were one 6 months ago; that's your edge)
- Attend one robotics event (CES 2027 or a Chicago-area robotics meetup circuit) as "the home robot apps guy"

**Milestones:**
1. Same home-task policy running in Isaac Sim with domain randomization
2. First "app" prototype: a packaged, installable task or behavior with a simple config UI — even if sim-only
3. Channel at a meaningful subscriber base with a clear niche identity
4. Decision point: buy/lease a real humanoid (used G1 market may exist by then) vs. stay sim + arm

**Exit criteria:** You have a portfolio piece a robot manufacturer or early NEO owner would recognize as valuable.

---

## Stage 3 — Commercialize (Late 2027-2028)
*"First dollar from robot software"*

Candidate first products (validate against what Stage 2 taught you):
1. **Task packs** — pre-trained/configured home routines for a specific platform (the "app" model)
2. **Local-brain conversion kit** — hardware + software bundle to de-cloud a consumer robot (your sovereign thesis productized; highest differentiation, highest difficulty)
3. **Customization service** — bespoke behaviors for early adopters (services revenue funds product development; classic bootstrap)
4. **Paid community/course** — "non-engineer's guide to robot apps" (lowest lift, monetizes the channel directly)

**Recommended sequence:** 4 → 3 → 1 → 2. Monetize knowledge first, services second, products third. Each stage funds the next and de-risks the product bet.

**Business hygiene:** LLC before first paid work; check Voya's moonlighting/IP policy *early* (you know how compliance works — get this in writing); simple Stripe + landing page, no more.

---

## Brand & Channel Plan

- **Format:** journey narrative, same DNA as the guitar channel — struggle on camera, celebrate small wins, never fake expertise
- **Cadence:** 2 videos/month minimum (sustainable with the job); Shorts from long-form cuts
- **Naming:** decide early whether this is a new channel or a rebrand — recommendation: **new channel** ("Phil Builds Robots" or similar) so the guitar audience isn't confused and the niche is pure
- **Content pillars:** (1) build episodes, (2) "robot market this month" explainers, (3) sovereign-AI/ownership commentary — pillar 3 is where your treasury/finance voice is genuinely unique
- **Brand succession plan:** the "non-engineer struggles" hook expires around Stage 2 — by Isaac Lab you're an engineer for audience purposes. The Stage 2+ identity is **the Translator**: "the guy who explains robot ownership to normal people." Pillar 3 promoted to headline. Begin seeding translator-voice content in late Stage 1 so the handoff is gradual, not a rebrand.
- **Compounding loop:** every repo README links to videos; every video description links to repos; email list from day one (even 50 subscribers matters at launch time)

---

## Market Monitoring System

Model this on your GEODNET weekly tracker — it worked there, reuse the pattern:

- **Build a "humanoid-market-tracker" custom skill** (Claude Desktop/Cowork) that runs on a weekly schedule: checks news on 1X NEO, Unitree, Tesla Optimus, Figure; flags developer-program announcements, price changes, and home-deployment milestones; appends to a tracking spreadsheet and writes a short dated brief
- **Thesis conditions to score weekly:** (1) Is a home humanoid shipping at <$25k or <$500/mo? (2) Is any consumer platform's SDK/app store open to independents? (3) Is there visible owner demand for customization (Reddit/Discord activity)?
- When condition 2 flips green, that's your signal to shift effort hard toward that platform.
- **Quarterly platform go/no-go (starting Oct 2026):** formal review of condition 2 in Robot Journey HQ. The commercial thesis depends on a door someone else opens — score it every quarter, not every six months. If platforms stay closed through 2027, shift Stage 3 weight toward course + Unitree-hobbyist services early rather than discovering it late.
- Monthly: turn the four weekly briefs into a "state of home robots" video — monitoring becomes content, content becomes brand.

---

## Claude Toolkit & Organization

**Claude.ai Projects:**
- **"Robot Journey HQ"** project — this plan as project knowledge, plus your decision log. Use it for strategy sessions, stage reviews, and pivots (same pattern as your AI-transformation advisor project).
- **"Robot Build Log"** project — technical troubleshooting; paste errors, get unstuck fast.

**Claude Code (terminal or Desktop):** your pair programmer for all LeRobot/MuJoCo work. Realistic framing: you're not "coding," you're directing — Claude Code writes and debugs, you learn by reading and running. Install docs: https://docs.claude.com/en/docs/claude-code/overview

**Claude Cowork:** weekly scheduled market-tracker skill (above); video script drafting from build notes; monthly progress reviews against this plan.

**Connectors:**
- **GitHub** — connect it so Claude can read/manage your repos in chat
- **Google Drive** — datasets index, video assets, market tracker spreadsheet
- **Asana** — mirror the stage milestones as projects; you already live in structured task tools at work
- **Gmail/Zapier** — developer-program email alerts routed into your weekly review

**Repos (public from Stage 1):**
- `robot-journey` — the meta-repo: this plan, weekly logs, decision records
- `home-robot-sims` — MuJoCo/Genesis scenes and configs (home environments are reusable content)
- `so101-experiments` — arm datasets, training configs, results
- One repo per "app" prototype later, each with a demo GIF in the README

**Custom skills to build as you go:** humanoid-market-tracker (Stage 0), video-episode-packager (turns build notes into script + description + chapters), dataset-logger (Stage 1).

---

## Time Budget & Guardrails

- **5-7 hrs/week** is the sustainable floor with the Voya job and the IR build cycle: ~3 hrs building, ~2 hrs filming/editing, ~1 hr market review. Protect it like a standing meeting.
- **Pre-decided sacrifice order for bad months** (hardware time WILL expand in Stage 1+): (1) market-watch video slips first, (2) video polish drops — publish rough, (3) build pace slows. **Build videos never slip** — they're the compounding asset. A bad month follows the order; it never becomes an unplanned pivot.
- **One platform bet at a time.** The market will tempt you weekly. The tracker decides pivots, not headlines.
- **Kill criteria (review every 6 months):** if by mid-2027 no consumer platform has opened to independent developers AND channel growth is flat, the pivot is to the integrator/service lane (Stage 3 option 3) targeting Unitree owners and small businesses — the skills transfer fully.
- **Don't let the day job starve this.** You solved the bootstrapping problem for Voya transformation work by making it systematic; do the same here. The weekly tracker + monthly review IS the system.

---

## First 30 Days (start now)

- [ ] Order external SSD
- [ ] Install Miniconda + MuJoCo; humanoid model on screen
- [ ] Create "Robot Journey HQ" Claude project; upload this plan
- [ ] Create `robot-journey` repo; commit this plan as README v1
- [ ] Film episode 1 (don't polish — the flopping robot IS the hook)
- [ ] Decide channel name; register handle
- [ ] Build v1 of the humanoid-market-tracker skill; run it manually once
- [ ] Check Voya moonlighting/IP policy
- [ ] Join LeRobot Discord; introduce yourself as a non-engineer building in public

*The kid who read Runaway Robot didn't have the tools. You do now. Build the flopping robot this week.*
