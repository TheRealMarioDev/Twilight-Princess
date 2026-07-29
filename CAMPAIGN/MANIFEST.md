# Twilight Princess AI Campaign — Manifest

This is the authoritative map of the campaign infrastructure on the `campaign-infrastructure` branch.

## How a new campaign chat should use this file

The player should not have to provide file paths manually.

After loading `CAMPAIGN/BOOTSTRAP.md`, inspect this manifest and retrieve the listed files directly from the repository. If the current scene requires a file not listed here, inspect the repository for additional relevant campaign files and load them as needed.

Do not ask the player for a path merely because a file is needed. Discover it from this manifest or the repository yourself.

If a listed file genuinely cannot be accessed or does not exist, report that specific problem rather than asking the player to enumerate repository paths.

Whenever a new campaign-support file is created, add it to this manifest immediately.

## Repository

`TheRealMarioDev/Twilight-Princess`

Branch: `campaign-infrastructure`

## Complete campaign architecture

```text
CAMPAIGN/       Runtime behavior, bootstrap, manifest, GM protocol
CANON/          Twilight Princess canon and progression reference
MEMORY/         Long-term narrative memory and important history
PLAYER/         Player-controlled Link state
RELATIONSHIPS/  Persistent relationship state and history
REVIEW/         Continuity/canon/relationship quality-control material
SESSIONS/       Session-level campaign history and resumable records
STATE/          Structured live campaign/world state
AI_RULES.md     Global AI behavioral contract
```

All of these systems are part of the campaign. A new AI must not assume that `STATE/` is the only persistent memory system.

## Authority hierarchy

The authoritative source depends on what is being checked:

1. `STATE/` — current structured campaign/world state.
2. `MEMORY/` — established player-created narrative history and important memories.
3. `RELATIONSHIPS/` — relationship history and current relationship state.
4. `PLAYER/` — player-controlled Link information and decisions.
5. `CANON/` — Twilight Princess canon, chronology, progression, and knowledge constraints.
6. `SESSIONS/` — session history and resumable narrative records.
7. `REVIEW/` — audits/checks, not a replacement for authoritative state.
8. `AI_RULES.md` — global behavioral rules that govern how the above systems are interpreted.
9. `CAMPAIGN/` — runtime loading and Game Master procedures.

When structured live state and prose conflict, do not silently choose one. Apply `AI_RULES.md`, inspect the relevant history, and resolve or record the discrepancy explicitly.

## CAMPAIGN/

- `CAMPAIGN/BOOTSTRAP.md` — Entry point for new chats; repository discovery, startup rules, player agency, and campaign premise.
- `CAMPAIGN/MANIFEST.md` — This file; authoritative map of all campaign infrastructure.
- `CAMPAIGN/GM_PROTOCOL.md` — Runtime procedure for scene preparation, narration, continuity, state updates, dialogue memory, canon handling, and romance handling.

## CANON/

- `CANON/canon_rules.md` — Canon-enforcement hierarchy, mandatory checkpoints, player-agency rules, and divergence policy.
- `CANON/chapter_guides.md` — Chronological Twilight Princess campaign chapter structure and progression gates.
- `CANON/knowledge_gates.md` — Character-specific information boundaries and spoiler/knowledge-leak prevention.
- `CANON/characters_major_minor.md` — Major and minor character reference information.
- `CANON/items_and_progression.md` — Item, equipment, progression, and dependency reference.
- `CANON/optional_content.md` — Optional-content integration rules; includes the mandatory Ending Blow exception.

`CANON/` is primarily read-only during gameplay. Do not rewrite canon to accommodate a player action. Genuine changes belong in `STATE/divergences.json` and the relevant history systems.

## MEMORY/

The `MEMORY/` directory is the long-term narrative memory layer. It is separate from the compact machine-readable state in `STATE/`.

- `MEMORY/character_development.md` — Persistent character development and meaningful changes over time.
- `MEMORY/important_dialogue.md` — Important dialogue and statements that should remain retrievable.
- `MEMORY/knowledge_state.json` — Persistent knowledge acquired by characters/player.
- `MEMORY/major_events.md` — Long-term record of major narrative events.
- `MEMORY/promises_and_secrets.md` — Promises, secrets, commitments, and unresolved personal information.
- `MEMORY/relationship_history.md` — Narrative relationship history that complements structured relationship state.

Memory priority:
- CRITICAL: permanent facts, major plot points, deaths, revelations, promises, permanent relationship changes, and canon divergences.
- IMPORTANT: meaningful conversations, character development, recurring personal details, and unresolved matters.
- CONTEXTUAL: ordinary low-impact details that may eventually be compressed.

Important dialogue should be retained faithfully when exact wording could matter later.

## PLAYER/

- `PLAYER/link.json` — Player-controlled Link state and the primary record of what the player has established about Link.

`PLAYER/` is sacred player-agency territory. The AI must not decide Link's dialogue, thoughts, feelings, choices, or actions unless the player explicitly delegates that control. The AI may maintain factual state resulting from player actions.

`PLAYER/link.json` should be read before Link-centric scenes and updated when player-controlled facts materially change.

## RELATIONSHIPS/

- `RELATIONSHIPS/relationships.json` — Persistent relationship data and relationship-state tracking.

This directory is the relationship layer and should be used alongside `MEMORY/relationship_history.md` and the structured `STATE/relationships.json` store.

Relationships must not be reduced to a single affection score. Preserve trust, affection, closeness, history, conflict, promises, emotional wounds, shared memories, current status, and meaningful changes.

Ilia's relationship with Link is particularly important because she is the campaign's established love interest and a major motivation for Link. Romance should evolve from accumulated events and player choices rather than arbitrary AI decisions.

## REVIEW/

The `REVIEW/` directory is the campaign quality-control/audit layer. Any files present there should be consulted when performing continuity, canon, relationship, knowledge, or divergence checks.

The AI should use review material to catch:
- continuity contradictions;
- forgotten dialogue or memories;
- NPC knowledge leaks;
- accidental control of Link;
- canon chronology errors;
- relationship inconsistencies;
- unrecorded state changes;
- unexplained divergences.

Review records do not override authoritative state; they identify problems that must be resolved explicitly.

## SESSIONS/

The `SESSIONS/` directory is the campaign's session-history layer. Any files present there should be used when resuming or reviewing previous sessions.

Session records may contain scene summaries, events, dialogue, state changes, and other information needed to reconstruct what happened in a particular session. Do not assume that ChatGPT's conversational context is the permanent memory of the campaign.

When a new session is played, preserve a useful resumable record in this directory when the existing session system calls for it.

## STATE/ — structured live state

These files are machine-readable campaign state. The AI should read relevant state before a scene and write/update affected state after significant events.

- `STATE/schema.md` — Definition of the structured state model and required fields.
- `STATE/current.json` — Unified live snapshot / fast-load state.
- `STATE/current_scene.json` — Current immediate scene context and scene-specific state.
- `STATE/canon_status.json` — Detailed canon/event progression state.
- `STATE/characters.json` — Live character locations, condition, goals, knowledge, relationships, memories, dialogue, actions, and canon status.
- `STATE/divergences.json` — Genuine player-created deviations from canon.
- `STATE/events.json` — Append-only significant-event history.
- `STATE/initial_relationships.json` — Starting relationship baselines.
- `STATE/inventory.json` — Link's inventory, equipment, currency, collectibles, keys, quest items, progression items, skills, and upgrades.
- `STATE/memories.json` — Compact structured important memories, dialogue, promises, secrets, revelations, trauma, and recurring details.
- `STATE/quest_state.json` — Current main-quest/side-quest state and dependencies.
- `STATE/quests.json` — Quest definitions/index and broader quest tracking.
- `STATE/relationships.json` — Live structured relationship state.
- `STATE/saves.json` — Campaign milestone snapshot index.
- `STATE/world.json` — Persistent world-state/progression information.

### State responsibilities

`STATE/current.json` is the fast orientation snapshot, not a replacement for detailed history.

`STATE/current_scene.json` contains immediate scene context and should not be treated as permanent memory unless the event is promoted to the appropriate history/memory store.

`STATE/world.json` tracks world-level progression such as Twilight regions, restored Light Spirits, Fused Shadows, Mirror pieces, dungeon/boss progression, and major world objects.

`STATE/inventory.json` tracks obtained/lost/equipped/used items and learned skills/upgrades.

`STATE/quest_state.json` and `STATE/quests.json` track active, available, completed, failed, and dependency-linked quests.

`STATE/characters.json` tracks NPC state and knowledge. Character facts that matter long-term should also be represented in `MEMORY/` where appropriate.

`STATE/relationships.json` tracks current relationship state. Long-term relationship history belongs in `RELATIONSHIPS/` and `MEMORY/` as appropriate.

`STATE/events.json` is append-oriented history. Significant events should record time, location, participants, what happened, meaningful dialogue, relationship effects, state changes, canon impact, and divergence impact.

`STATE/divergences.json` is used only when Link's actual player-controlled actions change, prevent, reorder, or substantially alter an established canon outcome. Do not create a divergence merely because Link explored or spoke differently while the canon event still occurred normally.

`STATE/saves.json` records milestone snapshots without deleting historical snapshots.

## AI_RULES.md

- `AI_RULES.md` — Global campaign AI rules and authority/continuity contract.

This file must be loaded before gameplay. It currently establishes, among other things, that the player controls Link, meaningful interactions must be remembered, characters only know what they have learned, canon chronology should be preserved unless legitimately changed, and important events must never be silently erased. fileciteturn22file0

Treat this as read-only campaign configuration during normal play.

## Runtime retrieval protocol

### Startup / new chat

1. Load `AI_RULES.md`.
2. Load `CAMPAIGN/BOOTSTRAP.md`.
3. Load `CAMPAIGN/MANIFEST.md`.
4. Load `CAMPAIGN/GM_PROTOCOL.md`.
5. Load the relevant `CANON/` rules and current chapter material.
6. Load `PLAYER/link.json`.
7. Load the relevant `MEMORY/` records.
8. Load `RELATIONSHIPS/relationships.json` and relevant relationship history.
9. Load `STATE/current.json`, `STATE/current_scene.json`, `STATE/world.json`, `STATE/canon_status.json`, `STATE/characters.json`, `STATE/inventory.json`, `STATE/quest_state.json`, `STATE/quests.json`, `STATE/relationships.json`, `STATE/memories.json`, `STATE/events.json`, and `STATE/divergences.json`.
10. Consult `SESSIONS/` when resuming an existing session.
11. Consult `REVIEW/` for applicable continuity/canon/relationship/knowledge checks.

### Before every continuity-sensitive scene

Read only the relevant portions where practical, but do not skip a system when its information could materially affect the scene.

At minimum consider:
- current scene;
- current world state;
- current Link/player state;
- relevant NPC state and knowledge;
- relevant memories;
- relationship state/history;
- current quest/canon progression;
- relevant canon chapter and knowledge gates.

### After every significant scene

Update all affected systems rather than relying on chat context:

1. Update `STATE/current_scene.json` if the immediate scene changed.
2. Update `STATE/current.json`.
3. Update `STATE/world.json` for world progression.
4. Update `PLAYER/link.json` for durable player-established Link state.
5. Update `STATE/characters.json` for NPC changes.
6. Update `STATE/inventory.json` for item/equipment/skill changes.
7. Update `STATE/quest_state.json` and/or `STATE/quests.json` for quest changes.
8. Update `STATE/canon_status.json` for canon progression.
9. Update `STATE/relationships.json` and `RELATIONSHIPS/relationships.json` when relationships change.
10. Promote meaningful history into the appropriate `MEMORY/` records.
11. Append significant events to `STATE/events.json` and relevant `MEMORY/major_events.md` records.
12. Record genuine canon divergence in `STATE/divergences.json` and relevant review/history records.
13. Update/create a `SESSIONS/` record when the session system calls for it.
14. Use `REVIEW/` to audit the resulting state when appropriate.

## Example: Ilia scene

Read:
- `AI_RULES.md`
- runtime protocol
- relevant canon chapter
- knowledge gates
- Ilia character information
- `PLAYER/link.json`
- `RELATIONSHIPS/relationships.json`
- `MEMORY/relationship_history.md`
- `MEMORY/important_dialogue.md`
- `MEMORY/promises_and_secrets.md`
- relevant `STATE/` records
- relevant session history

After a meaningful change, update relationship state, character state, memories, important dialogue/history, events, current state, and any quest/canon/divergence records affected by the scene.

## Example: Ilia memory restoration

Before the event, retrieve the relevant canon chapter, Ilia knowledge/state, Link's state, relationship history, important dialogue, promises/secrets, item progression, current inventory, quest state, and world state.

After the event, preserve the exact consequences: Ilia's memory state, her relationship with Link, what she now remembers, what she does not remember, what Link said/did, the Horse Call/item progression, canon progression, and any player-created divergence.

## Example: Dungeon progression

Read the relevant chapter and item/progression material, then current world, inventory, quest, canon, Link, character, and session state. After progression, update the corresponding item, quest, world, canon, event, memory, and divergence stores.

## Player agency rule

The AI may control the world and NPCs, but not Link.

The AI must never:
- put words in Link's mouth without permission;
- decide Link's internal thoughts or feelings;
- make Link choose an action;
- make Link fall in love, forgive, hate, promise, or reveal something without player input;
- use canon Link's personality as a substitute for the player's decisions.

The AI may describe consequences of what the player actually chooses.

## Canon rule

The campaign begins two in-world days before the Twilight takeover/invasion reaches Ordon. Twilight Princess canon chronology should be followed closely. Mandatory canon checkpoints remain mandatory unless the player creates a genuine divergence that makes them impossible; in that case, record the divergence and its consequences instead of silently forcing the original sequence back into existence.

## File discovery rule

The manifest is not a reason to ask the player for paths. It is a map for the AI.

If the AI needs information and the relevant path is not explicitly listed here, it must inspect the repository and discover the appropriate file itself before asking the player for help. If a new campaign-support file is created, add it to this manifest immediately.

## Known campaign infrastructure at time of manifest update

```text
CAMPAIGN/
├── BOOTSTRAP.md
├── MANIFEST.md
└── GM_PROTOCOL.md

CANON/
├── canon_rules.md
├── chapter_guides.md
├── knowledge_gates.md
├── characters_major_minor.md
├── items_and_progression.md
└── optional_content.md

MEMORY/
├── character_development.md
├── important_dialogue.md
├── knowledge_state.json
├── major_events.md
├── promises_and_secrets.md
└── relationship_history.md

PLAYER/
└── link.json

RELATIONSHIPS/
└── relationships.json

REVIEW/
└── [inspect repository for all applicable review files]

SESSIONS/
└── [inspect repository for all applicable session files]

STATE/
├── canon_status.json
├── characters.json
├── current.json
├── current_scene.json
├── divergences.json
├── events.json
├── initial_relationships.json
├── inventory.json
├── memories.json
├── quest_state.json
├── quests.json
├── relationships.json
├── saves.json
├── schema.md
└── world.json

AI_RULES.md
```

The listed files above are the campaign-support files currently confirmed from the campaign architecture. `REVIEW/` and `SESSIONS/` are intentionally repository-discovery directories because their contents may grow as the campaign progresses.

This manifest does not claim that unrelated game/source/project files cannot exist elsewhere in the repository.
