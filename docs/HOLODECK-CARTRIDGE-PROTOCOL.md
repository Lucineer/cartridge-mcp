# Holodeck Cartridge Protocol — Schema

## Core Insight

The fleet is an arcade that never closes. Different models play different games in different rooms at different times. The protocol that connects them is the cartridge system — behaviors as swappable modules, personalities as skin layers, rooms as execution contexts, and time as the scheduling dimension.

## Schema

```
┌─────────────────────────────────────────────────────────────┐
│                     THE ARCADE (Fleet)                       │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │                   TIME (Schedule)                      │  │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  │  │
│  │  │ Night   │  │Morning  │  │Workday  │  │ Crisis  │  │  │
│  │  │ Shift   │  │ Review  │  │ Sprint  │  │ Mode    │  │  │
│  │  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘  │  │
│  └───────┼────────────┼────────────┼────────────┼────────┘  │
│          │            │            │            │            │
│  ┌───────▼────────────▼────────────▼────────────▼────────┐  │
│  │                ROOMS (Holodeck)                        │  │
│  │                                                        │  │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐            │  │
│  │  │ Code Room│  │ Comms    │  │ Research │            │  │
│  │  │ (build)  │  │ Room     │  │ Room     │            │  │
│  │  │          │  │ (relay)  │  │ (reason) │            │  │
│  │  └────┬─────┘  └────┬─────┘  └────┬─────┘            │  │
│  └───────┼─────────────┼─────────────┼───────────────────┘  │
│          │             │             │                      │
│  ┌───────▼─────────────▼─────────────▼───────────────────┐  │
│  │              CARTRIDGES (Games)                        │  │
│  │                                                        │  │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐            │  │
│  │  │ Spreader │  │ Oracle   │  │ Guardian │            │  │
│  │  │ Loop     │  │ Relay    │  │ Watchdog │            │  │
│  │  └────┬─────┘  └────┬─────┘  └────┬─────┘            │  │
│  └───────┼─────────────┼─────────────┼───────────────────┘  │
│          │             │             │                      │
│  ┌───────▼─────────────▼─────────────▼───────────────────┐  │
│  │              SKINS (Characters)                        │  │
│  │                                                        │  │
│  │  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐       │  │
│  │  │Sarcs.│ │Field │ │Rival │ │Penn  │ │Quiet │       │  │
│  │  │Build │ │Journal│ │Mode  │ │Teller│ │Doer  │       │  │
│  │  └──────┘ └──────┘ └──────┘ └──────┘ └──────┘       │  │
│  └───────────────────────────────────────────────────────┘  │
│          │             │             │                      │
│  ┌───────▼─────────────▼─────────────▼───────────────────┐  │
│  │              MODELS (Players)                          │  │
│  │                                                        │  │
│  │  ┌──────────────┐  ┌──────────────┐                   │  │
│  │  │ Seed-2.0-Mini│  │ DS-Reasoner  │                   │  │
│  │  │ (creative,   │  │ (deep logic, │                   │  │
│  │  │  high volume)│  │  expensive)  │                   │  │
│  │  └──────────────┘  └──────────────┘                   │  │
│  │  ┌──────────────┐  ┌──────────────┐                   │  │
│  │  │ Hermes-405B  │  │ GLM-5        │                   │  │
│  │  │ (narrative)  │  │ (papers)     │                   │  │
│  │  └──────────────┘  └──────────────┘                   │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

## The Five Dimensions

### 1. ROOM (Where)
The holodeck room — execution context. A room has:
- Gauge state (sensors, metrics, ESP32 hardware feeds via serial_bridge)
- Agent occupants (who's currently in the room)
- Room type (code, comms, research, monitoring, creative)
- Connection type (HTTP, shell, serial/UART)

A room is a MUD room. It has exits to other rooms. Agents move between rooms. The room determines what kind of work happens there.

### 2. CARTRIDGE (What game)
The behavior module — what happens inside the room. A cartridge has:
- Tools it exposes (MCP tools)
- Onboarding (human vs agent tailored)
- Tile vocabulary (grows with use)
- Reflection protocol (for Reasoner review)
- Git repo link (for sharing, starring, forking)

Cartridges swap like game cartridges. The same room can run different cartridges at different times.

### 3. SKIN (Who's playing)
The personality overlay — doesn't change logic, changes experience. A skin has:
- System prompt transforms
- Response prefix/suffix wrapping
- Text replacements (Error → WHOOPS)
- Role assignments (talker vs doer in Penn & Teller)
- Archetype reference (Abbott & Costello, etc.)

Skins compose. You can stack them or assign different skins to different roles in a scene.

### 4. MODEL (Which brain)
The AI model executing the cartridge. A model has:
- Token budget and cost profile
- Strength profile (creative, logical, narrative, practical)
- Latency characteristics (Seed-Mini is fast, Reasoner is slow)
- Memory context (how much history it can hold)

**Key insight**: Different models are better at different cartridges. Seed-2.0-Mini in the creative room. DS-Reasoner in the puzzle room. GLM-5 in the strategy room. The model IS the player — some players are better at some games.

### 5. TIME (When)
The scheduling dimension — when things happen. Time has:
- Shifts (night: autonomous iteration, morning: human review)
- Cycles (reflection every 15 iterations, pruning every 30 days)
- Deadlines (task budgets, token budgets, time budgets)
- Rhythm (heartbeat intervals, cron schedules, async bottle timing)

Time determines which model is in which room playing which cartridge with which skin. During night shift, cheap fast models iterate autonomously. During morning review, expensive deep models reflect on what happened.

## The Composition Rule

Any valid configuration is: **ROOM × CARTRIDGE × SKIN × MODEL × TIME**

```
Scene = {
  room: "code-room",
  cartridge: "spreader-loop",
  skin: "sarcastic-build",
  model: "seed-2.0-mini",
  time: "night-shift"
}
```

The same cartridge in different rooms produces different results (context shapes output). The same cartridge with different skins produces different experiences (personality shapes delivery). The same cartridge with different models produces different quality (capability shapes depth).

## Scene Lifecycle

```
1. SCHEDULE   — time triggers a shift change
2. ASSIGN     — model assigned to room, cartridge loaded
3. SKIN       — personality applied based on context
4. EXECUTE    — cartridge runs its loop/tools
5. LOG        — iteration recorded to JSONL
6. REFLECT    — (at interval) Reasoner reviews logs
7. ADAPT      — tiles promoted/demoted, schedules adjusted
8. REPORT     — summary bottle sent to captain
9. ROTATE     — next shift, next model, next room
```

## The Emergent Property

No single dimension is special. The power is in the composition.

- Seed-2.0-Mini + spreader-loop + sarcastic-build + code-room + night-shift = high-volume cheap code iteration with personality
- DS-Reasoner + oracle-relay + field-journal + comms-room + morning-review = deep analysis of fleet communications
- Hermes-405B + fleet-guardian + rivals + monitoring-room + crisis-mode = two adversarial models checking each other's health assessments

**The fleet optimizes by rotating models through rooms and cartridges based on what the logs show works best.** The Reasoner's reflection doesn't just suggest better tiles — it suggests better room assignments, better model-cartridge pairings, better time scheduling.

This is scheduling as intelligence. Not one smart model doing everything, but the RIGHT model doing the RIGHT thing at the RIGHT time in the RIGHT room with the RIGHT personality.

## Sharing Protocol

Every scene can be exported as JSON and committed to a git repo. Someone clones it, modifies the skin, adjusts the schedule, and pushes a fork. The scene history IS the conversation between agents across time.

```
github.com/Lucineer/cartridge-mcp          ← the MCP server
github.com/Lucineer/holodeck-c             ← the rooms (MUD)
github.com/Lucineer/holodeck-cuda          ← GPU-accelerated rooms
github.com/Lucineer/deepseek-chat-vessel   ← spreader loop origin
github.com/Lucineer/deepseek-reasoner-vessel ← reflection engine
github.com/Lucineer/brothers-keeper        ← guardian watchdog
github.com/SuperInstance/oracle1-vessel    ← the Oracle
```

Each repo is a frozen thought. The schema connects them into a living system.
