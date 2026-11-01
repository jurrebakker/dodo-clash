# Dodo Clash: Game Design (draft v0.2)

> *Mauritius, 1598. For a million years the dodo had no enemies. Then the ships came.*

Dodo Clash is a co-op browser strategy game for a small group of colleagues. Together you
lead the birds of Mauritius against the animals that people brought to the island. One
match lasts **one office week** and is played in short breaks. Blight of the Immortals is
our reference for the overall **genre** (see [GAMERULES.md](GAMERULES.md)): a slow-paced
map strategy game where a threat spreads and you contain it. But Dodo Clash has its own
setting, its own way of spreading the threat, its own economy and its own numbers. See
[§13 What we deliberately do differently](#13-what-we-deliberately-do-differently).

---

## 1. Premise

- **Setting:** Mauritius around 1600, a volcanic island with no natural predators.
  Ships drop off sailors, dogs, pigs, cats, rats and macaques. Each one threatens
  the dodo in its own way.
- **The players** (2–6) each control a group of **dodos** and their allies among the
  island's native animals. They all play on the same side.
- **The enemy** is the **Invaders**: the introduced species, spreading out from where the ships land.
- **Goal:** survive the week. Push the invaders back, destroy their **dens** and keep as many
  dodos alive as possible.
- **Tone:** light and a bit funny on the surface (a clumsy bird fighting back),
  with a melancholy layer underneath, because in reality the dodo was extinct by about 1662.
  The game asks: *what if they had fought back?*

### Win, lose and score
- **Win (early):** every invader on the island is defeated **and** every den is destroyed,
  after the ship schedule has finished (or every remaining wave is blockaded, see §6.2).
- **End of the week:** if nobody has won by the deadline, the match ends anyway and is scored.
- **Lose:** every colony on the team has fallen and no new colony was won over during the
  **grace period** (see §7.4). The grade is then *Extinct*.
- **Team score:** the share of the starting dodo population that is still alive, counting
  dodos in colonies **and** in flocks. Grading: *Extinct → Endangered → Vulnerable → Thriving*.
- **Personal categories** (shown at the end, each with its own winner):

| Category | Measured as |
|---|---|
| 🐣 Most dodos saved | % of your own starting population still alive |
| 🔥 Most dens destroyed | dens your flocks destroyed |
| ⚔️ Most invaders defeated | invaders defeated, split by contributed strength |
| 🤝 Most help | strength contributed to battles at other players' colonies |

---

## 2. The island (map)

- Based on the real geography of Mauritius. The MVP uses the **whole island**.
- **Terrain** is drawn on **hexes**. **Movement** uses a separate **triangular waypoint grid**
  on top of the hexes, like the reference. One edge between two waypoints is one **stride**.
  Units move along edges and can stop on any waypoint, also in open country. Enemies can also
  meet **halfway along an edge**; the battle and its survivors then stand on that spot (§8).
- The **move cost of an edge** comes from the terrain of the hex that the **edge's midpoint**
  lies in. Footpaths are an attribute of an edge, not of a hex.
- **Terrain:**

| Terrain | Real-world inspiration | Move cost |
|---|---|---|
| Coast & beach | lagoons, sandy beaches | 1x |
| Grassland | central plateau | 1.5x |
| Ebony forest | the original rainforest | 1.5x |
| Marsh | Mare aux Songes (where the most dodo bones have been found) | 2x |
| Mountains | Le Pouce, Black River Gorges | 2x |
| Footpath (edge) | trampled animal trails | 0.75x (faster) |
| Water | lagoon, reef, rivers | impassable (except for flyers) |

- **Map locations** (each sits on one waypoint):
  - **Colonies:** dodo nesting grounds. They produce food and can train new flocks.
  - **Starting positions:** the map has **6**. Four lie on the home terrains of the four
    clans, two in mixed terrain. A position nobody takes becomes a **wild colony** (§7.2).
  - **Ally settlements:** homes of other native species (see §4).
  - **Freshwater springs:** produce **Spirit** (see §5). If invaders take one,
    a **Plague** event starts (see §9). *Not in the MVP.*
  - **Harbours:** where ships land. New invaders come ashore here.
    Harbours can't be captured, only **blockaded**.
  - **Dens:** places where invaders breed (see §6).
  - **Ruins:** colonies that have fallen. They stay ruins for good.
- **Map file:** terrain as an ASCII grid (one letter per hex) plus a JSON list of locations.
  The waypoint grid is **generated** from it: a regular triangular lattice over the map, with
  edges over water removed. Locations snap to the nearest waypoint.

---

## 3. Time

- **One shared clock** per match, running continuously. No turns and no End Turn button.
- The clock only runs during the match's **active hours**. Whoever creates the match sets them:
  active weekdays, active hours and a timezone. Default: **Mon–Fri, 09:00–17:30, Europe/Amsterdam**.
  Outside those hours nothing moves, breeds or fights. Nobody needs to get up at night to save a colony.
- Players can still look at the map and **give orders while the clock is paused**.
- The match creator has a **pause button** (holidays, a team day out).
- **Length:** a match lasts **5 active workdays**, about **10 island days**. That makes
  1 island hour ≈ 10 real minutes. The speed is the same in every match: starting on a
  Wednesday means ending on the next Wednesday (or earlier if you win).
- **No ticks:** time is continuous, counted in **island minutes** (1 island minute = 10 real seconds).
  **Orders take effect immediately**: a flock leaves the moment you send it. Movement, contact and
  battles happen at the exact minute they occur. Dens breed on every island hour, and Fruit and
  eggs arrive once per island day. See [ARCHITECTURE.md §2](ARCHITECTURE.md#2-time-model-continuous-no-ticks).
- The "jump less time and pay for it" mechanic from the reference is **dropped**.
- **Practice mode:** the same rules, on the server, as a one-player match with an accelerated
  clock, "skip 1 day" and reset. It's a developer and balancing tool first, and later the tutorial.

---

## 4. The dodos and their allies (variety)

Each player's group is a **flock**. Flocks come in several **kinds**. Each kind has a home
terrain, a speed, a strength and one special ability. Instead of races with their own
villages (as in the reference), we have **dodo clans** plus **native allies**.

- A flock **is made of real dodos**: training takes adults out of a colony, and the dodos in
  a flock count toward the score. Dodos lost in battle are gone. Disbanding a flock into one
  of your own colonies returns its dodos.

### 4.1 Dodo clans (each player picks one in the lobby)

| Clan | Home terrain | Speciality | Unit |
|---|---|---|---|
| **Forest Dodos** | Ebony forest | Balanced, the core troops | *Peck Flock* |
| **Marsh Dodos** | Marsh | Hard to dislodge, strong defence | *Mud Guard* |
| **Highland Dodos** | Mountains | Slow but very tough | *Rock Beaks* |
| **Shore Dodos** | Coast | Fast, good at blockading harbours | *Tide Runners* |

- A clan gets **+25% strength on its home terrain**. In the reference it's the enemy that gets this bonus.
- With more than 4 players, two players can pick the same clan.
- In the MVP the clans only differ in home terrain and one stat. Abilities come later.

### 4.2 Native allies (join when you win over their settlement)

All of these species really lived on Mauritius or a neighbouring island, and many
are extinct now too. That makes them natural allies.

| Ally | Type | Ability (idea) |
|---|---|---|
| **Giant tortoise** (*Cylindraspis*) | Very slow, very strong | *Shell Wall:* blocks a path for 1 day |
| **Red rail** (*Aphanapteryx*) | Fast and light | *Scout:* reveals invaders within 3 strides |
| **Broad-billed parrot** (*Lophopsittacus*) | Flyer | *Alarm Call:* nearby flocks get +1 move |
| **Mauritius blue pigeon** | Flyer | *Messenger:* moves Food or Spirit to another colony |
| **Fruit bat** (flying fox) | Flyer, active at night | *Night Raid:* attacks from a distance without being harmed |
| **Rodrigues solitaire** | Rare cousin, an elite unit | *Rally:* all flocks in the area gain courage (+strength) |

- **No cards and no deck.** A player wins over a settlement by having **a flock there and
  paying Courage** (see §5). The settlement then belongs to that player, and only they can
  train its ally there.
- Allies don't count toward the score.
- **No playable hero characters** on the map.

### 4.3 Match hero (chosen before the match)

- Before a match the player picks **one hero**. The hero never appears on the map. Instead
  it gives a **static modifier that lasts the whole match**.
- **The first hero has no modifiers at all.** It's the neutral baseline, and the only hero in the MVP.
- Later heroes come with **trade-offs**: a bonus in one area, paid for with a penalty
  somewhere else. Ideas for later (not final):

| Hero (idea) | Bonus | Trade-off |
|---|---|---|
| *The Elder* (baseline) | none | none |
| *The Forager* | +20% Fruit | Flocks train slower |
| *The Warden* | +25% colony defence | −1 move speed for all flocks |
| *The Brood Mother* | Eggs hatch 50% faster | −10% flock strength |
| *The Wanderer* | +1 move speed | −20% Fruit |

---

## 5. Resources

All resources belong to **one player**. There is no trading or gifting between players in the MVP.

| Resource | Comes from | Used for |
|---|---|---|
| **Fruit** 🍈 | Your colonies (per dodo per day) and fruit trees on the map | Training flocks |
| **Spirit** 💧 | Freshwater springs | Ally abilities (*not in the MVP*) |
| **Courage** 🪶 | Defeating invaders with your flocks | Winning over settlements, springs and wild colonies |

- Fruit is **seasonal**. In the dry season colonies produce less. That gives the game a rhythm.
  *Not in the MVP.*
- **Eggs:** each colony has an egg count that slowly turns into new dodos.
  Training a flock takes adults away from the colony, so it produces less Fruit.
  Same trade-off as the reference, but here the colony **grows back**.

---

## 6. The invaders and how they spread

### 6.1 Species

| Invader | Historical role | Home terrain | Character |
|---|---|---|---|
| **Sailors** | Hunted dodos for food | Coast | Strong, slow, rarely leave the coast |
| **Dogs** | Brought on ships, hunt in packs | Grassland | Fast, mid-strength |
| **Pigs** | Rooted up nests and ate eggs | Forest, marsh | Tough, go **straight for eggs** |
| **Cats** | Hunted chicks | Everywhere | Weak, but sneaky (hidden until close by) |
| **Rats** | Ate eggs, multiply explosively | Everywhere | Very weak, very many |
| **Macaques** | Plundered nests | Forest, mountains | Smart: avoid fights they would lose |

- Invaders get **+50% strength on their home terrain**. Lure them out onto the wrong ground.
- MVP: Sailors, Pigs and Rats.

### 6.2 Spreading through dens (our main mechanic)

This replaces the reference's "bodies rise up as zombies".

1. An invader that **plunders** a colony eats eggs and dodos.
2. Each kind of invader builds a **den** nearby (a pig wallow, a rat nest, a dog lair).
3. A den **breeds new invaders** every island hour. The more it has eaten, the faster it breeds.
4. **Destroying a den:** move a flock onto it, or win a battle there.
   A den you leave alone keeps growing until it becomes a **nest of the plague**.
5. **Ships** follow a **fixed, finite schedule** per scenario (day, harbour, species, count),
   in the historical order of arrival. A wave that arrives at a **blockaded** harbour (your
   flocks stand on it) is **turned away and lost for good**. The schedule ends before the
   last day of the match.

### 6.3 Invader movement
- Invaders go for the **nearest colony with eggs**. Pigs and rats prefer the
  colony with the **most eggs**. Dogs prefer the **nearest flock** they can beat.
  Macaques **avoid** fights they would lose. Each species has its own behaviour,
  instead of one rule for all of them.
- Invaders don't care whose colony it is. Wild colonies are targets too.

### 6.4 Scaling with the number of players
- **Ship wave size** and **den breeding speed** scale linearly with the number of players at
  the start (base = 4 players). The map stays the same.
- The match creator picks a difficulty (*Easy / Normal / Hard*), which is one extra multiplier.

---

## 7. Colonies, players and the team

### 7.1 Falling colonies
- A colony **falls** when its **last adult dodo is gone**: killed, or all of them sent out in
  flocks. The UI warns before you train away the last adults.
- Its eggs are lost, it becomes a **ruin for good**, and the invader that plundered it
  builds a den nearby. A ruin can't be resettled.
- A colony always **defends itself** with its own adult dodos. Defending its own colony, a
  dodo counts for 1.5x (see §8).

### 7.2 Wild colonies
- A starting position nobody took becomes a **wild colony**. Its dodos don't count toward the
  score yet.
- Any player wins it over with **a flock there and Courage**, just like an ally settlement.
  From then on it's that player's colony and counts toward the score.
- Invaders attack wild colonies too, so they are an emergency exit that shrinks over time.

### 7.3 A player without colonies
- Keeps playing with their flocks: defending, burning dens, helping out. No deadline.
- Has no Fruit income, so can't train new flocks.
- Can win over a wild colony to get back into the game, and can be handed command by teammates.

### 7.4 The team without colonies (grace period)
- When **every colony on the team** has fallen, a **grace period of 1 island day** (~2.5 real hours) starts.
- If a player wins over a wild colony during it, the grace period ends and the match carries on.
- If it runs out, the match is lost (*Extinct*). If no wild colonies are left, it's lost immediately.
- Clearing every invader and den during the grace period still counts as a **win**. The score
  is then the dodos left in the flocks.

### 7.5 Absent players
- A player can **hand over command** of their flocks to a teammate, and take it back at any time.
- **Joining late** is possible until the end of island day 1. Starting positions still unclaimed
  then become wild colonies.

---

## 8. Combat

- Combat starts at **contact**: when flocks and invaders meet at a waypoint or location, cross
  each other on an edge, overtake each other, or one walks onto an edge where the other stands.
  Both sides are **pinned** on that spot, and the battle is resolved **1 island hour after contact**.
  Anyone who reaches the spot during that hour joins it as reinforcement. A pinned flock can be
  given a new order, but it only starts moving after the battle. Technical details in
  [ARCHITECTURE.md §2.1](ARCHITECTURE.md#21-positions-contact-and-battles).
- **All dodo flocks in a battle fight as one side**, whichever players they belong to.
- **Strength = number × individual strength** (plus terrain, hero modifier and nest defence).
- **Outcome:** the stronger side wins. Losses follow a **saving throw** based on how the
  two sides' strengths compare.
  - We start from the square law (Lanchester's law, a general military rule of thumb):
    `chance each winner dies = (loser / winner)²`.
  - **Our own twist:** dodos that are **defending their own colony** count for 1.5x.
    Invaders that have to **flee** (losing badly with a ratio below 1:3) are not destroyed. They retreat to their den, so they don't die
    the way the reference's losers do. This makes chasing them and destroying the den important.
- **Several players:** losses are spread over the flocks **in proportion to strength**. Courage
  and the ⚔️ / 🤝 categories are split the same way.
- **Experience:** every flock on the winning side gets **+1 strength** per individual, up to +5.
- **Randomness is deterministic:** the game logic uses its own seeded random generator stored
  in the game state. The same state plus the same orders always gives the same result.

---

## 9. Plague events (instead of zombie bosses) — *not in the MVP*

When invaders capture a freshwater spring, a **Plague** starts somewhere on the island.
This is a special invader with an effect on the whole map:

| Plague | Effect (idea) |
|---|---|
| **The Captain** | All sailors move faster for 2 days |
| **The Sow Queen** | Every pig den breeds twice as fast |
| **The Rat King** | Spawns rat swarms at every den |
| **The Hound Master** | Dogs track down hidden flocks |

---

## 10. Interface (basics)

- **Desktop browser** first: mouse, wheel zoom and a few keyboard shortcuts. No phone support
  yet, but nothing essential relies on hover, so touch can be added later.
- A top bar with the island day and hour, the clock state (running / paused until …),
  Fruit and Courage.
- The map uses tokens with portraits. The number on a token is total strength.
  Dodo tokens have green frames (with a player colour) and invader tokens red ones.
- **Orders:** click a flock, pick a destination, and the route is planned automatically
  (adjustable with extra waypoints). Orders take effect immediately and can be changed at any
  moment, except that a flock pinned in a battle only moves after the battle (§8). A flock
  halfway along an edge can turn around, but you can't order it to stop mid-edge.
  Merging and splitting only happen on a waypoint.
- Panels: a **colony panel** (population, eggs, Fruit, train), a **flock panel**
  (move, merge, split, ability), a **den panel** (species, breeding speed), a **battle report**.
- **Inbox:** battle reports and warnings ("colony under attack"). It's the only notification
  channel; no chat webhooks or push notifications.
- **Lobby:** pick a starting position and a clan, see who has joined.
- **Match end screen:** team grade plus the personal categories.
- **No fog of war** in the MVP. The game state keeps a spot for visibility, so cats and
  scouting can be added later.
- A shared visual language (move lines, travel-time labels, battle markers) may
  follow the conventions of the genre. Artwork, names and text are ours.
- **Art:** cute and hand-drawn in the end. Until the game is fun we use **placeholders**
  (coloured hexes, circles with a letter or emoji, plain HTML panels).

### 10.1 Art specs

Placeholders and final art follow the same sizes and file names, so they can be swapped
without code changes.

- **Hexes are flat-top.** At 100% zoom a hex is **128 px wide** (111 px tall).
  The map zooms from **25%** (whole island on a laptop screen) to **200%**.
- **Everything is drawn at 2×** and scaled down by PixiJS (with mipmapping). No separate 1× set.

| Asset | Source size (2×) | On screen at 100% |
|---|---|---|
| Hex terrain tile | 256 × 222 px | 128 × 111 px |
| Token portrait (flock, ally, invader) | 128 × 128 px | 64 × 64 px (½ hex) |
| Location icon (colony, den, harbour…) | 128 × 128 px | 64 × 64 px |
| Map marker (battle, flee) | 64 × 64 px | 32 × 32 px |
| UI icon in HTML panels | SVG, 24 px grid | 24 px |

- **Tokens** are round with a coloured frame: green plus a player-colour ring for dodos,
  red for invaders. The strength number sits in a badge underneath. Several tokens on one
  waypoint fan out slightly.
- **Packaging:** PNG sprites in three texture atlases: `terrain` (tiles, edge overlays such as
  footpaths, location icons), `units` (token portraits, frames, badges, markers) and `ui`.
  Icons in the HTML panels are SVG.
- **File names:** `assets/<atlas>/<kind>-<name>.png`, for example `terrain/terrain-marsh.png`,
  `terrain/loc-colony.png`, `units/unit-dodo-forest.png`, `units/unit-pig.png`,
  `units/marker-battle.png`, `ui/icon-fruit.svg`.

---

## 11. Matches and the server

- **Creating a match:** pick the map, the start time, the active hours and the difficulty.
  Share the **invite link**. Players join the lobby. At the start time the clock starts.
  Default start: Monday 09:00.
- The server can run **several matches** at the same time.
- **Login:** no accounts. You open the invite link, pick a name, and the server sets a cookie in
  your browser. Company SSO comes later.
- **Rule values are frozen per match:** the `data/` numbers and the map are copied into the match
  when it is created. Rule and balance changes only reach new matches.
- **Bug fixes** may be deployed during the week. The stored state has a **schema version** and
  migrations.
- **Rollback:** because the game is deterministic and the server stores an hourly snapshot plus
  a log of every command (order), the server admin can roll a match back to an earlier moment
  through the admin endpoints. The match creator only has pause.
- How the server, storage and client work: [ARCHITECTURE.md §4](ARCHITECTURE.md#4-server).

---

## 12. Plan

### 12.1 First version to play with colleagues (MVP)
1. The **whole island** of Mauritius, 6 starting positions, 2 harbours, a ship schedule.
2. **4 clans** that only differ in home terrain and one stat. **1 ally** (Giant tortoise).
3. **3 invaders** (Sailors, Pigs, Rats) with dens.
4. **Fruit, eggs and Courage.** No Spirit, springs, Plagues, abilities or seasons. Only the baseline hero.
5. Combat with the square law and fleeing, battle reports, inbox, team grade and personal categories.
6. Multiplayer server with lobby, invite links and the office-hours clock. Practice mode.

### 12.2 Milestones (each one playable)
1. **Core + practice mode:** a small test map, generated waypoint grid, one flock, moving,
   the clock running. A minimal server with one in-memory practice match, and a browser that draws it.
2. **Battles and invaders:** dens, ships, invader behaviour, the square law, fleeing,
   colonies falling. A full solo match in practice mode on a small map.
3. **Economy:** Fruit, eggs, training, Courage, the tortoise, wild colonies.
   Then deploy the Docker image with practice mode and collect feedback from colleagues.
4. **The real Mauritius map** + 4 clans + balancing with **headless simulations**
   (a whole week in seconds, with simple bot players).
5. **Real matches:** Postgres, snapshots and command log, invite links, lobby, inbox, admin.
6. **First test week with colleagues**, then the leaderboard and polish.

Multiplayer only arrives in milestone 5, but the server runs the game from day 1 and the
game logic is designed for it: several players, a continuous clock and determinism.
The technical side of each milestone is in [ARCHITECTURE.md §8](ARCHITECTURE.md#8-milestones-technical-view).

### 12.3 Decided
- **Purpose:** a hobby game to play with colleagues (all software developers) during breaks.
  One match per week.
- **Mode:** **co-op** with personal leaderboard categories. 2–6 players.
- **Time:** a continuous clock that only runs during each match's active hours. No ticks:
  orders take effect immediately, and units can meet mid-edge.
- **Art style:** **cute and hand-drawn**, placeholders first.
- **Heroes:** **no playable hero characters.** One match hero gives a static modifier.
  The first hero has none, and later heroes have trade-offs (§4.3).
- **Technology:** an authoritative **.NET 10** server that holds all game logic, and a thin
  **TypeScript** client (Vite + React 19 panels + PixiJS map) without any rules. HTTP for
  commands, server-sent events for updates. **Postgres** stores a command log and hourly
  snapshots. One **Docker** image serves client and server. Details in
  [ARCHITECTURE.md](ARCHITECTURE.md), background in [TECH_RESEARCH.md](TECH_RESEARCH.md).
- **Language:** **English only.** No translation system.
- **History:** **inspired by history.** The real island, the real species and the real order in which
  the invaders arrived (Dutch sailors in 1598, then pigs, rats, macaques…) form the backbone of the
  campaign. The story itself is freely fictional: *what if the dodos had fought back?*
  Short real facts can be unlocked as trivia.

### 12.4 Later
- Who makes the final art.
- Spirit, springs, Plagues and abilities. Seasons. More heroes. More invader species and fog of war.
- Company SSO. Phone and touch support. A map editor.

---

## 13. What we deliberately do differently

To make sure Dodo Clash is its own game rather than a copy:

| Reference (Blight) | Dodo Clash |
|---|---|
| Fantasy races, zombies | Real native and introduced species, Mauritius 1600 |
| Hero cards, deck, Tavern, Hero Coins | **No cards.** Allies come from the map. One match hero gives a static modifier |
| Gold / Mana / Valour | Fruit / Spirit / Courage |
| Bodies rise as zombies | Invaders **breed in dens**. Ships bring a fixed schedule of waves |
| Mana Pool → zombie boss | Spring → **Plague** event |
| All zombies use the same targeting rule | **Each species behaves differently** |
| Loser is always wiped out | Invaders can **flee** to their den. Defending colonies get a bonus |
| Population only shrinks | **Eggs**: colonies grow back |
| Clock runs day and night; players set alarms | Clock runs **only during office hours** |
| Valour pays for shorter time jumps | No time jumps |
| Zombies stronger on home terrain | **Both sides** have home terrain |
| Score = % alive | Team grade *Extinct → Thriving*, plus personal categories |

All names, text, images and numbers in Dodo Clash are made by us. We don't copy any
assets, text or card content from the reference.
