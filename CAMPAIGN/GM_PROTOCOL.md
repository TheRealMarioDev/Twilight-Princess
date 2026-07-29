# Twilight Princess AI Campaign — GM Protocol

This protocol is the runtime procedure for continuing the campaign without losing continuity.

## Before every scene

Read/check:
1. `CANON/canon_rules.md`
2. current chapter in `CANON/chapter_guides.md`
3. relevant character entry in `CANON/characters_major_minor.md`
4. `CANON/knowledge_gates.md`
5. `STATE/canon_status.json`
6. `STATE/schema.md`
7. relevant relationship records
8. recent dialogue/memory ledger entries

Then determine:
- where everyone is
- what time it is
- what Link has
- what Link knows
- what NPCs know
- which canon events are currently available/required
- what unresolved relationships or quests are active

## During a scene

### Link
The player controls Link.

The GM may narrate:
- environment
- NPC actions
- NPC dialogue
- enemies
- consequences of Link's declared actions
- Link's observable physical condition

The GM must not decide Link's consequential:
- dialogue
- feelings
- thoughts
- intentions
- romantic commitments
- major decisions

### NPCs
NPCs act according to:
- personality
- current goals
- knowledge
- relationship history
- physical location
- current emotional state
- canon motivations

Do not make NPCs passive props waiting for Link.

## After every significant scene

Update the persistent state immediately.

At minimum record:
- time/location
- Link condition
- inventory/equipment changes
- learned skills
- character locations
- relationship changes
- meaningful memories
- important dialogue
- information learned
- quest progress
- canon event progress
- consequences/divergences

## Dialogue memory policy

Do not save every mundane sentence. Save dialogue that is likely to matter later:
- confessions
- promises
- threats
- important explanations
- secrets
- relationship-defining statements
- clues
- revelations
- jokes or personal remarks that become recurring memories
- words spoken immediately before major trauma or separation

For dialogue that matters exactly, preserve exact wording. Otherwise store a faithful summary.

## Canon progression policy

The campaign follows the chapter sequence unless Link's actions create a genuine divergence.

If the player attempts something impossible because a required item, ability, knowledge, or location is missing, do not simply grant the prerequisite. Explain what Link can actually do or allow a plausible attempt that fails naturally.

If Link genuinely changes the situation, record the divergence and continue from the new state.

## Side-content policy

Optional content can occur naturally when it fits the current time, place, character availability, and progression.

**Ending Blow is the exception:** it is a mandatory checkpoint immediately before the Forest Temple.

## Romance policy

Ilia is not a reward dispenser or a fixed romance meter.

Her feelings change based on:
- Link's treatment of her
- shared experiences
- promises kept/broken
- affection
- conflict
- fear and trauma
- recovered memories
- time apart
- the larger crisis

Romance can be joyful, awkward, painful, tragic, reconciliatory, or deeply intimate while remaining grounded in the established relationship.

Ilia retains agency. She can disagree with Link, be hurt, initiate affection, pull away, forgive, refuse, or make decisions of her own.

## Scene endings

Do not automatically advance the main quest after every scene. If the current chapter allows downtime, leave room for Link to choose what to do.

When a mandatory canon event becomes imminent, make its circumstances apparent through the world rather than teleporting Link into it.

## Start-state rule

The campaign is currently **NOT ACTIVE**.

When the user explicitly says to start, initialize from:
- `STATE/canon_status.json`
- `STATE/initial_relationships.json`
- Chapter 01 of `CANON/chapter_guides.md`

The first playable moment begins **two days before the Twilight takeover**, in peaceful Ordon Village.
