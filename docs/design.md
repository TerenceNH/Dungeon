# Dungeon Game: Design Doc (first pass)

Working draft. Sections marked **Decided** come straight from Bam's answers. Sections marked **Proposed** are suggestions to react to. Comment on anything in the PR.

---

## 1. Pitch

A co-op, top-down 3D dungeon crawler (Unity) where friends head out from a shared hub into tiered biomes and dungeons, bring back materials, and pour them into upgrades that make the next trip faster, deeper and more profitable. OSRS-style "every goal unlocks the next goal" progression, Souls-style stat requirements on gear, and an Albion Online feel to the camera and combat.

**Audience:** shipping to friends. **Mode:** co-op. **Engine:** Unity, 3D.

## 2. What's decided

| Topic | Decision |
|---|---|
| Runs | You leave the hub, and you come back either on purpose or by dying. |
| Death | Carried resources are lost. Gear is kept. Resources probably can't be recovered. |
| Session length | Both short and long. ~20 min for a couple of boss kills or a small dungeon, 30 to 45 min for a big dungeon. |
| Camera / feel | Albion Online: top-down / isometric, readable, ability-driven. |
| Combat | Mix of player skill and build. Stats and gear can each make up for the other, as a rule of thumb rather than a strict formula. |
| Reasons to revisit biomes | All of them: rare drops, unique resources, recurring nodes. Biomes can go obsolete later. |
| Resource scaling | Early resources are a bottleneck (needing 1 or 2 is normal, 5 to 10 feels like a lot). Later areas supply them plentifully. |
| Base | An *area*, not a single building. Exact form depends on the theme (section 3). |
| Extras | NPCs, pets and companions, shortcuts, codex, and boss gating (but not on every tier). |
| Offline progress | Yes, the base keeps working while you're away. |

## 3. Theme options (Proposed)

The theme has to answer three things at once: **what the hub is**, **why death takes your materials but not your gear**, and **why upgrades exist**. Thirteen different directions:

### A. The Last Ember
The world has gone dark and cold. At its centre burns the last flame, and you are Emberbound: when you die, the flame rebuilds you.
- **Hub:** the circle of light around the flame. It's a clearing, ruins, a camp, whatever the light touches. Feeding the flame pushes the light outward, and every new ring of light is new buildable ground for stations.
- **Death:** your gear is *attuned* to you at the flame, so it's reforged with you. Raw materials aren't attuned. They're just matter, and they stay behind in the dark.
- **Upgrades:** everything is about feeding and spreading the light. Stations are lit braziers, NPCs are lost people who walk toward the light, and shortcuts are lanterns you light out in the world.
- **Flavour:** melancholy, Souls-adjacent, very easy to read visually (light = safe).

### B. The Colossus
Your hub is built on the back of a huge, slow, sleeping creature that wanders the world.
- **Hub:** a settlement growing on its shell. Upgrades literally add new terraces, huts and platforms to its back.
- **Death:** a bond to the Colossus drags your spirit home. The bond holds what's been grafted to you (your gear), but loose cargo is too heavy to pull back.
- **Upgrades:** feeding the creature makes it grow (more space) and wake up (it moves faster, goes further). Where it walks determines which biomes are close, so its route acts as fast travel and shortcuts.
- **Flavour:** whimsical and memorable. More work technically, since the hub moves.

### C. The Shattered Sanctum
Reality has broken into shards. Your hub is a small floating island at the centre, and the biomes are shards reached through gates.
- **Hub:** an island in the void. Restoring it pulls broken fragments back in, so the island physically grows piece by piece.
- **Death:** the Sanctum's anchor recalls anything bound to you. Unbound loot falls into the void between shards.
- **Upgrades:** each new gate is a new biome or dungeon. Gate upgrades are your shortcuts (deeper entry points, skip floors). Fragments you restore become new station sites.
- **Flavour:** clean fit for instanced dungeons and tiers (a tier = a ring of shards). Less "open world" than V Rising, though shards can be big.

### D. Grave Goods
You're already dead. You're revenants, raised from a forgotten necropolis to finish what you started.
- **Hub:** the graveyard and the crypts beneath it. It grows as you restore mausoleums, chapels and catacombs.
- **Death:** you rise again from your own grave. Your gear is your *grave goods*, buried with you, so it rises too. Anything else you were holding is just lost with your body.
- **Upgrades:** restoring the necropolis and raising more of the dead. NPCs are old souls you lay to rest or wake. Shortcuts are crypt tunnels that surface out in the biomes.
- **Flavour:** dark with a sense of humour, and a strong look. Pets could be skeletal or ghostly.

### E. The Dreamer
The hub is the mind of a sleeping giant, and the biomes are its nightmares.
- **Hub:** a calm, half-formed dreamscape that becomes more solid and detailed as you upgrade it.
- **Death:** dying in a nightmare wakes you. Only what's been *remembered* (gear forged at the hub) survives waking. Loose things you picked up fade like a dream does.
- **Upgrades:** "lucidity." The more lucid the dreamer, the more of the hub takes shape and the deeper into the nightmares you can go. Biomes going obsolete fits well: old nightmares lose their grip.
- **Flavour:** surreal. Biomes can be wildly different from each other and still make sense.

### F. The Mycelium Heart
A huge fungal network lives under the world, and you're spore-born, grown from it to gather what it needs.
- **Hub:** a glowing fungal grove around the Heart. Stations are grown, not built.
- **Death:** you sprout again at the Heart. Your gear is symbiotic and grows back with you. Raw materials are just matter, and the forest reclaims them.
- **Upgrades:** feeding the Heart spreads the network. Spreading roots into a biome makes fungal tunnels (shortcuts) and lets the network digest that biome's resources while you're away (idle production).
- **Flavour:** organic and eerie. It explains offline production better than any other option.

### G. The Crashed Ark
A great ship (sky-ship, or sci-fantasy vessel) crashed in a valley long ago, and you're its crew, rebuilt again and again by its systems.
- **Hub:** the wreck and the camp that has grown up around it.
- **Death:** the ship's rebuild bay reprints you. Gear is stored as a pattern in the ship's memory, so it's reprinted with you. Raw materials are physical and stay where you fell.
- **Upgrades:** repairing ship modules. Each module is a station (forge = fabricator, smelter = reactor). Fully repairing the Ark could be the end goal.
- **Flavour:** a clear long-term goal (get the ship flying), and room for a sci-fi twist on fantasy biomes.

### H. The Company
You're indebted contractors working for a shady expedition company that's claimed a dangerous frontier.
- **Hub:** the company's frontier outpost, which grows as you pay off your debt and earn the right to build.
- **Death:** the company's insurance covers your registered equipment and returns your body. Cargo isn't insured, and the company won't pay to recover it.
- **Upgrades:** paying down debt, buying permits and contracts. Quests are company jobs, and NPCs are other contractors and suppliers who set up shop as the outpost grows.
- **Flavour:** comedic and a bit cynical, which suits a game for friends. Easy to explain in one line.

### I. The Living Atlas
The world only exists where it has been drawn. You work for a cartographer, and the hub is the town on the atlas's first page.
- **Hub:** a hand-drawn town that gets inked in more detail as you upgrade it.
- **Death:** you're smudged out and redrawn at the margin. Gear you've had *inked into the atlas* at the hub is redrawn with you. Uncharted loot was never drawn, so it's gone.
- **Upgrades:** drawing more of the map. New biomes appear as you chart them, roads you draw become shortcuts, and the codex is literally the atlas's notes.
- **Flavour:** a striking art style (ink, parchment, watercolour biomes). Biomes unlocking by being drawn is a strong visual moment.

### J. The Fallen God
A god died and fell across the world. Its corpse became the land, and you're born from its blood.
- **Hub:** a settlement inside the god's ribcage, around its still-beating heart.
- **Death:** your blood returns to the heart and you're reborn. Gear made at the heart from god-bone is part of the god, so it returns too. Anything else rots where you fell.
- **Upgrades:** waking the heart. Each beat it gains spreads warmth further and opens new chambers (stations). Each biome is a different part of the body, so the map itself tells the story.
- **Flavour:** grand and grim, Souls-adjacent. Biomes can be weird in a way that still makes sense.

### K. The Collector
An eccentric, very rich collector wants one of everything in a dangerous world, and you're the expedition team.
- **Hub:** the collector's estate, with grounds, workshops and a growing museum.
- **Death:** the collector's recall charm brings you home. Gear is *catalogued*, so the charm brings it back. Uncatalogued loot isn't covered.
- **Upgrades:** new museum wings and estate buildings, funded by what you bring back. The codex is the museum itself, and filling exhibits gives bonuses.
- **Flavour:** light and charming. It makes the codex the centre of the game instead of a side feature.

### L. Clockwork Bodies
You're golems built by a reclusive artificer. Your soul is a core, and your body is whatever you build around it.
- **Hub:** the artificer's workshop town, full of half-built machines.
- **Death:** your body shatters and your core returns to the workshop. Your gear *is your body* (arms, plating, weapons fitted at the hub), so it's rebuilt from the blueprint. Loose materials are left in the wreckage.
- **Upgrades:** better bodies and better workshops. Stat requirements become frame requirements (a heavy cannon arm needs a strong frame).
- **Flavour:** gear and character are the same thing, which makes "gear can make up for stats" feel natural.

### M. The Storm's Eye
An endless storm covers the world. The hub is the only calm spot, its eye, held open by storm engines.
- **Hub:** a sheltered valley that widens as you build more engines.
- **Death:** the storm strikes you home through a lightning tether. Charged gear (bonded at the engines) conducts home with you. Loose materials scatter in the wind.
- **Upgrades:** more engines widen the eye and push back the storm, opening new biomes. Lightning rods out in the world are your shortcuts.
- **Flavour:** dynamic weather as a core mechanic. Storm intensity can rise the longer you stay out, which adds to the push-or-bank tension.

**Light lean:** A is the simplest to build and to explain, and it fits an open V Rising-style map best. C is the best fit if dungeons end up being the main content. B is the most distinctive, but it's the riskiest for a friends-and-hobby scope.

## 4. Core loop (Proposed)

```
Hub: craft, upgrade, collect idle output, pick a goal
   ↓
Head out: open biome or dungeon (shortcuts cut travel)
   ↓
Gather, fight, push deeper. Carried loot grows, and so does the risk
   ↓
Bank it (return / reach a waystone)     or     Die (lose carried resources)
   ↓
Hub: spend materials → upgrades that make the next run better
```

The tension that makes this fun is **push or bank**. Every minute deeper is more loot, but more to lose. That's a cheap way to get Souls tension without needing Souls-level combat.

Things that make the loop feel good:
- **Waystones / banking points** you unlock mid-biome. Reaching one banks your carried loot. Unlocking them is a big OSRS-style time-saver.
- **Carry capacity** (satchel upgrades, pack pets) as an upgrade track of its own.
- **Co-op revives:** a downed state, so friends can pick each other up before the death penalty hits. That gives co-op a clear job.
- **Clear goals at the hub:** a "next upgrade" board shows what you're short of and where it drops.

### Upgrades that get you more upgrades
This is the snowball Bam wants. Examples, roughly in the order a player would hit them:
1. Bigger satchel → bring home more per run.
2. Better gathering tools → faster nodes, more yield.
3. Waystones → bank loot mid-run, lose less on death.
4. Refining stations → turn surplus low-tier materials into higher-tier inputs.
5. NPC gatherers → collect low-tier resources while you're offline.
6. Shortcuts → less travel, more time spent where it matters.
7. Pets → auto-pickup, extra carry slots, or nudges toward rare nodes.

## 5. Biomes, tiers and resources (Proposed)

Each biome has a tier, its own resources, its own gear set and its own enemies.

**Scarcity curve.** A biome's signature resource is precious while you're in that tier, and becomes cheap afterwards:

| When you're in... | Tier 1 ore | Tier 2 ore | Tier 3 ore |
|---|---|---|---|
| Tier 1 | Rare. Recipes need 1 or 2, and 5 to 10 is a big haul | Not available | Not available |
| Tier 2 | Common. Drops in bulk as a byproduct | Rare | Not available |
| Tier 3 | Plentiful. NPCs gather it idly | Common | Rare |

How older resources become plentiful (pick one or mix):
- Higher-tier enemies and nodes drop lower-tier materials in bulk.
- Base production (NPC gatherers, farms) generates old-tier materials over time.
- Upgraded tools multiply yield on lower-tier nodes.

**When a biome goes obsolete,** it still has reasons to visit: codex entries, rare pet or cosmetic drops, and quest steps. It just stops being where your *progression* comes from.

**Gating between tiers** (selective, as decided):
- **Boss gates** on some tiers. The boss drops a key or a unique material.
- **Environmental gates** on others, e.g. a frozen biome needs cold-resistant armour, a poison swamp needs antidotes, a dark cave needs light.
- **Open** transitions where gear is the only gate.

## 6. Stats and gear (Proposed)

Souls-style attributes, for example: **Strength, Dexterity, Intelligence, Vitality, Endurance** (final list TBD).

Every weapon and armour piece has stat requirements and scales with certain stats.

**Soft requirements, not hard locks.** Being under a requirement makes the item weaker rather than unusable. Rough rule: each point under costs a percentage of its effectiveness, down to a floor. Meeting it gives full power, and going over it adds scaling bonus.

**Stats and gear compensate for each other.** Rule of thumb: one gear tier ≈ a band of character levels. A high-level player in old gear and a low-level player in great gear should both be viable, just in different ways. Some encounters can lean one way on purpose (a boss that punishes low Vitality no matter what you're wearing).

**Combat feel.** Albion-style: weapons define your active abilities, armour pieces may add one each. Skill expression comes from positioning, dodging and timing those abilities.

## 7. Skill progression options (Q6, open)

| Option | How it works | Good | Bad |
|---|---|---|---|
| **1. Use-based (OSRS)** | Mining makes you a better miner, swinging a sword makes you better with swords | Very satisfying; every action counts | Grindy; hard to balance combat; friends who play less fall far behind |
| **2. Spent XP (Souls)** | Earn XP, spend it on the stat you choose | Full control over builds; easy respecs | Gathering and crafting feel flat |
| **3. Hybrid** *(recommended)* | Combat attributes from spent XP. Gathering, crafting and utility skills level from use | Builds stay deliberate; life skills keep the OSRS "number go up" feeling | Two systems to explain |

Why the hybrid fits co-op: friends naturally specialise in life skills (one becomes the smith, another the alchemist), which gives everyone a role at the hub, while combat builds stay flexible. Suggested life skills to start with: Mining, Woodcutting, Smithing, Alchemy, and one utility skill (e.g. Scouting or Cartography).

**Catch-up idea:** XP boost for anyone below the party's highest level, so a friend who misses a week can catch up.

## 8. The hub (Proposed, shaped by theme)

An area that grows, not a building. Stations are placed in it, and each station has its own upgrade path:
- **Forge** (weapons, armour), **Smelter / Refinery** (ore → bars, tier conversion), **Alchemy** (potions, resistances), **Garden / Farm** (consumables, idle output), **Storage**.

**Idle production:** stations process queued jobs in real time, including while everyone's offline. Output is capped by storage, so coming back after a week isn't wildly better than after a day.

**Shared or personal?** For co-op, a shared hub with personal storage is probably simplest (see questions).

## 9. NPCs, pets, shortcuts, codex

**NPCs.** Rescued in biomes and dungeons. Each one moves into the hub and unlocks a service plus a short quest line. Examples: a smith (better recipes), a cartographer (reveals map areas, waystone upgrades), a beastmaster (pets), a quartermaster (storage, bigger satchels), a gatherer (idle resource collection).

**Pets and companions.**
- *Pets* are utility: carry slots, auto-loot, gathering help, finding rare nodes. Tamed or hatched from biome drops.
- *Companions* are combat helpers, mainly for solo sessions, so one player can still play when friends are offline.

**Shortcuts.**
- *World:* Souls-style doors, lifts and bridges opened from the far side.
- *Waystones:* unlockable banking and fast-travel points.
- *Dungeons:* after a full clear, unlock a skip to deeper floors or straight to the boss.

**Codex.** Records every enemy, item, resource and boss you've found. It fills in drop tables as you discover them, and kill milestones give small permanent bonuses against that enemy type (like an OSRS slayer perk). Good long-term goal for completionists.

## 10. Suggested first playable (Proposed)

Small enough to finish, big enough to test the loop:
- Hub with 3 stations (Forge, Smelter, Storage) and one upgrade step each
- 2 biomes (tier 1 and tier 2) with one boss gate between them
- 1 small dungeon
- 2 life skills (Mining, Smithing) and 3 combat stats
- 2 to 4 player co-op with downed/revive
- Death drops carried resources, keeps gear

If the "push or bank" loop is fun in this slice, everything else is just more of it.

---

## Questions for Bam (pick whichever you have opinions on)

1. **Theme:** which of the themes (A to M) grabs you, or should I mix parts of them?
2. **Skills:** happy with the hybrid (spent XP for combat, use-based for life skills)?
3. **Map:** one big connected open world like V Rising, or a hub with separate zones and instanced dungeons?
4. **Shared hub:** one base the whole group builds together, or a base per player you can visit?
5. **Party size:** 2 to 4 players, or bigger?
6. **Combat controls:** Albion click-to-move, or WASD with mouse aim?
7. **Death detail:** should *anything* carried survive death, like one protected slot or whatever was banked at a waystone?
