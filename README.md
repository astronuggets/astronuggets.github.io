[README (3).md](https://github.com/user-attachments/files/34941671/README.3.md)
# Astronuggets // Mars Outpost Command

A browser game where students run a Mars outpost in Jezero Crater. Power is scarce, the base wears down every sol, and every choice trades one need against another: life support, radiation shielding, food and science.

Built for the NASA Space Apps Challenge. Space-themed STEM content often oversimplifies engineering trade-offs, or buries them under too much complexity. This game tries to make those trade-offs tangible and fun for ages 7 to 12.

## Contents

1. [Quick start](#quick-start)
2. [Game modes](#game-modes)
3. [Master guide to every feature](#master-guide-to-every-feature)
   - [Goal, win and lose](#goal-win-and-lose)
   - [A sol, step by step](#a-sol-step-by-step)
   - [Every number on screen](#every-number-on-screen)
   - [Power](#power)
   - [The five buildings and every action](#the-five-buildings-and-every-action)
   - [Upgrades](#upgrades)
   - [Scrap](#scrap)
   - [Rock samples and research](#rock-samples-and-research)
   - [Evening decisions](#evening-decisions)
   - [Weather: flares and dust storms](#weather-flares-and-dust-storms)
   - [The Great Dust Storm](#the-great-dust-storm)
   - [The rover and the map](#the-rover-and-the-map)
   - [Mission Control and Earth](#mission-control-and-earth)
   - [Moving around: views, controls and interiors](#moving-around-views-controls-and-interiors)
   - [Menus, panels and settings](#menus-panels-and-settings)
   - [Learning features](#learning-features)
   - [Endings and scoring](#endings-and-scoring)
   - [Story Mode](#story-mode)
   - [Mars Base Jr.](#mars-base-jr)
   - [Home screen](#home-screen)
4. [NASA data and resources](#nasa-data-and-resources)
5. [Built with](#built-with)
6. [Testing](#testing)
7. [Known limits](#known-limits)

## Quick start

Open `index.html` in a modern browser. It is one self-contained file. It needs an internet connection the first time to load Three.js and the fonts, and to fetch recent solar flares from NASA. If the NASA request fails, the game falls back to archived flare data.

You can skip the home screen with a link parameter: `index.html?mode=jr`, `?mode=full` or `?mode=story`. An old-style `?age=7` also works (under 9 starts Jr., otherwise the full game).

## Game modes

| Mode | Recommended age | What it is |
|---|---|---|
| **Mars Base Jr.** | 7 to 8 | A simpler 24-sol mission with three meters (life support, radiation shield, power), a smaller map and a gentler pace. |
| **Outpost Command** | 9+ | The full game: five buildings, hidden odds, nightly emergencies, a science goal and a Great Dust Storm on sols 17 to 20. Survive to Sol 20 with the goal met. |
| **Story Mode** | 9+ | The full game engine with no sol limit and no science quota. Pick optional goals and see how long the base lasts. |

Ages are only a suggestion; any player can pick any mode.

---

# Master guide to every feature

This guide covers the full game (Outpost Command). Story Mode shares all of it except where [noted](#story-mode). Mars Base Jr. has its own simpler rules, described [last](#mars-base-jr).

## Goal, win and lose

- **Mission:** run Jezero Base for **20 sols** (a sol is one Mars day). Collect the science goal **and** keep the crew alive through Sol 20.
- **Science goal** depends on difficulty: **Easy 60, Normal 80, Hard 100**.
- Reaching the goal early does **not** end the game. You must still survive to the end of the mission. Science is capped at 125% of the goal.
- **You lose** if **O₂, Shield or Food reaches 0%**, or the crew's **radiation dose reaches 100%**. Surviving all 20 sols without enough science is also a loss.
- The base **wears down faster every sol**, so early comfort never lasts.

### Difficulty (Settings)

| | Easy | Normal | Hard |
|---|---|---|---|
| Science goal | 60 | 80 | 100 |
| Power capacity | +3 kW | standard | -1 kW |
| Life-support drain | 0.8x | 1x | 1.2x |
| Radiation dose | 0.6x | 0.8x | 1x |
| Flare days / dust days | 2 / 1 | 3 / 2 | 4 / 2 |
| Automatic weather warning | 50% of weather days | 25% | none, check the Outlook |

## A sol, step by step

1. **Read the forecast** at the top and in the event log.
2. **Spend power** on actions in the five buildings, send the rover, collect scrap, answer Earth.
3. Press **End Sol & Decide**. You must have done something (an action, scrap pickup and so on) before the button unlocks; a base left unattended is penalised.
4. An **evening decision** appears: one emergency, four unlabeled plans.
5. **The night passes:** supplies drain, standby power is paid, modules that are ON produce their free gains, weather damage lands, new power arrives, and the next sol begins.

On a flare or dust day there is **no evening decision**; that day is just a labeled regular day. In the Great Dust Storm, surprise events pop up while you work, plus one evening decision. See below.

## Every number on screen

**Top bar (HUD)**

| Pill | Meaning |
|---|---|
| SOL | Current sol / mission length (shows ∞ in Story Mode) |
| O₂ | Oxygen. Reach 0% and you lose |
| SHIELD | Radiation shielding. Thin walls let radiation in. 0% loses |
| FOOD | Food stores. 0% loses |
| DOSE | Crew radiation dose. 100% loses. Only goes down through special actions |
| POWER | kW you can still spend today |
| BATT | Stored battery energy (kW) |
| NEXT SOL | Power you are expected to have tomorrow |
| SCIENCE | Points toward the goal |
| SCRAP | Usable scrap for upgrades and repairs |
| RAW | Raw scrap that still has to be processed |
| SAMPLES | Rock samples (a Research stat) |
| Weather label | Appears on flare days, dust days and during the Great Dust Storm |

Buttons: **Home**, **First-Person EVA [V]**, **How to Play**, **NASA Data**, **Sound**, **Settings**, **Replay Cutscene**, **Reset View**.

**Building stats** (shown on each building's panel and wall screens)

| Stat | Belongs to | What it does |
|---|---|---|
| Crew morale | Habitat | Low morale means sloppy work, slower science and leaking air |
| Panel cleanliness | Solar | Cleaner panels make more power every sol |
| Instrument calibration | Research Lab | Scales science from lab actions |
| Crop health | Food Silo | Scales harvests |
| Water supply | Food Silo | Under 40% cuts harvests; thirsty crews lose air and morale |
| Antenna alignment | Comms | Scales transmissions |

**Stat effect rule:** a stat at **70% or more** gives full effect, **40 to 69%** gives 75%, **below 40%** gives 50%. Actions tell you when a low stat is hurting them.

## Power

- Each sol you get a **power budget** in kW. With panels **deployed** it is your max power scaled by panel cleanliness (50% to 100%). With panels **stowed**, or on a dust day, it is only about **5 kW**.
- **Stow / Deploy Panels** is free but only once per sol. Deploying them brings full power; stowing protects them from dust.
- **Standby cost:** every module that is switched ON uses power each night: Habitat 1 kW, Silo 1 kW, Research Lab 2 kW, Comms 1 kW. The Solar Array has none.
- **Module switch:** turning a module **OFF** saves its standby kW but its stats wear **twice as fast** and its buttons lock (except shelter actions).
- **Free gains while ON:** the Habitat adds oxygen and shield each night, the Silo adds food, the Lab and Comms each add 1 science. Upgrades increase these.
- **Battery:** *Charge Battery Bank* stores kW; *Use Battery Power* spends it. Extra capacity comes from solar upgrades.
- **Blackout:** if you run out of power overnight every module shuts down and nothing runs on its own.
- **Power saver:** in emergencies the base switches modules off for you to keep life support alive.

## The five buildings and every action

Every action costs power, scrap or a stat. Each can be used **once per sol** unless noted. All of them appear both as **wall buttons inside the building** and as buttons on the building's **control panel**.

### 🏠 Habitat (oxygen, shield, morale)

| Action | Cost | Effect |
|---|---|---|
| Run MOXIE O₂ Cycle | 3 kW | Converts Mars CO₂ into +9% oxygen |
| Reinforce Shielding | 3 kW | +10% shield |
| Activate Storm Shelter | 2 kW | Shields the crew from a flare today (locks outside work). Prepared the day before it works better; if tomorrow is a known flare it prepares early lockdown instead |
| Crew Movie Night | 1 kW | Morale +20% |
| Crew Exercise Hour | 1 kW | Morale +15% |
| Scrub Air Filters | 1 kW | +3% oxygen. **Dust storm prep** when used the day before |
| **Extra Work Shift** | -12 morale | **+3 kW today.** Needs morale of 45+ |
| Module Power switch | standby 1 kW | ON/OFF |
| Upgrade Habitation | scrap | See [Upgrades](#upgrades) |

### ☀️ Solar Array (power)

| Action | Cost | Effect |
|---|---|---|
| Stow / Deploy Panels | 0 kW | Toggle panel angle. Stowed protects from dust, deployed makes full power |
| Brush Dust Off Panels | 1 scrap | Cleanliness back to 100% and +2 kW |
| Shake Panels Clean | 1 kW | Cleanliness +25% |
| Charge Battery Bank | 3 kW | Stores +2 kW |
| Use Battery Power | stored kW | Adds stored energy to today's power |
| **Overclock Inverters** | 1 kW, -15 clean | **+4 kW now.** Needs deployed panels at 60%+ clean |
| Upgrade Solar Array | scrap | See [Upgrades](#upgrades) |

### 🔬 Research Lab (science)

| Action | Cost | Effect |
|---|---|---|
| Run Laser Spectrometer | 4 kW | +9 science (scaled by calibration) |
| Calibrate Instruments | 1 kW | Calibration +40% |
| **Core Drill Sample** | 2 kW, -8 calib | **+2 rock samples** (+3 at Lab Lv 3+). Needs calibration 40+. Locked while sheltering |
| **Deep Rock Analysis** | 3 kW, 6 samples, 1 scrap | **+15 science.** Needs calibration 70+. The biggest single science action |
| Analyze Rock Samples | 1 kW | Turns all your samples into science, one for one |
| Secure Instruments | 1 kW | **Storm prep** for the Lab |
| Module Power switch | standby 2 kW | ON/OFF |
| Upgrade Research Lab | scrap | See [Upgrades](#upgrades) |

### 🌱 Food Silo (food, crops, water, scrap workshop)

| Action | Cost | Effect |
|---|---|---|
| Harvest Hydroponic Crops | 3 kW | +9% food (scaled by crop health and water) |
| Tend & Mist Crops | 1 kW | Crop health +30%, water +25% |
| Melt Ice for Water | 2 kW | Water +35% |
| **Harvest Feast** | 2 kW, -12 crop, -8 water | **+14% food and +8 morale.** Needs crop 50+ and water 30+ |
| Salvage Spare Parts | 2 kW | +1 usable scrap |
| **Process Raw Scrap** | 1 kW | Turns up to 3 raw scrap into usable scrap. Can be pressed more than once a sol |
| Cover Crops | 1 kW | **Storm prep** for the Silo |
| Upgrade Food Silo | scrap | See [Upgrades](#upgrades) |

### 📡 Comms Dish (Earth link, weather outlook)

| Action | Cost | Effect |
|---|---|---|
| Transmit Science to Earth | 3 kW | +6 science and +1 scrap (scaled by alignment) |
| Realign DSN Antenna | 1 kW | Alignment +45% |
| **Live Call Home** | 2 kW, -10 align | **+15 morale and +3 science.** Needs alignment 60+ |
| Weather Outlook | 1 kW | See the next 1 to 3 sols of space weather |
| Receive: Mission Control | free | Open requests from Earth |
| Broadcast: Send Report | 1 kW | Sends finished requests to Earth |
| Stow Dish | 1 kW | **Storm prep** for the dish |
| Upgrade Comms Array | scrap | See [Upgrades](#upgrades) |

Buttons that go outside are **locked while the crew is sheltering**. A button greyed out on the wall or panel says why (not enough power, scrap, a stat too low, or module OFF).

## Upgrades

Every building has **four levels**, costing **2, then 4, then 7 scrap**. Each level gives a bigger bonus.

| Building | Level 2 | Level 3 | Level 4 |
|---|---|---|---|
| Habitat | +2% O₂ and shield per action, +1% passive, wear -10% | +5% per action, +2% passive, flare dose -15%, wear -25% | +9% per action, +3% passive, flare dose -30%, wear -40% |
| Solar | +1 kW max, battery +2, wear -10% | +1 kW more (+2 total), battery +4, wear -25% | +2 kW more (+4 total), battery +6, wear -40% |
| Research | +2 science per run, wear -10% | +4 per run, spectrometer wears less, wear -25% | +7 per run, +1 science each sol on its own, wear -40% |
| Silo | +2% food per harvest, +1% passive, wear -10% | +5% per harvest, +2% passive, water lasts longer, wear -25% | +9% per harvest, +3% passive, wear -40% |
| Comms | Outlook sees 2 sols, +2 science per send, wear -10% | Outlook sees 3 sols, +4 science, +10% auto-warnings, wear -25% | +7 science, +1 science each sol on its own, +20% auto-warnings, wear -40% |

Upgraded buildings show a blue badge. The rover has its own upgrades and modules (see [The rover](#the-rover-and-the-map)).

## Scrap

- **Raw scrap** appears as glowing amber markers on the map: **1 to 3 pieces each sol**, up to 14 on the map. Collect one by clicking it, or aim and press **E** within about 9 m. The minimap shows them as yellow squares.
- Raw scrap **cannot be used** for upgrades or repairs. Process it with **Process Raw Scrap** in the Food Silo (1 kW, up to 3 at a time).
- **Usable scrap** also comes from Salvage Spare Parts, Transmit Science, some decisions, Mission Control rewards and rover trips (as raw).
- Uses: upgrades, rover repairs and modules, Brush Dust Off Panels, Deep Rock Analysis, decision costs.

## Rock samples and research

- **Rock samples** are a Research stat with their own HUD counter.
- Sources: **rover trips**, the **Core Drill Sample** action, and some decisions.
- Uses: **Analyze Rock Samples** (cheap, one science per sample) or **Deep Rock Analysis** (6 samples for +15 science, a much better rate but with strict conditions).
- Science from lab actions is scaled by **instrument calibration**. Keep it up with Calibrate Instruments and avoid actions that wear it.

## Evening decisions

After End Sol, an emergency presents **four plans**.

- Plans are **not labeled** safe or risky, and their **order is shuffled** every time.
- Every plan shows **visible costs and gains** (power, scrap, O₂, shield, food, science, morale and stat changes).
- **Gamble plans** show both outcomes ("If it works / If it fails") but **hide the odds**.
- Some plans have effects **tomorrow** ("What happens next").
- A plan you cannot afford, or one that could end the mission outright, is locked. At least two are always available.
- After choosing you see the result, a **Real science** fact and a link to the NASA or CSA source.
- Keys **1 to 4** pick a plan, **Enter** continues.

**35 events**, picked to fit the situation: Solar Storm Tomorrow, Dust Storm Tomorrow, A Spacewalk Before the Storm, Science Under Dark Skies, Air Is Getting Thin, Pantry Getting Empty, Walls Are Wearing Thin, Power Budget Is Tight, Rover Signal Is Wobbly, The Crew Is Tired, Strange Layered Rock, Hiss! A Pressure Leak, Earth Wants Extra Data, Gear Needs Attention, Dust Devil Outside, Ice Under the Soil, Surprise Particle Burst, Scrap Field Spotted, The Air Filters Are Clogged, Dusty Solar Panels, Sleep Schedule Fight, Spots on the Lettuce, Too Many Rock Samples, A Tool Snaps, Two Experiments One Lab, A Bitter Cold Night, A Crew Member Gets Hurt, Extra Lights for the Plants, The Dish Is Wobbling, The Food Freezer Is Warming, A Trip to the Ancient Delta, The Airlock Seal Hisses, A Cheerful Feast or Careful Meals, A Quarrel About the Chores, The Safety Beacon Test.

The night **before** a flare or dust day, the decision is a **preparation** decision whose result carries into the weather day.

## Weather: flares and dust storms

Flare and dust days are **whole days** with a label in the HUD. There is **no evening decision** on them; your preparation decides what you lose.

**Schedule:** flares and dust days fall between sols 3 and 15, spaced apart, in the numbers shown in [Difficulty](#difficulty-settings). Flare events come from real NASA DONKI records (live recent flares when online, archived otherwise), with their class (A, B, C, M, X) setting severity.

**Knowing ahead:** some weather days **warn you a sol ahead on their own** (chance depends on difficulty and Comms upgrades). The **Comms Weather Outlook** reveals the rest, looking 1 to 3 sols ahead.

**Prepare the day before**, with one prep button per building. A prepared building is protected; an unprepared one is damaged:

| Building | Prep action | Flare damage if unprepared | Dust damage if unprepared |
|---|---|---|---|
| Habitat | Prepare Storm Shelter (flare) / Scrub Air Filters (dust) | Large radiation dose to the crew | O₂ -6, morale -8 |
| Solar | Stow Panels | Open panels get dirty (-15 clean) | Deployed panels are scratched: **max power -1 kW forever** |
| Research Lab | Secure Instruments | Calibration -30 | Calibration -20 |
| Food Silo | Cover Crops | Crop health -25 | Crop health -20 |
| Comms | Stow Dish | Alignment -30 | Alignment -25 |
| Rover | Cover Rover | May break (see rover) | May break (see rover) |

Also: bring the rover home before a storm, charge the battery before a dust day (power drops to about 5 kW), and shelter on a flare day. **Sheltering late** protects less than preparing the day before, and an unprepared crew can also lose science to glitching electronics.

## The Great Dust Storm

- Hits on **Sol 17** and lasts **4 sols** (to Sol 20), even if your science is done.
- Power is only about **5 kW** a sol, so keep just the modules you need ON.
- Each storm sol has **surprise events that pop up on their own while you work** (1 to 2 per sol, at least 45 seconds apart, never while another menu is open), plus **one evening decision**.
- **10 storm-only events:** Power Is Collapsing, Dust in the Air Plant, Radio Blackout, Plants Need Light, Cabin Fever, A Panel Has Torn Loose, The Rover Is Out There, A Pressure Alarm, Dust on the Samples, The Longest Night. Their facts reference the real 2018 global dust storm that ended the Opportunity rover mission.
- The Great Dust Storm is also announced in the tutorial and the "Sols 17 to 20" slide.

## The rover and the map

**The map** has four glowing site beacons (click one to open it) and the minimap shows sites, scrap and the rover.

| Site | Trip | First-visit science | Scrap |
|---|---|---|---|
| Sand Dune Field | 2 sols | 4 | 0 |
| Iron-Rich Ridge | 3 sols | 7 | 1 |
| Old Impact Crater | 3 sols | 8 | 1 |
| Ancient River Delta Mesa | 4 sols | 11 | 2 |

- **Send the rover:** costs **2 kW** (1 kW with the Solar Charger). It drives out, explores, and brings back **samples** (science to analyze in the Lab) and **raw scrap**. Visiting a site again gives only about **40%**.
- **Survey on foot (EVA):** in first person, walk within 9 m of a beacon for **+2 science** and **+2% radiation dose**, once per sol per site.
- **Recall:** bring the rover home early. If it is already exploring it keeps **60%** of its samples; if it has not arrived it returns empty-handed.
- **Storms can always hurt the rover.** On a flare or dust day an exploring rover, **and** one parked at base, can break. Base risk is **40%**, **30%** with Level 1 and **20%** with Level 2, and it can **never drop below 10%**, even with the Storm Shell. **Cover the rover** the day before to protect it at base.
- **Damage:** an exploring rover that is hit comes back **1 sol late**, loses **30%** of its samples and needs a **2 scrap repair**. A rover broken at base cannot go anywhere until repaired and shows a red warning light.
- **Rover panel** (click the rover):
  - **Recall**, **Repair** (2 scrap)
  - **Upgrade** Lv 1 (3 scrap): trips 1 sol shorter, less storm risk. Lv 2 (3 scrap): even less storm risk and **+25%** science from drill upgrades
  - **Jobs at base:** **Cover the rover** (1 kW, storm prep), **Fetch scrap** (1 kW, brings back up to 2 raw scrap), **Sweep the panels** (1 kW, +25% cleanliness)
  - **Modules:** **Cargo bay** (3 scrap, +30% science), **Solar charger** (2 scrap, trips cost 1 kW), **Storm shell** (3 scrap, halves the break chance)
- The rover drives at about 70% of its original speed and avoids boulders, the landing pad and the base deck.

## Mission Control and Earth

- **Six requests** arrive on sols **2, 5, 8, 11, 14 and 17**, each with a 6-sol deadline: Data Downlink, Rock Analysis, Fresh Food Report, Salvage Survey, Rover Expedition, Power Reserve Test.
- Do the task, then use **Broadcast: Send Report** (1 kW). **Earth replies after a delay** (about 2 sols, a stand-in for the real 3 to 22 minute light delay each way), shortened by Comms upgrades. Rewards are **science and scrap**.
- **Receive: Mission Control** opens the request list. Progress is tracked for you.

## Moving around: views, controls and interiors

| Control | Action |
|---|---|
| Click a building | Open its control panel |
| Click a beacon / the rover | Open the site / rover panel |
| `V` | Toggle first-person view |
| `W` `A` `S` `D` | Move (first person) |
| Space | Jump |
| `E` | Enter a door, press a wall button, collect scrap |
| Mouse | Look around (first person); drag to orbit and scroll to zoom in the overview camera |
| `1` to `4`, `Enter` | Pick a decision plan, continue |
| Reset View | Put the overview camera back |

- **Orbit view** (default) shows the whole base; **first-person EVA** lets you walk outside, survey sites and collect scrap.
- **Walk into any building** through its front door. Inside you see **wall screens** and **physical buttons** with the same actions as the control panel, a **power switch**, and **upgrade pedestals**. Special pedestals (Mission Control, rover samples) are marked differently from routine buttons.
- Doors only work from the front, with a short lock so they cannot flicker, and you exit to a clear spot outside.
- **Interior signs** show the status (PRESS, DONE, LOCKED, OFF), the cost and a short description. Long costs shrink to stay readable.
- **Hover tags** and an aiming **reticle** with an on-screen prompt tell you what a click or `E` will do.
- **Minimap** ("Outpost Radar", or "EVA Radar" in first person) shows you, the buildings, sites, scrap and the rover.
- **Day and night** animate when you end a sol; the sky turns red on dust days.

## Menus, panels and settings

- **Intro cutscene:** a 3-step landing sequence (mission objective, touchdown, controls). Use **Skip Intro**, or **Replay Cutscene** at any time.
- **How to Play:** a collapsible guide covering the goal, the sol cycle, every number, the five modules, scrap and the rover, controls, forecasts and surprises.
- **Tutorial:** a 6-step illustrated tour opens automatically the first time (mission, five numbers, buildings, ending a sol, reading the forecast, the Great Dust Storm). **Watch Tutorial** replays it.
- **Settings:**
  - Music and volume, sound effects and volume
  - Building labels, minimap, screen shake
  - Look sensitivity, field of view
  - **Difficulty** (Easy, Normal, Hard)
  - A quick glossary (sol, kW, dose, O₂, shield, standby, scrap, EVA)
  - **Mission statistics**, **How to play**, **Restart mission** (asks twice)
  - Settings are saved in the browser.
- **Building control panel:** a drawer for each building with live stat tiles, every action and its cost, and the module switch.
- **Mission statistics:** a chart of your journey sol by sol (oxygen, shield, food, dose, science, power) with a legend.
- **Per-sol performance report:** a letter grade, what changed, what was well used, "Pattern spotted" notes (for example "Food has dropped about 6 points a sol") and a coaching tip.
- **NASA Data panel:** where each fact and data set comes from, with live or archived status for the flare feed.
- **Event log:** shows today's forecast, what happened overnight, and a "Why?" line explaining the science.
- **Toasts and wall messages** confirm every action.

## Learning features

- Every decision ends with a **Real science** fact and a source link.
- The event log explains **why** the game does something (for example why Mars crews shelter behind regolith or water).
- Hover text and wall signs explain each action's trade-off before you press it.
- **Command style summary** at the end describes how you played.
- The game uses real mission references: Spirit's sand trap, Opportunity and the 2018 storm, Perseverance's MOXIE and sample depot, Curiosity's RAD, Jezero's ancient delta, perchlorate in Martian soil.

## Endings and scoring

- **Victory:** survive to the end of Sol 20 with the science goal met.
- **Defeat:** life support or shielding failed, food ran out, the crew hit the radiation limit, or you ended with too little science.
- **Grade (stars):** one star for winning, one for a final dose under 50%, one for finishing with O₂, shield and food all above 30%.
- The end screen also shows your decisions made, upgrades bought, your command style, and a real-world takeaway. A final slide sequence reviews the mission.

## Story Mode

Story Mode reuses the whole full game with these changes:

- **No sol limit and no science quota.** The sol counter shows ∞ and science has no cap.
- **No Great Dust Storm.** Random flares and dust storms keep coming after sol 20.
- The base still **wears down faster every sol**, so every run eventually ends.
- **Pick your goals** on the home screen (all optional, two are pre-ticked):
  - Survive to Sol 10 / 20 / 40
  - Fully upgrade one building / upgrade all 5 buildings
  - Collect 100 science
  - Ride out 3 solar flares
  - Finish 5 rover trips
  - Reach Sol 15 with radiation under 25%
- A **Story Mode panel** shows your day count, your best run and your goals with check marks, and a toast celebrates each goal you reach.
- When the base fails you see **how many sols you survived** and how many goals you reached. Your **best run** is saved in the browser.
- The intro and tutorial text change to describe Story Mode, but some screens still mention the 20-sol mission.

## Mars Base Jr.

A simpler version for ages 7 to 8, with its own interface and rules:

- **24 sols.** Keep the crew alive until a rescue ship arrives on **sol 25**. The **Great Dust Storm starts on sol 20**.
- **Three meters:** **Life Support**, **Radiation Shield** and **Power**.
- **Five modules**, shown as cards you tap and on a smaller map: Habitat (air), Food Silo (food and air), Research Lab (builds the shield), Comms Dish (talks to Earth) and Solar Array (power, always on). Each uses a set amount of power; switching a module OFF saves it.
- **Power:** the Solar Array makes **9 kW** (12 and 15 when upgraded). Dust storms cut power to about **45%**, the Great Dust Storm to about **40%**.
- **Upgrades:** each module can be upgraded twice for **6 kW, then 9 kW** of that day's power, and **only one upgrade per sol**. Upgrades multiply gains by 1.3 and 1.6.
- **Weather:** calm days, solar flares and dust storms. The **Comms Dish**, when ON, shows tomorrow's weather, cuts flare damage (to 60%, 40% and 25% with upgrades), softens the night's damage and sends nightly survival tips.
- **Evening events** with three plans each (safe, balanced or bold, not labeled), some with a hidden gamble, and a special set for the storm.
- A **tray** of module cards at the bottom, a large **End Sol** button, friendly forecast banners and a short tutorial.

## Home screen

- Three cards: **Mars Base Jr.** (ages 7 to 8), **Outpost Command** (9+), **Story Mode** (9+), each with an age badge, a short description and tags.
- The Story card opens a **goal picker** with a Back button.
- It works on phones (one column) and desktop, and is built over a blurred picture of the base.

---

## NASA data and resources

- NASA DONKI space weather database (solar flares): https://ccmc.gsfc.nasa.gov/tools/DONKI/
- NASA Open APIs: https://api.nasa.gov/
- NASA Open Science Data Repository and RadLab radiation data: https://osdr.nasa.gov/bio/repo/ and https://visualization.osdr.nasa.gov/radlab/
- NASA Mars Trek (Jezero Crater and Mars terrain): https://trek.nasa.gov/mars/
- Curiosity RAD, Perseverance MOXIE, the Opportunity 2018 storm and the Spirit rover sand event are used as facts in the in-game text.
- Canadian Space Agency food production toolkit: https://www.asc-csa.gc.ca/eng/youth-educators/toolkits/food-production/

Flare and storm days are drawn from real archived flare events. They are an educational model, not a physical simulation.

## Built with

- A single HTML file with JavaScript
- [Three.js](https://threejs.org/) r160 (MIT license) for the 3D base, loaded from unpkg
- Orbitron and Space Grotesk fonts from Google Fonts (SIL Open Font License)
- All buildings, the rover and the interface are built in code, so there are no external image or model files
- Claude Code (Anthropic) was used to help write and test the game
- Playwright and Node.js for testing, ffmpeg for the trailer video

## Testing

The game was checked with scripted tests that mock the 3D layer and the browser:

- A smoke test of every building, action, panel and menu (about 430 checks)
- A battery of full playthroughs, storm tests, decision fuzzing and weather tests
- Tests for each recent feature: raw scrap processing, the new actions, rover storm risk and modules, surprise storm events, Story Mode goals
- A separate smoke test for Mars Base Jr.
- Browser tests (Playwright) for the home screen, layouts at several screen sizes, and full flows in both versions

## Known limits

- The 3D scene needs WebGL. The automated tests mock the 3D layer, so the visuals were checked by hand rather than by automated screenshots.
- Mars Base Jr. has its own simpler rules and does not include raw scrap, the rover jobs or Story Mode.
- Story Mode reuses the full game's intro and tutorial screens, which are only partly adapted to it.
- The in-game "How to Play" text has not been rewritten for every new feature, so this guide is the most complete reference.
