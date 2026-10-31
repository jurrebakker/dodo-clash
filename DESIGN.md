# Dodo Clash: Game Design (draft v0.1)

> *Mauritius, 1598. For a million years the dodo had no enemies. Then the ships came.*

Dodo Clash is a browser strategy game. You lead the birds of Mauritius against
the animals that people brought to the island. Blight of the Immortals is our reference
for the overall **genre** (see [GAMERULES.md](GAMERULES.md)): a slow-paced map
strategy game where a threat spreads and you contain it. But Dodo Clash has its own
setting, its own way of spreading the threat, its own economy and its own numbers. See
[§12 What we deliberately do differently](#12-what-we-deliberately-do-differently).

---

## 1. Premise

- **Setting:** Mauritius around 1600, a volcanic island with no natural predators.
  Ships drop off sailors, dogs, pigs, cats, rats and macaques. Each one threatens
  the dodo in its own way.
- **The player** controls the **dodos** and their allies among the island's native animals.
- **The enemy** is the **Invaders**: the introduced species, spreading out from where the ships land.
- **Goal:** survive. Push the invaders back, destroy their **dens** and keep as many
  dodos alive as possible.
- **Tone:** light and a bit funny on the surface (a clumsy bird fighting back),
  with a melancholy layer underneath, because in reality the dodo was extinct by about 1662.
  The game asks: *what if they had fought back?*

### Win, lose and score
- **Win:** every invader on the island is defeated **and** every den is destroyed.
- **Lose:** every dodo colony has fallen.
- **Score:** the share of the starting dodo population that is still alive. Grading:
  *Extinct → Endangered → Vulnerable → Thriving*.

---

## 2. The island (map)

- Based on the real geography of Mauritius, simplified to a hex map with
  a **waypoint grid** for movement. One step on the grid is one **stride**.
- **Terrain:**

| Terrain | Real-world inspiration | Move cost |
|---|---|---|
| Coast & beach | lagoons, sandy beaches | 1x |
| Grassland | central plateau | 1.5x |
| Ebony forest | the original rainforest | 1.5x |
| Marsh | Mare aux Songes (where the most dodo bones have been found) | 2x |
| Mountains | Le Pouce, Black River Gorges | 2x |
| Footpath | trampled animal trails | 0.75x (faster) |
| Water | lagoon, reef, rivers | impassable (except for flyers) |

- **Map locations:**
  - **Colonies:** dodo nesting grounds. They produce food and can train new flocks.
  - **Ally settlements:** homes of other native species (see §4).
  - **Freshwater springs:** produce **Spirit** (see §5). If invaders take one,
    a **Plague** event starts (see §7).
  - **Harbours:** where ships land. New invaders come ashore here.
    Harbours can't be captured, only **blockaded**.
  - **Dens:** places where invaders breed (see §6).

---

## 3. Time

- **Single player:** turn-based. One turn is **4 hours** on the island. A **day** is
  6 turns, and food is counted per day.
- *Option for later:* asynchronous co-op, where several players each defend a part of the
  island and the clock runs slowly in real time.
- The "jump less time and pay for it" mechanic from the reference is **dropped**.
  Turns always have the same length.

---

## 4. The dodos and their allies (variety)

Each player's group is a **flock**. Flocks come in several **kinds**. Each kind has a home
terrain, a speed, a strength and one special ability. Instead of races with their own
villages (as in the reference), we have **dodo clans** plus **native allies**.

### 4.1 Dodo clans (you start with these)

| Clan | Home terrain | Speciality | Unit |
|---|---|---|---|
| **Forest Dodos** | Ebony forest | Balanced, the core troops | *Peck Flock* |
| **Marsh Dodos** | Marsh | Hard to dislodge, strong defence | *Mud Guard* |
| **Highland Dodos** | Mountains | Slow but very tough | *Rock Beaks* |
| **Shore Dodos** | Coast | Fast, good at blockading harbours | *Tide Runners* |

- A clan gets **+25% strength on its home terrain**. In the reference it's the enemy that gets this bonus.

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
| **Rodrigues solitaire** | Rare cousin, a hero unit | *Rally:* all flocks in the area gain courage (+strength) |

- **No cards and no deck.** Allies become available by **winning over their settlement**
  (with *Courage*, see §5). Each one can be trained at its own settlement.
- **Elders:** unique leader birds (one per clan or ally) appear when a
  colony grows big enough. An Elder has one active ability that costs Spirit.
  This replaces the reference's heroes and cards with something that grows out of the map itself.

---

## 5. Resources

| Resource | Comes from | Used for |
|---|---|---|
| **Fruit** 🍈 | Colonies (per dodo per day) and fruit trees on the map | Training flocks |
| **Spirit** 💧 | Freshwater springs | Elder and ally abilities |
| **Courage** 🪶 | Defeating invaders | Winning over settlements and springs |

- Fruit is **seasonal**. In the dry season (one "season" is every 10 days) colonies
  produce less. That gives the game a rhythm.
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

### 6.2 Spreading through dens (our main mechanic)

This replaces the reference's "bodies rise up as zombies".

1. An invader that **plunders** a colony eats eggs and dodos.
2. Each kind of invader builds a **den** nearby (a pig wallow, a rat nest, a dog lair).
3. A den **breeds new invaders** every turn. The more it has eaten, the faster it breeds.
4. **Destroying a den:** move a flock onto it, or win a battle there.
   A den you leave alone keeps growing until it becomes a **nest of the plague**.
5. **Ships** bring a new wave every X days, until the harbour is **blockaded**:
   your flocks stand on the harbour, so no new invaders can land.

### 6.3 Invader movement
- Invaders go for the **nearest colony with eggs**. Pigs and rats prefer the
  colony with the **most eggs**. Dogs prefer the **nearest flock** they can beat.
  Macaques **avoid** fights they would lose. Each species has its own behaviour,
  instead of one rule for all of them.

---

## 7. Plague events (instead of zombie bosses)

When invaders capture a freshwater spring, a **Plague** starts somewhere on the island.
This is a special invader with an effect on the whole map:

| Plague | Effect (idea) |
|---|---|
| **The Captain** | All sailors move faster for 2 days |
| **The Sow Queen** | Every pig den breeds twice as fast |
| **The Rat King** | Spawns rat swarms at every den |
| **The Hound Master** | Dogs track down hidden flocks |

---

## 8. Combat

- Combat starts when a flock and invaders meet on a waypoint or at a location.
  The battle is resolved **at the end of the turn**, so reinforcements can still join that turn.
- **Strength = number × individual strength** (plus terrain, Elder bonus and nest defence).
- **Outcome:** the stronger side wins. Losses follow a **saving throw** based on how the
  two sides' strengths compare.
  - We start from the square law (Lanchester's law, a general military rule of thumb):
    `chance each winner dies = (loser / winner)²`.
  - **Our own twist:** dodos that are **defending their own colony** count for 1.5x.
    Invaders that have to **flee** (losing badly with a ratio below 1:3) are not destroyed. They retreat to their den, so they don't die
    the way the reference's losers do. This makes chasing them and destroying the den important.
- **Experience:** a flock that wins gets **+1 strength** per individual, up to +5.

---

## 9. Interface (basics)

- A top bar with the day and turn, Fruit, Spirit and Courage, and an **End Turn** button.
- The map uses tokens with portraits. The number on a token is total strength.
  Dodo tokens have green frames and invader tokens red ones.
- Panels: a **colony panel** (population, eggs, Fruit, train), a **flock panel**
  (move, merge, split, ability), a **den panel** (species, breeding speed), a **battle report**.
- A shared visual language (move lines, travel-time labels, battle markers) may
  follow the conventions of the genre. Artwork, names and text are ours.

---

## 10. First playable version (MVP)

1. One small map (south-east Mauritius), single player, turn-based.
2. 2 dodo clans (Forest and Marsh), 1 ally (Giant tortoise).
3. 3 invaders (Sailors, Pigs, Rats), 1 harbour, dens.
4. Fruit and Courage. Spirit and abilities come later.
5. Combat with the square law, a battle report, and the win/lose screen with a score.

---

## 11. Open questions

1. **Technology:** plain HTML/Canvas or TypeScript, or a framework such as Phaser or PixiJS?
2. **Multiplayer:** single player only at first, or co-op from the start?
3. **Art style:** hand-drawn and cute, or atmospheric and realistic like the reference?
4. **Elders:** do we keep a hero layer, or do we leave it out entirely?
5. **Language:** English, Dutch or both?
6. **Historical accuracy:** how far do we follow real history (the dates of the ships, the
   extinction) for the story and the campaign?

---

## 12. What we deliberately do differently

To make sure Dodo Clash is its own game rather than a copy:

| Reference (Blight) | Dodo Clash |
|---|---|
| Fantasy races, zombies | Real native and introduced species, Mauritius 1600 |
| Hero cards, deck, Tavern, Hero Coins | **No cards.** Allies and Elders come from the map |
| Gold / Mana / Valour | Fruit (seasonal) / Spirit / Courage |
| Bodies rise as zombies | Invaders **breed in dens**. Ships bring waves |
| Mana Pool → zombie boss | Spring → **Plague** event |
| All zombies use the same targeting rule | **Each species behaves differently** |
| Loser is always wiped out | Invaders can **flee** to their den. Defending colonies get a bonus |
| Population only shrinks | **Eggs**: colonies grow back |
| Valour pays for shorter time jumps | Fixed turns, **End Turn** |
| Zombies stronger on home terrain | **Both sides** have home terrain |
| Score = % alive | Score = % of dodos alive, graded *Extinct → Thriving* |

All names, text, images and numbers in Dodo Clash are made by us. We don't copy any
assets, text or card content from the reference.
