# Game Rules Reference: Blight of the Immortals

Rules and mechanics taken from the official help codex at
<https://blight.ironhelmet.com/help/index> and the help pages it links to.
Use this as a design reference. Where the source gives no value, the rule
says **Not specified**, and that number is ours to design.

---

## 1. Overview

- Each game starts with a zombie outbreak in a distant village or city. The zombies
  multiply and spread across the map.
- The game is **cooperative**. All players win together once the Blight is defeated.
- Players deploy **heroes**, expand their **empire** by taking settlements, and
  **train armies** to fight the zombies.
- **End condition:** the game ends only when both of these are true:
  1. Every zombie (walking dead) has been killed.
  2. Every infected body (restless soul) in the graveyards has been burned.
- **Score:** see [Reaper's Tally](#12-reapers-tally-scoring).

### Terminology
- Zombies are also called **Immortals**, **Undead** or **Blighted**.
- An ability that targets Immortals hits every zombie type unless it says otherwise.
- An ability that targets Mortals hits any living creature unless it says otherwise.

---

## 2. Races

There are six races. Each has a living version, which players control, and a zombie version.

| Race    | Gold per villager / 24h | Trainable unit   | Zombie version  | Zombie home terrain |
|---------|-------------------------|------------------|-----------------|---------------------|
| Humans  | 0.5                     | Human Swordsman  | Zombie Humans   | Plains              |
| Elves   | 1                       | Elven Archers    | Immortal Elves  | Forests             |
| Dwarves | 2                       | Dwarven Hammers  | Undead Dwarves  | Mountains           |
| Orcs    | 0.5                     | Orcish Swords    | Zombie Orcs     | Deserts             |
| Goblins | 2                       | Goblin Bows      | Undead Goblins  | Forests & Swamps    |
| Trolls  | 1                       | Trollish Spears  | Immortal Trolls | Swamps              |

Racial flavour mentioned in the source:
- Goblin and Dwarf heroes often produce extra **Gold**.
- Elf heroes often produce extra **Mana**.

---

## 3. Time

### Single player (turn-based)
- The player controls the clock and advances it several hours at a time.
- The **standard jump is 6 hours**.
- Jumping **further than 6 hours** earns **Valour**. The amount is not specified.
- Paying **Valour** allows **smaller jumps** for finer control. Observed costs
  (§18.8): **6h = free, 2h = 4 Valour, 1h = 5 Valour**. *(inferred)* cost = 6 − hours.

### Multiplayer (slow real-time)
- The clock always runs. A game lasts several days or weeks.
- Players log in whenever they like to check armies, read battle results and give orders.
  Players don't need to be online at the same time.

### Admin options (password-protected games, a Premium feature)
- **Jump ahead:** force game time forward. The amount is not specified.
- **Pause:** stops the production clock and unit movement.
- **Delete:** the creator can delete the game at any time.

### Standard durations
| Thing                                | Duration           |
|--------------------------------------|--------------------|
| Standard single-player time jump     | 6 hours            |
| Unit training time                   | 6 hours            |
| Hero deployment                      | Instant            |
| Cooldown between hero deployments at the same settlement | 6 hours |
| Delay from first contact to battle resolution | 1 hour    |
| Gold production cycle                | Per 24 hours (a "day") |

---

## 4. Resources

| Resource       | Starting amount  | Used for                                   | Sources |
|----------------|------------------|--------------------------------------------|---------|
| **Gold**       | 1,000            | Training units, deploying heroes           | Settlements (villagers), some heroes |
| **Mana**       | 20               | Casting hero special abilities             | Mana Pools (20 Mana per day each), some heroes |
| **Valour**     | 20               | Capturing settlements and Mana Pools, Shadow Bazaar, time control, flyer stance changes, gifting settlements | Killing zombies; in single player, jumping more than 6h |
| **Hero Coins** | Not specified    | Accepting Volunteer heroes, the Tavern     | Not specified |

- Gold, Mana and Valour can all be **sent to other players** (see [Diplomacy](#13-diplomacy--trade)).

---

## 5. Map & Movement

### Distance
- Distance is measured in **Leagues**. One League is the distance between two
  neighbouring **waypoints**, which are the points where dotted paths intersect.

### Speed and terrain
- A unit's base speed is the time it takes to cover **1 League on a road**.
- Terrain multiplies the time per League:

| Terrain                    | Time multiplier |
|----------------------------|-----------------|
| Road                       | 1x              |
| Plains, Forests, Deserts   | 1.5x            |
| Mountains, Swamps          | 2x              |

### Movement types
- **Flying units**
  - Ignore terrain penalties and can cross rivers, lakes and seas.
  - Have a stance:
    - **Avoid Zombies:** the unit won't engage zombies and won't burn bodies.
    - **Engage Zombies:** the unit engages zombies.
  - Switching stance costs **Valour**. The amount is not specified.
- **Swimming units**
  - Can cross rivers, lakes and seas.
  - Can't leave **Swamps**. They can't enter Plains, Forests, Deserts or Mountains.

### Giving orders
- Mouse: select a unit, then **right-click** a waypoint to move there.
  **Alt + right-click** adds more waypoints to the path. Right-clicking the unit's own position clears its orders.
- Touch: open the unit's details, press **Move**, tap waypoints, then press **Save** or double-tap the last waypoint.

---

## 6. Settlements

- Settlements come in three sizes: **Villages**, **Towns** and **Castles**.
- Each settlement belongs to a race and has a **population** of villagers.
- **Capturing:** move a unit into a neutral settlement and pay a **Valour** cost.
  The help pages give no exact values. Observed in-game: a **200-person Human village costs
  2 Valour** and a **150-person Elven Great Hall costs 3 Valour** (see §18.7–18.8). Until you claim it, the settlement panel already shows its
  production and training options, but you can't use them.
- **Claim reward:** the help pages don't mention this, but in-game the people of a newly
  claimed settlement give you a **reward** for taking them under your protection.
  Observed: *"A pouch of Gold! +150 Gold"* from a 200-person Human village. The reward
  table is otherwise unknown. It could also hold Mana, Valour, cards or volunteer heroes
  (compare *Volunteers* in §9).
- A settlement you command provides:
  - **Gold income:** each villager produces a race-dependent amount every 24h
    (see [Races](#2-races)).
  - A place to **deploy heroes** of the same race.
  - A place to **train units**.
- Recruiting villagers, whether by training units or deploying heroes, **lowers the population**.
  Recruited villagers no longer produce Gold. The map shows each settlement's daily Gold
  income and its population.
- **Fortifications:** some settlements give a defensive bonus to the troops inside.
  Larger cities and castles start with one. Some heroes and special units can raise a
  settlement's fortifications. Observed value: **Elven Great Hall: Fortifications +2 Strength**,
  i.e. +2 Strength for each defending soldier. Ordinary villages show no fortifications line.
- **Gifting:** a settlement can be given to another player through the Trade section.
  Gifting costs **Valour**. The amount is not specified.

---

## 7. Mana Pools

- Special map locations that produce **Mana**.
- **Claiming:** move onto the pool and pay a **Valour** cost. The amount is not specified.
- A claimed pool gives its owner **20 Mana per day**, paid out over the course of the day.
- If a zombie reaches **any** Mana Pool, claimed or not, it **blights** the pool and
  a **Zombie Boss** is created (see [Bosses](#11-zombie-bosses)).

---

## 8. Units, Heroes & Armies

### Unit card stats
Each hero or unit card shows:
- Name
- Gold cost to deploy
- **Strength**
- Special abilities
- Movement speed
- Mana cost to cast its ability
- Recharge time of its ability

### Training regular units
- Units can be trained in any settlement you control.
- Training costs **Gold** and uses up **population**.
- Training takes **6 hours**. Population is removed only when training finishes.
- A settlement with no population can't train.
- If a settlement doesn't have enough population for a full unit, it trains a smaller unit
  equal to its remaining population.
- Each race can train **only one unit type** (see [Races](#2-races)). Other unit types
  come only from deploying hero or special-unit cards.
- The help pages don't give exact Gold costs or unit sizes. The in-game tutorial shows one
  (see §18.7): a village trains **50 villagers** into **50 Human Swordsmen at 10 Strength
  each** (Might 500) for **250 Gold** (5 Gold per soldier). Training takes **6 hours = 1 turn**.

### Deploying heroes and special units
- They are played from your **hand** (see [Deck](#9-hero-collection-deck--hand)).
- The target settlement must:
  - be under your command,
  - be the **same race** as the card,
  - have enough **population**.
- You pay the card's **Gold cost**, and the settlement loses population.
- Deployment is **instant**.
- After deploying a hero at a settlement, you must wait **6 hours** before deploying
  another hero there.

### Grouping (armies)
- Heroes and units can be grouped into an **army** by ordering them to **follow** a leader.
  The army moves as one.
- Units that follow certain heroes gain a **Buff**.
- Units can be grouped or ungrouped one at a time or all together.

### Merging
- **Regular units** can be merged into a single unit. **Heroes can't be merged.**
- Merging adds individuals to the target unit, which makes it bigger.
  A bigger unit also makes a **ranged attack** stronger.
- Merged individuals receive the **Buffs of the target unit**. This includes Combat
  Experience, so merging can spread positive buffs and dilute or remove negative ones.
- Only units of the **same type** can be merged, for example two Human Swordsmen units.
  *(Observed in-game.)*

### Splitting
- A unit can also be **split** into smaller units of the same type. *(Observed in-game.
  The help pages don't mention it.)* How the split amount is chosen, and whether buffs
  are copied to both halves, isn't known yet.

### Selection info
- Selecting a unit or army shows its **total strength** (Might) and lists the **individual
  units** it's made of. *(Observed in-game.)*
- Example (`reference/screenshots/stack-selection-list.webp`): a stack token reading
  **1650** at Warmwood lists:

  | Unit | Strength | Per soldier |
  |------|----------|-------------|
  | 50 Human Swordsmen | 600 | 12 |
  | 25 Elven Archers ⚡ | 350 | 14 |
  | 25 Elven Archers ⚡ | 350 | 14 |
  | 25 Elven Archers ⚡ | 350 | 14 |
  | **Total** | **1650** | |

  - The map token shows the **sum** of every unit in the stack.
  - **Elven Archer units are 25 strong**, half the 50 of Human Swordsmen.
    *(inferred)* Training size may depend on race or unit type.
  - The **⚡ icon** marks units with an active ability. For archers that's their ranged attack.
  - *(inferred)* Each soldier is +2 above its base (Swordsman 10 → 12, Archer 12 → 14).
    That could be **two battle wins** at +1 each, or a **settlement's +2 Fortifications**.
    In the intro video, archers standing in a hall with +2 Fortifications also show 350
    (§18.8). Fortification is the more likely explanation.
  - These three archer units are the same type, so they could be merged into one unit of 75
    (Might 1050). That makes a single, stronger ranged attack.

### Buffs
- A Buff is an enchantment or special condition on a unit. It can be positive
  (such as +Strength) or negative (such as being unable to move).
- Each Buff shows its effect, its remaining duration (unless permanent) and its caster.
- Every Buff comes from a special ability, except for:
  - **Combat Experience:** every battle a unit wins gives each of its individuals **+1 Strength**.
  - **Fortifications:** a settlement defence bonus.

---

## 9. Hero Collection, Deck & Hand

### Collection
- A persistent, cross-game set of **hero cards** and **special unit cards**.
- It grows through:
  - **Volunteers:** when you take over a settlement, a hero may offer to join you.
    You pay **1 Hero Coin** instead of its Gold cost. The hero deploys
    immediately and is added to your Collection permanently.
  - **The Tavern** (see [Shadow Bazaar](#10-shadow-bazaar--tavern)).

### Deck
- You build your deck from your Collection before a game starts.
  A minimum or maximum deck size is not specified.
- Build advice from the source:
  - Include cards of your **own race**.
  - Include races found **near you** on the map, since you're likely to capture their settlements.
  - Leave out races that don't appear on the map, or appear only far away.

### Deck builder ("Assemble Your Heroes!")
- Seen in the intro video (§18.8). The left side shows **Your Deck** with a card count, and the right side
  shows **Your Collection**, filtered by race (dropdown) and with a count per card (×1, ×2…).
- The deck starts with **Deck Essentials**, a fixed set of 5 kinds (7 cards).
- On top of that you can **select up to 12 kinds of card** from your collection. Adding a
  card lowers its count in the collection (×1 → ×0).
- Buttons: *Add To Deck*, *Remove from Deck*, *Start Game*.

### Hand
- The game starts with a **5-card hand** drawn from your deck.
- Whenever the hand has **fewer than 5 cards**, **1 card** is drawn from the deck.
- The hand can go **above 5** through Tavern purchases or extra draws.

---

## 10. Shadow Bazaar & Tavern

| Shop          | Cost         | You get |
|---------------|--------------|---------|
| Shadow Bazaar | 10 Valour    | 20 Mana |
| Shadow Bazaar | 10 Valour    | 200 Gold |
| Shadow Bazaar | 2 Valour     | Draw the next card from your deck into your hand |
| Tavern        | 2 Hero Coins | Draw 3 cards of a race you choose and keep 1. It goes into your hand **and** your Collection |

---

## 11. Zombies

### Terrain bonus
- Each zombie race is **50% stronger** on its home terrain (see [Races](#2-races)).
- Luring zombies off their home terrain removes the bonus.
- A unit's current buffs appear in its details panel.

### Zombie movement AI
- Zombies always head for the **nearest unblighted settlement or Mana Pool**,
  measured in a **straight line** ("as the Gryphon flies").
- If two targets are equally close, one is chosen **at random**.
- Zombies are usually **slower than their living counterparts**. Each race has its own speed.
  For example, Undead Goblins are slower than living Goblins but faster than living Trolls.
  Exact speeds are not specified.
- Buffs can make zombies faster or slower.
- Hero powers can make zombies **flee**, **follow the caster**, or stay **pinned in place**
  for a while. The source calls controlling zombie movement a key strategy.

### Zombie bosses
- A boss is created when a zombie **blights a Mana Pool**.
- A boss has unique powers that **affect the whole map**. Players usually have to work
  together to defeat it.
- Each race has two possible bosses:

| Zombie race     | Boss 1          | Boss 2              |
|-----------------|-----------------|---------------------|
| Zombie Humans   | Dread Knight    | Necromancer Lord    |
| Immortal Elves  | Lich King       | Nightmare Lord      |
| Undead Dwarves  | Ironhide        | Lord of Destruction |
| Zombie Orcs     | Queen of Lies   | Lord of Purgatory   |
| Immortal Trolls | Trailblazer     | Lord of Confusion   |
| Undead Goblins  | Jester King     | Master of Coin      |

Boss stats and powers are not specified.

---

## 12. Graves, Spawning & Reaper's Tally (scoring)

### Graves and spawning
- When a zombie kills a living creature, an **infected body** goes into a
  **battlefield graveyard** at that spot.
- After a while, each infected body (a **restless soul**) **rises as a new zombie**.
  The delay is not specified.
- The more zombies spawn, the further they spread and the more graveyards they create.
  The Blight grows exponentially.
- **Burning bodies** stops them from ever rising:
  - Moving **any** of your heroes or units through a graveyard burns its bodies automatically.
    Flyers set to Avoid are the exception.
  - Winning a battle over a graveyard burns its bodies when the battle ends.
- The game can't end while any infected bodies remain unburned.

### Reaper's Tally (scoring)
- The game starts with a fixed **living population** across the map.
- Living creatures die as **soldiers killed in battle** or **civilians slaughtered by zombies**.
- The dead become restless souls. They stay that way until they are burned on a
  pyre or rise as walking dead.
- **Score** is the percentage of the starting living population still alive at the end.
- The faster the game is won, the more souls survive and the higher the score.

---

## 13. Combat

### When combat starts
- Combat starts when enemy units meet **on a path** or **in a settlement**.
- The battle is resolved **exactly 1 hour** after first contact.
- Any unit that arrives at the location during that hour **joins** the battle.
- Units that have joined a battle **can't leave** it.
- Heroes can use special powers during the battle.

### Might
```
Might = Population × Strength
```
Might is totaled for each side at the start of the battle. Strength includes terrain bonuses,
buffs, Combat Experience and fortifications.

### Melee resolution
- The side with the **higher Might wins**.
- **Every unit on the losing side is destroyed.**
- The winner takes casualties. Each individual in the winning army has a
  chance of dying, calculated from the **squared** ratio of the two sides:
  ```
  P(death per winning individual) = (Might_loser)² / (Might_winner)²
  ```
  The source's example: if the loser's squared value is 25% of the winner's, each winner has a 25% chance to die.
  A much stronger winner loses very few troops.
  > The in-game Combat Detail screens confirm that squared **Might** is used
  > (see the worked examples in §18).
- After winning, the survivors gain **Combat Experience** (+1 Strength each).

### Ranged attacks
- The attack's Might is compared with the defending stack's Might.
- If **attack Might > defender Might**, the defender is **destroyed**.
- Otherwise, each individual in the defender dies with probability:
  ```
  P(death per defender individual) = Might_attack / Might_defender
  ```
  This ratio is **not squared**.
- The ranged attacker **can't be harmed**.

| Aspect               | Melee                          | Ranged |
|----------------------|--------------------------------|--------|
| Outcome              | Higher Might wins, loser wiped out | Defender wiped out if attack > defense |
| Casualty ratio       | Squared                        | Linear |
| Who takes casualties | Winner (loser is wiped out)    | Defender only |
| Attacker risk        | Yes                            | None |

---

## 14. Diplomacy & Trade

- **Chat:** one shared channel for all players.
- **Diplomacy:** private conversations with one or more chosen players.
- Gold, Mana and Valour can be sent to any ally through the **Trade** section of their
  Empire screen: pick the resource, enter an amount, press Send.
  Examples from the source: Dwarves trade Gold to Elves for Mana, and Dwarves trade Valour with Humans.
- Settlements can be **gifted** (costs Valour).
- Teams are expected to send help to players who are being overrun.

### Inbox
- Shows messages, a **Combat** tab with a log of every battle and its details, and an **Events** tab
  with spells and ranged attacks. Selecting an event pans the map to it and replays it.
- This matters in async multiplayer, because a lot happens while you're offline.

---

## 15. Strategy notes from the source

1. Deploy heroes right away and get them moving.
2. Take a **Mana Pool** and several settlements toward the zombies early.
3. Reach the outbreak quickly and **burn graveyards**. Every body burned is one fewer zombie later.
4. **Lure zombies off their home terrain** to remove their +50% bonus.
5. Keep zombies away from Mana Pools to prevent bosses.
6. Coordinate with teammates and trade resources to where they're needed.

---

## 16. UI / Controls (original game)

| Key            | Action |
|----------------|--------|
| Space / Q      | Next idle unit |
| E              | Previous idle unit |
| Arrows / WASD  | Pan map |
| R              | Move selected unit |
| Z              | Toggle max zoom |
| - / +          | Zoom out / in |
| 1              | Player screen |
| 2              | Settlement summary |
| 3              | Army summary |
| O              | Options |
| I              | Inbox |
| H              | Help |
| Esc            | Close current screen |

Interface options: map graphics quality (low/high), UI docking (left/right/center),
audio toggle, and leaving a game so another player can take the slot.

---

## 17. Values not specified by the source (to design ourselves)

Items marked ✓ are partly answered by the screenshots in §18.

- Valour cost to capture each settlement or Mana Pool (✓ observed: 2 Valour for a 200-person Human village)
- Valour reward per zombie kill (✓ observed: about 1 per 6–7 kills), and for long time jumps in single player
- Valour cost of short time jumps, flyer stance changes and gifting
- Gold and population cost of each regular unit, and its size
- Strength and speed of every unit, hero and zombie race (✓ partial, see §18.3)
- Hero roster, abilities, Mana costs and recharge times (✓ a few cards, see §18.4)
- Delay before an infected body rises
- Fortification bonus values
- Starting map population, settlement sizes per type (✓ typical sizes, see §18.5)
- Deck size limits; Hero Coin sources
- Boss stats and powers (✓ three bosses, see §18.4)
- Claim reward table: what rewards exist and how they're chosen (✓ one seen: +150 Gold)

---

## 18. Worked examples & observed values

Taken from the in-game screenshots and text of the wargamer.fr preview
(<https://www.wargamer.fr/apercu-de-blight-of-the-immortals/>, 2016). Values marked
*(inferred)* are worked out by us from the numbers shown and weren't stated by the game.

### 18.1 Melee combat, example A: defenders win (Eagles Vail, day 2, 20h)

| Side      | Unit             | Might | Souls before | Souls after |
|-----------|------------------|-------|--------------|-------------|
| Attacker  | Immortal Elf     | 1666  | 119          | 0           |
| Defender  | Elven Archer     | 300   | 25           | 16          |
| Defender  | Human Swordsman  | 750   | 50           | 23          |
| Defender  | Wizard (hero)    | 105   | 1            | 0           |
| Defender  | Knight           | 500   | 20           | 9           |
| Defender  | Human Swordsman  | 750   | 50           | 33          |
| **Total** |                  | **1666 vs 2405** | 119 vs 146 | 0 vs 81 |

- The game's text: *1666² is 48% of 2405². All Attackers were completely destroyed.
  Each Defender had a 48% chance of being killed.*
- Check: (1666 / 2405)² = 0.4799, so 48%. The defenders actually lost 65 of 146 (44.5%),
  which is close to the expected 48%. Each individual rolls separately.
- The player earned **17 Valour** for **119 kills**.

### 18.2 Melee combat, example B: a near-even fight (Falcons Mire, day 4, 17h)

- 1 Immortal Elf stack (Might 1701, 81 souls) attacks 3 Ents (Might 781, 501 and 500, 1 soul each).
  The totals are **1701 vs 1782**.
- (1701 / 1782)² = 0.91, so each Ent had a 91% chance of dying. **All three died anyway**,
  even though their side won and the whole zombie stack was destroyed.
- Lesson: winning by a small margin is nearly as costly as losing, but it still stops
  the zombie stack. The article notes this is still better than losing to the zombies.
- **11 Valour** for **81 kills**.
- *(inferred)* Valour reward is roughly **1 per 6–7 zombies killed**. Observed: 119 kills → 17,
  81 kills → 11, 24 kills → 4 (§18.8). No simple formula fits all three exactly.

### 18.3 Battle preview, example C: overwhelming force

- Stacks: 32 Dwarven Hammers (Might 1071) + 40 Dwarven Hammers (Might 640) against
  11 Undead Dwarves (Might 297).
- The preview reads *Living: 1711 Strength* against *Undead: 297*, and *"Living win and each soldier has a 3% chance of dying."*
- Check: (297 / 1711)² = 0.030, so 3%. A 6:1 advantage makes losses nearly zero.
- *(inferred)* Per-individual strengths you can read off these numbers:
  | Unit | Might ÷ souls | Note |
  |------|---------------|------|
  | Human Swordsman (fresh, from tutorial) | 500 / 50 = **10** | stated on the training screen |
| Undead Dwarves (tutorial, plains) | 720 / 40, 1440 / 80 = **18** | off home terrain, so this fits a base of 18 |
| Dwarven Hammers (fresh) | 640 / 40 = **16** | |
  | Dwarven Hammers (veteran) | 1071 / 32 ≈ **33** | combat experience plus buffs |
  | Undead Dwarves | 297 / 11 = **27**; 1269 / 47 = **27** | in mountains, so 18 × 1.5 home bonus |
  | Human Swordsman (mid-game) | 750 / 50 = **15** | base 10, so +5 from experience or buffs |
  | Elven Archer | 300 / 25 = **12** | |
  | Knight | 500 / 20 = **25** | |
  | Immortal Elf | 1666 / 119 ≈ **14** | |
  | Ent (hero-like, 1 soul) | **500** base, 781 buffed | |

### 18.4 Card examples (heroes and bosses)

| Card | Type | Cost | Might | Speed (h/League road) | Ability |
|------|------|------|-------|-----------------------|---------|
| **Wizard** (Uncommon) | Mortal Human Mage, Plain | 200 Gold | 1 × 100 | 4h | **Shall Not Pass:** range 1, a Strength 200 ranged attack, and the target can't move for 6h. Recharges in 6h and costs **12 Mana**. |
| **Gryphon Riders** (Rare) | Mortal Dwarf, flying | ~2,500 Gold (hard to read) | 5 × 300 = 1500 | Flying | Hard to read in the screenshot |
| **Nightmare Lord** (boss) | Immortal Elf Warrior, Forest | — | 1 × 600 | 4h | **Fear the Dark:** every 18h, all Mortal units within 2 Leagues must **flee for 6h**. |
| **The Jester King** (boss) | Immortal Goblin Warrior, Swamp | — | 1 × 300 (+400 shown) | 4h | **Fool's Power:** +100 Strength for **every hero or unit card deployed** by players. Kill him early. |
| **The Trailblazer** (boss) | Immortal Troll Warrior, Swamp | — | 1 × 900 | **2h** (fast) | **Demon Speed:** every 18h, all Immortals within 2 Leagues **move faster**. |

Card-rule patterns worth copying:
- Normal speed is **4 hours per League on road**. Fast units take 2h.
- Ability text gives **range in Leagues**, a **duration**, a **recharge** time ("Restores in Xh") and a **Mana cost**.
- Boss auras work on a timer ("every 18 hours") and affect an area ("2 league area").
- The Wizard's Might of 105 in example A, against a base of 100, shows that combat experience or buffs add to a hero's
  strength as well.

### 18.5 Map, economy and session values

- **Settlement sizes seen:** villages of 20–50, towns of 100–300 (200 is common), and
  dwarven fortresses of about 200 Dwarves paying 400 Gold a day.
- **Monster lairs:** 20 Gryphons, 6 Hydra, 3–5 Ents.
- **Mana Pool output:** each shows **20** on its badge (20 Mana/day).
- **Starting resources** at game start in the screenshots: **1000 Gold, 20 Mana, 20 Valour**.
- **Single-player jump:** "Jump 6 Hours" costs **0 Valour**. The arrows change the length.
- **Game length:** the solo scenario "Ironwood River" (Hard) was won at **Age 7d 16h**.
- **Score example:** **2,334 souls saved = 47%**, so the starting population was about 4,970.
  The result screen shows a **star rating** (47% gave 2.5 of 5 stars).

### 18.6 Strategy notes from the article

- **Population is a double-edged sword.** It is income and the source of soldiers, but if
  a town falls, all of it becomes zombies. Sometimes the right move is to **empty or raze
  a village** before a horde you can't stop reaches it.
- **Keep reserves.** Zombie movement has random elements (tie-breaks, rising graves,
  boss auras), so you need spare troops to react.
- **Some powers are double-edged** and can hurt you as well (for example, fear effects scattering
  nearby units).
- **Protect Mana.** Losing your Mana Pools leaves your heroes' abilities useless.
- **Difficulty levels:** at least *Hard* and *Nightmare*. A 6-player Nightmare co-op is the
  hardest setting.
- **Meta progression:** after each game you earn **Hero points** based on your score.
  You spend them in the Bazaar on new cards.

### 18.7 The in-game tutorial (single player)

From the tutorial screenshots in [reference/screenshots/](reference/screenshots/):

1. **Objective** (`tutorial-1-objective`): destroy the undead outbreak **as fast as you can**.
   You win when every zombie is destroyed. Your score is how many people are left alive.
2. **The horde** (`tutorial-2-zombie-horde`): a horde of Undead Dwarves moves **from village to
   village**, kills everyone and infects their bodies with the Blight. The blighted bodies
   **slowly rise** as zombies.
   - At the start, three dwarven fortresses (Shallow Mountain, Ironhelm Fortress, Rams Pass)
     are already blighted. Zombie stacks of **720** and **1440** Might sit around them.
3. **Starting position:** the player already owns **6 Human villages** (200 Humans each,
   100 Gold/day each, so 600 Gold/day in total) and **1 Mana Pool** (Yellowsprings, 20 Mana/day).
   One village (Wolfs Plain) already has an army of 500 Might. Starting resources are 1000 Gold, 20 Mana and 20 Valour.
4. **Training** (`tutorial-3-train-units`): open a village and press *Train for 250 Gold* to train
   50 of its 200 villagers as Human Swordsmen at 10 Strength each (Might 500).
   - Training takes **6 hours (1 turn)**.
   - The tutorial's advice: at the start, **build an army at each of your villages**.
   - Village Gold is paid as a **lump sum once every 24h**. The panel shows a countdown,
     e.g. *"100 Gold in 7h 9m 44s"*.
   - A village can be given up with **Relinquish Command**.
5. **Moving** (`tutorial-4-move-army`): select the army and press *Move*. The tutorial's advice:
   **intercept the zombies** before they reach your undefended villages.
   Use *gather* (▲) to pull all nearby units into one army, and *disband* (▼) to split it again.
   - **Worked example** (user-provided screenshot, not saved): 50 Human Swordsmen
     (500 Strength) at Wolfs Plain are ordered **1 League north-west across open plains**
     to an empty waypoint. The path label reads **6h**. That matches the rule:
     4h per League by road × 1.5 for plains = 6h, so the move takes exactly one turn.
6. **Combat** (`tutorial-5-combat`):
   - The army with the **smaller strength is completely destroyed**.
   - There is **no luck in deciding the winner**. Luck only decides losses: each soldier in the
     winning army **rolls a saving throw**.
   - The illustration shows an Orc army of 1200 beating zombies of 560 and ending at 696.
     The formula predicts about 22% losses (an expected ~936 left), so the art is
     probably just an illustration, not an exact result.
6b. **Battle in progress** (`tutorial-7-combat-markers`): the stacks in a fight merge into
   one **crossed-swords token** showing the **combined Might of both sides**, for example
   1940 = 1440 zombies + 500 Swordsmen. It stays until the battle resolves 1 hour after contact.
   Battles happen on open-country waypoints too. The same screenshot confirms that training
   lowers income: Rangersplain went from 100 to 75 Gold/day after training 50 of its 200 villagers.
6c. **Claiming a settlement** (`tutorial-8-claim-settlement`), at Age 18h:
   - The panel prompts you to move a unit into the settlement and take command, then train its
     villagers and collect its Gold.
   - Your unit must be **standing in the settlement**. Here a 50 Human Swordsmen (500)
     army is listed under *Heroes & Armies*.
   - **Claim for 2 Valour** (a 200 Human village).
   - **Before you claim it,** the panel already shows population (200), production (0.5 Gold per villager
     every 24h) and a running **Production ETA** countdown ("100 Gold in 13h 59m 13s"). The
     clock keeps running for neutral settlements too.
   - The training offer is shown but locked: claim the settlement first, then train
     50 Swordsmen for 250 Gold.
   - Resources at 18h: 125 Gold, 40 Mana, 24 Valour. Mana has gone up from 20 to 40 (one Mana Pool payout),
     and Valour from 20 to 24 *(inferred: from zombie kills)*.
   - **After claiming** (user-provided screenshot, not saved): a *Reward* panel opens: *"The people
     of Druid Farm offer you this reward for taking their settlement under your
     protection."* The reward is **A pouch of Gold! +150 Gold**. A *Show Settlement* button
     returns you to the settlement panel.
   - Net effect: Valour **24 → 22** (−2 to claim) and Gold **125 → 275** (+150 reward).
     Claiming for 2 Valour paid back more than half the cost of training an army.
7. **Turns** (`tutorial-6-jump-6-hours`): **single player is turn-based**. When your turn is done,
   press *Jump 6 Hours* to move the clock forward. **1 turn = 6 hours.**

Example opening based on the tutorial, as a design reference:
- Turn 1: train 50 Swordsmen in all 6 villages, which costs 6 × 250 = 1500 Gold. You can only afford 4 with
  1000 Gold, so train in the 4 villages closest to the zombies first.
- Each trained village drops to 150 villagers, so its income falls from 100 to 75 Gold/day.
- Turn 2 (6h later): the armies are ready. Gather them and march to meet the 720 stacks
  one at a time. 4 × 500 = 2000 Might against 720 gives each soldier a
  (720 / 2000)² ≈ 13% chance to die. Against the 1440 stack it would be
  (1440 / 2000)² ≈ 52%, so wait for reinforcements first.

### 18.8 Official 4-minute introduction video

Source: *"Blight of the Immortals – 4 Minute Introduction"* by the developer, Jay Kyburz
(<https://www.youtube.com/watch?v=Q4_sKhbQSzU>). This combines the narration (auto-captions)
with frames saved in [reference/video-intro/](reference/video-intro/). The file names start
with the timestamp in seconds.

**What the narration says (paraphrased):**
- Co-op multiplayer against a zombie outbreak. Multiplayer is **slow real-time**: the game ticks on in
  the background and you check in during the day to use powers and give orders.
  Single player is turn-based, and **you choose how far to jump**. The developer says
  multiplayer is the best way to play.
- A move that says *4 hours* in multiplayer takes **4 real hours**.
- Kinds of hero powers mentioned: **pin** hordes in place, **send them running**, **draw
  zombies to you**, **raise armies faster**, **dig for Gold**, **build fortifications**.
- Gold deploys heroes from your hand. Heroes go into settlements of **their own race**. Mana pays
  for powers.
- Using a power: click the hero, click the power button, then **confirm the area** or **click a
  specific target** on the map.
- Moving: select the unit, click *Move* and **build a list of nodes**. On PC you can
  right-click instead.
- Claiming: with a unit in a settlement, spend Valour. **In multiplayer the only way to earn
  Valour is fighting zombies.** You get Valour for every zombie destroyed.
- Combat happens automatically when enemies meet **on a hex or on the path between two
  hexes**. The bigger army always wins with no randomness, and the loser is wiped out. A detailed
  combat log goes to your inbox after every battle.
- Burn bodies in a battlefield graveyard by **moving any unit past it**.
- A claimed **Mana well** gives Mana throughout the day. If zombies capture one, a boss spawns.

**Hard numbers from the frames:**

| Frame | Observation |
|-------|-------------|
| 0040, 0168 | Time-jump costs: **Jump 2 Hours = −4 Valour**, **Jump 1 Hour = −5 Valour**, Jump 6 Hours = 0 |
| 0072 | Deck builder: Deck Essentials 7 cards; "select up to 12 kinds of card"; deck grew 7 → 10 |
| 0106 | Hero stack at Blue Plain (570): **Wizard 100**, **Cowardly Noble 20**, **20 Knights 400** (20 each), **Gnostic Mage 50**. Rows with an ability show ⚡ |
| 0112 | *Shall Not Pass* targeting: "5 Immortal Elves, 70 Strength" (14 each). The target gets a red bullseye on the map |
| 0128 | Move mode: "Build a list of locations for your hero to move to" with **Clear Path / Save / Cancel** |
| 0145 | **Elven Great Hall** (neutral): 150 Elf Villagers, 1 Gold/villager/24h, **Fortifications +2 Strength**, **Claim for 3 Valour**. Train **25 Elf villagers → Elven Archers @ 12 Strength for 225 Gold** (9 Gold per archer) |
| 0158 | After claiming: population **149** (a deployed **Elven Princess**, 188 Strength, took 1 villager). The train button reads **"Training for 6h"** while busy. *Show Reward* replays the claim reward |
| 0190 | Combat log at Yellow Vail: Zombie Human 432 (24 souls, 18 each) against Human Swordsman 500 (50) + **Storm Friar** 50 (1). *432² is only 62% of 550²*: undead destroyed, each living soldier had a 62% chance of dying. Result 51 → 20 survivors. **24 kills → 4 Valour** |
| 0200 | Clicking a blighted settlement lists *"Brown Valley — Blighted"* and **"158 Human Bodies"** in its graveyard |
| 0212 | A 300-strength army ordered from Yellow Vail to Brown Valley (**6h**) to burn the bodies |
| 0222 | Red Mud Mana well (owned, 20/day) surrounded by zombie-held villages. Tall Valley is **on fire** under a 1419 horde |

**What this adds or changes:**
- **Unit size and cost differ by race:** Humans train 50 Swordsmen (10 Str) for 250 Gold. Elves train
  25 Archers (12 Str) for 225 Gold.
- **Deploying a hero costs 1 villager** of population (Elven Princess: 150 → 149).
- **A whole settlement becomes bodies:** Brown Valley's ~158 villagers became 158 Human Bodies.
- **A battle can kill most of the winner:** at 62%, the Swordsmen lost 30 of 50 and the Storm Friar died.
- **More hero names to use as inspiration:** Wizard, Cowardly Noble, Knights, Gnostic Mage, Elven Princess, Storm
  Friar.
