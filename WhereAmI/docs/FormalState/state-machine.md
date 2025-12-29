# State Machine - формальные таблицы переходов + ссылки

## Game State Transitions

| Current State | Event / Trigger | Condition | Next State | Notes |
|--------------|----------------|-----------|------------|-------|
| GameCreated | CreateLobby | Host assigned | Lobby | Game initialized |
| Lobby | StartGame | Min players reached | GameInProgress | Settings locked |
| GameInProgress | AllRoundsFinished | — | GameFinished | Final scoring |
| GameFinished | — | — | — | Terminal |

## Round State Transitions

| Current State | Event / Trigger | Condition | Next State | Notes |
|--------------|----------------|-----------|------------|-------|
| RoundInit | InitCompleted | — | CardsDistribution | Setup round |
| CardsDistribution | CardsViewed | All confirmed | RoundActive | Cards immutable |
| RoundActive | ResolutionTriggered | — | RoundResolution | |
| RoundResolution | ResolutionCompleted | — | RoundFinished | |
| RoundFinished | NextRound | More rounds | RoundInit | |
| RoundFinished | EndGame | No rounds | GameFinished | |

## Phase Transitions (RoundActive)

| Current Phase | Trigger | Actor | Condition | Next Phase |
|---------------|---------|-------|-----------|------------|
| Questioning | TimerExpired | System | — | Voting |
| Questioning | EarlyVoteRequested | Any | — | Voting |
| Questioning | SpyGuessRequested | Spy | — | SpyGuessing |
| Voting | VotingCompleted | System | Consensus | Resolution |
| Voting | VotingCompleted | System | No consensus | Questioning |
| SpyGuessing | GuessSubmitted | Spy | Any | Resolution |

## Diagrams

- [Game Flow Diagram](FormalState/diagrams/game-flow.mermaid)
- [Round Flow Diagram](FormalState/diagrams/round-flow.mermaid)
