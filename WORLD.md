# How the Game World Works: Blight of the Immortals

Descriptions based on the 16 screenshots in the wargamer.fr preview
(<https://www.wargamer.fr/apercu-de-blight-of-the-immortals/>, April 2016) and the
article text, plus in-game tutorial screenshots (saved in
[reference/screenshots/](reference/screenshots/)) and frames from the developer's
4-minute intro video (saved in [reference/video-intro/](reference/video-intro/)). Rules and numbers are in [GAMERULES.md](GAMERULES.md). This file covers what
the world **looks like** and how its parts fit together.

---

## 1. The map

- **A hex-based overworld.** The ground is made of large hexagonal tiles. Each hex
  has one terrain type, and hexes of the same terrain cluster into regions such as
  forest belts, mountain ranges and swamp patches.
- **Terrain is visible at a glance:**
  | Terrain   | Look |
  |-----------|------|
  | Plains    | Open light-green grass (the default ground) |
  | Forest    | Dense dark pine woods |
  | Mountains | Grey rocky peaks, often in ridges |
  | Desert    | Sandy tan ground with red-brown rock outcrops |
  | Swamp     | Darker, saturated green with ponds and reeds |
  | Water     | Blue rivers winding between hexes, plus large lakes or inland seas |
- **A triangular waypoint grid covers the whole map.** Faint dashed white lines criss-cross
  the terrain in a **triangular lattice**. Every intersection is a **waypoint**, and one edge between
  two neighbouring waypoints is **1 League**. Units move only along these edges, from
  waypoint to waypoint, and can stop on an **empty waypoint** in open country, not only at settlements.
- **Settlements, Mana Pools and monster lairs sit on waypoints.**
  Some edges are **roads**, drawn as solid beige lines, usually linking settlements.
  Travel time per League depends on the edge: road 1x,
  plains/forest/desert 1.5x, mountain/swamp 2x.
  - Example: a Human Swordsman army (4h/League by road) moving 1 League across plains
    shows **6h**.
- **Rivers and seas are barriers.** Only flyers and swimmers can cross them, except where a road
  crosses the river.
- **Map size varies by scenario:**
  - A small solo scenario ("Ironwood River", 2 player slots) has about 25 settlements, with
    one zombie outbreak in the north, the player in the south-east and neutrals in the west.
  - A large 6-player co-op map is **mirror-symmetric**: two halves split by a long
    north-south sea, each half with its own plains, forests, desert, swamp and
    mountains. It holds dozens of settlements and several outbreak points.
- **Region flavour follows race:** dwarf strongholds sit in mountains, elf villages in
  forests, human towns on plains, orc camps in desert, troll huts in swamp. This matters
  because a race's zombies are 50% stronger on that same terrain.

## 2. Settlements (map nodes)

Each settlement is drawn as a **round plate** of buildings with a label underneath:

```
        [ unit token, if any ]
           (buildings icon)
      (G) 400   [blue shield]      <- gold income per day, owner shield
           Hydrasedge              <- name
          200 Dwarves              <- population + race
```

- **The building art shows race and size:** stone towers for dwarven castles, wooden huts for
  villages, round tents for orc camps, larger walled clusters for towns.
- **The gold badge** shows the settlement's daily Gold, which is population × the race rate.
  Screenshot examples:
  - 200 Dwarves → **400** (2 per villager)
  - 50 Elves → **50** (1)
  - 200 Humans → **100** (0.5)
  - 150 Trolls → **150** (1)
- **A blue shield badge** next to a settlement means a player owns it. Neutral settlements
  have no shield. Neutral ones still show their gold value as a preview of what they'd pay.
- **Settlement states:**
  1. **Neutral:** clean plate, no shield.
  2. **Owned:** blue shield. Gold flows in, and it can train units and deploy heroes.
  3. **Under attack:** a crossed-swords combat marker sits on it until the battle resolves
     (see [Combat markers](#4b-combat-markers)).
  4. **Blighted:** the ground around it turns into **dark brown-black splatter**,
     a **skull and crossbones** appears under it (the graveyard of infected bodies), and
     the buildings may be shown **on fire**. A blighted settlement is no longer a zombie
     target, so the horde moves on to the next nearest one.
  5. **Reclaimed:** living troops retake the hex and **burn the corpses**. The skull
     disappears, but the blight scar stays on the ground.
- **Monster lairs** are neutral places with non-standard races, such as
  **Lost Nest (20 Gryphons)**, **Shreps Pool (6 Hydra)** and **Falcons Mire (3–5 Ents)**.
  They work like settlements but supply special creatures.

## 3. Mana Pools

- Drawn as a **glowing blue pool** in a stone ring, with a green Mana badge reading
  **20**, its daily Mana output.
- They have names like Valiantpool, Red Mud and Wolfspond, and there are usually several
  spread around the map.
- Zombies treat them as targets just like settlements. A blighted pool spawns a **boss**.

## 4. Units on the map (tokens)

- Every army or unit is a **portrait token** standing above the hex it occupies, with a
  number in a pill below it.
  - **The number is total Might** (population × strength), not head-count.
    For example, the token "1269" is *47 Undead Dwarves at 27 Strength each*.
- **Colour tells you the side:**
  - **Blue frame and blue pill:** your units.
  - **Dark or red pill with a grimy portrait:** zombies.
- **Badges on a token:**
  - A small **blue shield** marks a token as yours.
  - A small number in a circle on the left shows how many followers are grouped under it.
- **A zombie group with a skull marker** under it is sitting on a graveyard it is creating.
- **Stacks:** several tokens can sit on one node. The game lists them in the unit panel.
- **A selected unit** gets a white outline around its token. A **selection bar** at the top
  shows the owner shield, portrait, name and total strength, for example
  `[shield][portrait] 50 Human Swordsmen ... 500 Strength`.
- **Movement orders** show as a **pale yellow line** along the waypoint edges to the
  destination. The destination waypoint is marked with a **black dot**, and a blue
  **ETA pill** next to the path gives the travel time (for example "6h").

## 4b. Combat markers

From `reference/screenshots/tutorial-7-combat-markers.png`:

- When enemy stacks meet, their separate tokens are **replaced by one combat token** on that
  waypoint. It has a **grey frame with a crossed-swords icon** instead of a portrait.
- Battles happen wherever the stacks meet, **often on empty waypoints in open country**,
  not only at settlements.
- A blue owner shield on top shows that one of your armies is in the fight.
- **The number under the swords is the combined Might of everything in the battle**:
  - **1940** = a 1440 Undead Dwarf horde + a 500 Swordsman army.
  - *(inferred)* **1022** is probably 500 Swordsmen + about 522 of a weakened zombie stack.
- The token stays until the battle resolves, **1 hour after contact**. More units moving
  onto that waypoint during that hour join the battle.
- Also visible in the same screenshot:
  - **Rangersplain's income has dropped from 100 to 75.** It trained 50 Swordsmen, leaving
    150 villagers × 0.5 Gold.
  - **A freshly deployed hero** (portrait token, Might **100**) stands on Rangersplain. That's a
    single 1 × 100 hero, the same as the Wizard card.
  - **Untouched armies of 500** wait on nearby waypoints as reserves.

## 5. The outbreak and how the blight spreads

The screenshots of the solo game form a time-lapse:

| Game age | What the map shows |
|----------|--------------------|
| **1d 18h** | Zombies (red tokens of a few hundred Might) hold a few northern villages. The player's blue troops cluster in the south-east. Neutral elves and dwarves sit untouched in the west. |
| **3d 4h** | The horde has grown (tokens of 1,000 to 2,500+) and pushed south-west into the dwarven mountains. A brown blight scar spreads across the central plain. The player's towns form a defensive line. |
| **5d 22h** | The north-east has been retaken and the graves there burned. Fighting is now in the **western mountains** (dwarves) and the **central forest** (Ents). |
| **6d 10h** | Dwarven Hammers retake a mountain city and burn its corpses. |
| **7d 16h** | Victory. Most zombies are dead and one south-western city is still burning. |

How the spread works:
1. Zombie stacks walk toward the nearest unblighted settlement or pool.
2. When they win a fight, every killed defender or villager becomes an infected body in a
   **graveyard** at that node.
3. After a delay, those bodies rise and **add new zombies** to the map. This is why
   the Might numbers on zombie tokens grow as the game goes on.
4. Burning the graveyard means walking any living unit through it or winning a battle there.
   This removes the bodies before they rise.

From the article: because a town's population is both its **income** and future **zombie
fodder**, it's sometimes best to **empty a village**, by recruiting or evacuating everyone,
before an unstoppable horde reaches it.

## 6. Interface layout

```
+-----------------------------------------------------------------+
| [inbox]  Age: 5d 22h   (G) 209 Gold (M) 21 Mana (V) 68 Valour [menu] |
|              < Jump 6 Hours >   cost: 0 Valour                  |
|                                                                 |
|                      (hex map, pan and zoom)                    |
|                                                                 |
|   [popup panels: Combat Detail, card view, target select...]    |
|                                                                 |
|          [hand: 5 hero card portraits] [deck: N] [bazaar]       |
+-----------------------------------------------------------------+
```

- **The top bar** shows the game clock as **Age** in days and hours (`Age: 3d 4h`), plus the three
  resource counters. In solo mode the **Jump** control sits under it. Its arrows change
  the jump length, and a Valour cost or reward line shows underneath.
- **The bottom bar** holds the hand (small portraits of the cards you hold), a counter for
  cards left in the deck, and buttons for the deck and the Bazaar/Tavern.
- **Popup panels** open over the map:
  - **Combat Detail:** location, time, the two sides' Might (`1666 VS 2405`), the
    casualty formula in words, a per-unit table (Might, souls before, souls after) and the
    Valour each player earned.
  - **Battle preview:** opens when you inspect a pending fight. It lists every stack and its
    Might, then the predicted outcome, for example *"Living win and each soldier has a 3% chance of dying."*
  - **Target selection:** for powers such as *Valour Strike*. Valid targets get
    **red-and-white bullseye rings** on the map, and the panel lists each target's name,
    head-count and Might.
  - **Card view:** the full card art and rules (see below).
  - **Mission Complete:** the scenario name, difficulty, souls saved, score % and a
    **star rating** (47% gave 2.5 of 5 stars).
- **Before a game starts,** a red banner warns you if no deck has been chosen, and a social
  share box offers open player slots.
- **The top-left corner** shows the player's round avatar badge. A small **"S" coin** next to
  the Valour counter opens the Shadow Bazaar.
- **Settlement panel** (click an owned village):
  ```
  Human Village                                  [?] [x]
  [village art]          100 Gold in: 7h 9m 44s
                         [ Relinquish Command ]
  Population        200 Human Villagers
  Production        0.5 Gold / Villager Every 24 hours
  Production ETA    100 Gold in 7h 9m 44s
  ---------------------------------------------------
  [unit portrait 500]  Train 50 of the 200 Human Villagers to become
                       Human Swordsmen @ 10 Strength each.
                       [ Train for (G) 250 Gold ]
  ```
- **Settlement panel, neutral** (a unit of yours is standing in it):
  ```
  Human Village                                  [?] [x]
  [village art]   Move a unit into this settlement and take
                  command! Train its villagers and collect its Gold.
                         [ Claim for (V) 2 Valour ]
  Population        200 Human Villagers
  Production        0.5 Gold / Villager Every 24 hours
  Production ETA    100 Gold in 13h 59m 13s
  ---------------------------------------------------
  [unit 500]  Claim this settlement so you can train 50 Human
              Villagers to become Human Swordsmen @ 10 Strength each.
              [ Train for (G) 250 Gold ]   (locked until claimed)
  v Heroes & Armies
  [shield][portrait] 50 Human Swordsmen          500 Strength
  ```
  Neutral and owned panels look the same. The neutral one swaps *Relinquish Command* for
  *Claim for X Valour* and adds a **Heroes & Armies** list of the units present.
- **Claim reward panel** (opens right after claiming):
  ```
  Human Village                                       [x]
  [village art]   The people of Druid Farm offer you this
                  reward for taking their settlement under
                  your protection.
  Reward
  [art: leather pouch of coins]   A pouch of Gold!
                                  (G) +150 Gold
                                  [ Show Settlement ]
  ```
- **Army panel** (click a unit):
  ```
  50 Human Swordsmen                             [?] [x]
  [unit card, cost 250]   Not Moving
                          [ Move ]
  Followers: use ▲ to gather all nearby units into one army, ▼ to disband it
  > Other Heroes & Armies:  None
  ```
- **Stack list popup** (`reference/screenshots/stack-selection-list.webp`): clicking a
  stack token opens a dark list at the top of the screen with one row per unit:
  `[owner shield][portrait] 25 Elven Archers   ⚡   350 Strength`.
  The selected row is outlined. A ⚡ marks units with an ability. The map token shows
  the sum of all rows (1650).
- Other things in the same screenshot:
  - **A blighted settlement** (Forgotten Valley) has a dark splatter ring, no gold badge and no
    population label. A zombie token (288) stands next to it.
  - **A skull marker** under a waypoint or token marks a **graveyard** there, with bodies still to burn.
  - **A battle in progress**: a crossed-swords token (560) stands next to a player army with a
    small **"2" badge**, meaning 2 units are grouped in that army.
  - **Mixed tokens on one settlement**: Swans Forest (50 Elves) shows a zombie token (16)
    and a player token (300) side by side. That's the contact hour before a battle token
    replaces them *(inferred)*.
- Selecting a unit shows its **total strength** and a list of the **individual units** in it.
  From that view, units of the **same type** can be **merged** into one, and a unit can
  be **split** into smaller ones. *(Described by the user; no screenshot yet.)*
- **Tutorial pop-ups** are black boxes with a pointer arrow aimed at the UI element they
  explain, plus **Back** and **Next** buttons. They walk you through the objective, the zombie horde,
  training, moving, combat and the 6-hour jump. Screenshots are in
  [reference/screenshots/](reference/screenshots/).

## 6b. Typical single-player opening (tutorial map)

- The player starts in the south: **6 Human villages** (200 Humans, 100 Gold/day each) in a
  plains region by the sea, plus **1 Mana Pool** (Yellowsprings) on the coast. All are already owned.
  One village already has a 500-Strength Swordsman army.
- To the north is a **mountain and forest** region with three **dwarven fortresses** (Shallow
  Mountain, Ironhelm Fortress, Rams Pass). All three are **already blighted**: dark splatter on the
  ground and no population label. **Undead Dwarf** stacks of 720 and 1440 Might are spreading
  out from there.
- The player's first decisions: train armies everywhere, gather them, and march north to
  intercept the zombies before they reach the villages.

## 6c. More UI from the intro video

Frames in [reference/video-intro/](reference/video-intro/):

- **Hero power toolbar:** a vertical strip of square **power buttons** sits on the right edge of
  the map, one per available power (icons such as a staff, a sun or a flame). Click one, then pick an
  area or a target.
- **Target selection:** the top panel reads *"Select a target for Shall Not Pass"* and lists the
  valid targets (`5 Immortal Elves ... 70 Strength`) with a Cancel button. The target on the map
  gets a **red-and-white bullseye**.
- **Path builder:** the top panel reads *"Build a list of locations for your hero to move to"*
  with **Clear Path / Save / Cancel**. You click waypoints to add them to the path.
- **Time-jump control:** `< Jump 6 Hours >`. The arrows step the jump down to 2h or 1h, and the
  Valour cost shows underneath (0, −4 or −5).
- **Deck builder** ("Assemble Your Heroes!"): two columns. *Your Deck* on the left has the card count, the
  Deck Essentials row and up to 12 extra slots. *Your Collection* on the right has a grid of portraits
  with ×counts and a race dropdown. *Start Game* is at the bottom right.
- **Settlement panel extras:** a *Fortifications +2 Strength* row for big settlements, a
  *Show Reward* button after claiming, and the train button turning into *"Training for 6h"*.
- **Graveyard info:** clicking a blighted settlement lists its status (*Blighted*) and its
  graveyard (*158 Human Bodies*), shown with a skull icon.
- **Battlefield Graveyard panel** (`reference/screenshots/battlefield-graveyard-panel.png`):
  ```
  Battlefield Graveyard                         [?] [x]
  [art: moonlit battlefield, broken banners, spears, crows]
    Here lie the bodies of those slain by the Undead.
    Restless souls compelled to rise again.
    Move your forces to this location and burn these bodies
    so that they may rest in peace evermore.
  Restless Souls
    Human ............................................ 158
  ```
  Each race of body gets its own row.
- **Mid-game look:** whole regions turn into dark blight splatter. Almost every zombie
  token has a skull (graveyard) under it. Burning towns show **big orange flames**, and the
  few owned settlements still show blue shields.

## 7. Cards

Every hero or unit card has the same layout:

```
+---------------------------------+
| Name                  (G) cost  |
|  +---------------------------+  |
|  |        artwork            |  |
|  |                 [ HERO  ] |  |  <- HERO or unit count
|  |                 [ 100   ] |  |  <- total Might
|  |                 [1 x 100] |  |  <- individuals x strength
|  | Mortal Human Mage (Plain) |  |  <- alignment, race, class, home terrain
|  +---------------------------+  |
|          Ability Name           |
|   rules text (range, effect,    |
|   duration, recharge, Mana)     |
| 4 Hours / League by Road  Rarity|
+---------------------------------+
```

- Card frames are **brown/orange for mortal heroes** and **dark grey for immortal
  (zombie) bosses**. Living unit cards for sale appear with a **blue** frame.
- **Rarity:** Common, Uncommon, Rare. A rarer card can be shown with a coloured footer.
- **Speed** is printed as *hours per League by road*. Normal is 4h. A faster value, such as 2h,
  is highlighted in orange.
- Strength can be split as **base + bonus** (`1 x 300+400`) when a buff is active.

## 8. The Tavern / Bazaar screen

- A **"Select One Card"** popup shows the Tavern keeper and **3 cards** of the race you
  chose, each with a **Select** button. The one you pick goes into your hand **and** your
  permanent Collection.

## 9. Session flow (as described in the article)

1. **Before the game:** pick a scenario (free solo scenarios, a tutorial, paid Premium campaigns,
   or join a co-op game), then build a deck from your Collection.
2. **During the game:** expand, fight, burn graves and keep zombies away from Mana Pools. In solo play
   you advance the clock in jumps. In co-op the clock runs in slow real time over days.
3. **After the game:** you get a score (souls saved, as a % of the starting population) and
   **Hero points** based on it. You spend these in the Bazaar on new cards
   for future games. Co-op play with Premium earns Hero points faster.
4. **Difficulty levels** include **Hard** and **Nightmare** (the hardest). The reviewer found
   solo Hard harder than the co-op difficulty he'd played, and a 6-player Nightmare game
   much harder again.
