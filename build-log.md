# Robot Build Log
*Started July 2026 — Mac Mini M4 era*

## How to use this file
After each build session, add an entry at the TOP of the Log (newest first). Honest and fast beats polished — this is raw material for episodes and a searchable memory of every fix.

---

## Stage 0 install checklist
- [x] External SSD formatted (APFS), folder structure: `/robot-journey/models` created (skipping `/conda-envs` — conda manages its own env dir)
- [x] Miniconda installed (Apple Silicon build) — `/Volumes/RobotSSD/miniconda3`
- [x] Conda env created — **`mujoco-env` / Python 3.11** (deviation from plan: `robots` / 3.10)
- [x] MuJoCo installed + `python -m mujoco.viewer` opens
- [x] Humanoid model loaded and flopping (📹 Episode 1!)
- [ ] LeRobot installed from source
- [ ] Genesis installed (optional)
- [ ] Ollama installed + 7-8B model pulled and responding

---

## Log

### YYYY-MM-DD — [Session title]
- **Goal:**
- **What I tried:**
- **What broke:**
- **The fix:**
- **Why it broke (in plain English):**
- **Time spent:**
- **📹 Episode-worthy?** yes/no — [what's the moment?]

### 2026-07-19 — The Three Pythons (pygame moves into the wrong house)
- **Goal:** Install pygame in mujoco-env (prep for game controller teleop).
- **What I tried:** `conda activate mujoco-env` then `pip install pygame` in a terminal left over from the day before.
- **What broke:** `CondaError: Run 'conda init' before 'conda activate'` — but pygame still "successfully installed." Plot twist: it installed into the wrong Python (conda base, 3.13) instead of mujoco-env (3.11).
- **The fix:** Quit Terminal, reopen with the SSD mounted, `conda activate mujoco-env` (prompt shows `(mujoco-env)`), reinstall pygame. Then evicted the stray copy with `/Volumes/RobotSSD/miniconda3/bin/pip uninstall pygame`.
- **Why it broke (in plain English):** The old terminal session started before RobotSSD had mounted. The conda setup note in `.zshrc` was there all along, but it ran before the drive woke up and failed *silently* (the `2> /dev/null` from July 11's gotcha — it struck for real this time). It fell back to a bare PATH entry, so pip worked but pointed at conda base's Python. The forensic clue: the first install downloaded a `cp313` wheel (Python 3.13 = conda base); the correct install downloaded `cp311` (mujoco-env). Wheel filenames tell you which Python is answering. Also learned: `pip3` isn't one command — it's whichever pip is first in PATH for that tab, and `cd` never changes which Python runs.
- **New ritual:** Mount SSD first, terminal second. Always confirm `(mujoco-env)` in the prompt before installing anything.
- **Time spent:** ~30 min
- **📹 Episode-worthy?** yes — "My Mac has three Pythons and pygame moved into the wrong one." Detective arc: silent error → wrong-house install → cp313 clue in the wheel filename → `pip show` confession → eviction. Before/after shot of the wheel filenames (cp313 vs cp311) is the receipt.

### 2026-07-11 — Nuke and pave: clean Miniconda reinstall + first humanoid flop

- **Goal:** Activate `mujoco-env` and load a humanoid in MuJoCo. Record Episode 1 footage.

- **What I tried:** `conda activate mujoco-env` in a fresh Terminal.

- **What broke:** A cascade. In order:
  1. Tried to "start" Miniconda by double-clicking the `conda` file in Finder. Got a help dump and a dead `[Process completed]` window.
  2. `conda activate mujoco-env` → `EnvironmentNameNotFound`. `conda info --envs` showed only `base`. `ls /Volumes/RobotSSD/miniconda3/envs` → **empty**. The env from the previous session was simply gone. Never determined why.
  3. Went to record the reinstall — discovered the **Mac Mini has no built-in microphone**. Screenshot app's Microphone dropdown was greyed out because there is genuinely no input device. Abandoned audio; recording silent, will voice over later.
  4. After clean reinstall, `conda create` failed with `CondaToSNonInteractiveError` — Anaconda's Terms of Service not accepted on the new install.
  5. Typed `mkdir`/`cd`/`curl` into a Terminal that was still running `mujoco.viewer` in the foreground. Commands went nowhere. `Ctrl+C` didn't release it either — the GUI render loop swallowed the interrupt.

- **The fix:**

  Full uninstall, **in this order** (order matters):

      conda init --reverse zsh
      rm -rf /Volumes/RobotSSD/miniconda3
      rm -rf ~/.condarc ~/.conda

  Reinstalled from `Miniconda3-latest-MacOSX-arm64.sh`, custom path `/Volumes/RobotSSD/miniconda3`, answered `yes` to shell init. Then `conda config --set auto_activate_base false` (throws a harmless alias WARNING — not an error).

  Accepted the Terms of Service:

      conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
      conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r

  Rebuilt the env, installed MuJoCo, pulled the humanoid:

      conda create -n mujoco-env python=3.11 -y
      conda activate mujoco-env
      pip install mujoco
      mkdir -p /Volumes/RobotSSD/robot-journey/models
      cd /Volumes/RobotSSD/robot-journey/models
      curl -O https://raw.githubusercontent.com/google-deepmind/mujoco/main/model/humanoid/humanoid.xml
      python -m mujoco.viewer --mjcf=/Volumes/RobotSSD/robot-journey/models/humanoid.xml

  Escaped the hung viewer with a new Terminal tab (`Cmd+T`) instead of fighting it.

- **Why it broke (in plain English):**
  - **Conda is not an app.** There's no icon, no window. It's a command you type into a Terminal that's already open. Double-clicking it just runs it with no instructions, so it prints its help menu and dies.
  - **`conda init --reverse` must come before `rm -rf`.** Reverse-init strips conda's block out of `~/.zshrc`. Delete the folder first and every new Terminal tries to load a conda that no longer exists.
  - **The ToS error is legal, not technical.** Anaconda changed their terms; conda now refuses to download from their default channels until you explicitly accept. Nothing was broken.
  - **A foreground program owns the Terminal.** While `mujoco.viewer` runs, that tab is hostage — anything you type is ignored. And `Ctrl+C` interrupts the *Python process*, but a GUI render loop can swallow it. Open a second tab (`Cmd+T`) instead of wrestling with it. Every new tab starts clean — you must `conda activate mujoco-env` again.
  - **The humanoid falls because it has no policy.** It has a body, joints, and physics — but nothing telling the muscles what to do. It's not broken. It's a ragdoll, because there's no brain yet. Teaching it to *not* fall is the rest of this journey.

- **Gotcha for future me:** The conda init block in `.zshrc` ends with `2> /dev/null`. That means **if the SSD isn't mounted, conda fails silently** — `command not found`, no explanation. If conda ever "disappears," check the drive is mounted before panicking.

- **Time spent:** ~2 hours.

- **📹 Episode-worthy?** **YES — this IS Episode 1.** The arc: install conda → environment vanishes → nuke and pave → ToS plot twist → no-microphone discovery → humanoid finally flops.

### 2026-07-04 — Log created
- **Goal:** Start the build log habit before touching a terminal.
- **What broke:** Nothing yet. Enjoy this feeling. It will not last. 🤖
