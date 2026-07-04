# Non-Engineer Builds Home Robot Apps 🤖
### From reading *Runaway Robot* as a kid to building apps for real home robots

**Started:** July 2026 | **The journey:** simulation → robot arm → humanoid → home robot apps

<!-- 📹 Once Episode 1 exists: GIF of the flopping humanoid goes HERE, then subscribe link. Proof of work above the fold, strategy below. -->

**Follow along:** [YouTube channel coming soon] | Build log: [build-log.md](build-log.md)

---

## Why this journey

1. **Software eats robotics.** Whichever humanoid wins the hardware race, the app-layer skills (VLA models, simulation, ROS 2) transfer across all of them.
2. **Home is the underserved lane.** Enterprise gets all the attention. Early home-robot owners will have almost no third-party app ecosystem — and they'll want customization.
3. **Sovereignty is the differentiator.** Most home robots ship cloud-tethered. Your robot, your data, local brain.
4. **The non-engineer angle is the point.** I'm not a roboticist. I'm a finance guy with a Mac Mini and a childhood dream. If I can do it, you can do it.

---

## The stages

### Stage 0 — Simulation Foundation (now)
*"Make a robot move without owning one"*

Stack: Mac Mini M4 + MuJoCo + LeRobot + Genesis + Ollama (local LLM robot brain).

Milestones — each one is an episode:
1. Humanoid model standing (well... flopping) in MuJoCo
2. Teleoperate the sim robot with a game controller
3. Run a pretrained LeRobot policy — robot picks something up
4. Build a home scene (kitchen, laundry) and script a task
5. Talk to the robot via a local LLM running on the Mac Mini — no cloud

### Stage 1 — Real Hardware, Small
*"A robot arm on the kitchen table"*

LeRobot SO-101 arm kit (~$110-350), webcams, imitation learning. Goal: one genuinely useful micro-task that makes a stranger say "wait, you built that?"

### Stage 2 — Scale Up
RTX rig + NVIDIA Isaac Sim, first packaged "app" prototype, and a seat in the first wave when home robot platforms open their developer programs.

### Stage 3 — Real Apps for Real Home Robots
Task packs, customization, and local-brain options for the robots people actually own. The goal since page one.

---

## Repo map
- [build-log.md](build-log.md) — every session: what I tried, what broke, the fix, and whether it's episode-worthy
- `logs/` — session details as they accumulate
- More repos coming as the journey progresses: `home-robot-sims`, `so101-experiments`

---

## The origin story

When I was a kid I read *Runaway Robot* and never stopped wanting one. For forty years the tools didn't exist for a non-engineer to build robot software. Now they do. This repo is the receipt.

⭐ Star the repo to follow the journey.
