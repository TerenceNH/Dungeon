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

The theme has to answer three things at once: **what the hub is**, **why death takes your materials but not your gear**, and **why upgrades exist**. Three different directions:

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

1. **Theme:** which of A (Last Ember), B (Colossus) or C (Shattered Sanctum) grabs you, or should I mix parts of them?
2. **Skills:** happy with the hybrid (spent XP for combat, use-based for life skills)?
3. **Map:** one big connected open world like V Rising, or a hub with separate zones and instanced dungeons?
4. **Shared hub:** one base the whole group builds together, or a base per player you can visit?
5. **Party size:** 2 to 4 players, or bigger?
6. **Combat controls:** Albion click-to-move, or WASD with mouse aim?
7. **Death detail:** should *anything* carried survive death, like one protected slot or whatever was banked at a waystone?
