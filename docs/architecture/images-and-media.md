---
icon: lightbulb
---

# Advanced Workflow

#### [Initialization & Setup](images-and-media.md)



1. **Start Lunar AI Agent**:

```java
bun start --advanced --agent-type "strategy-agent"
```

2. **Load Game Context**:

```java
const gameContext = {
  playerID: "0xabcdef1234567890",
  resources: { gold: 500, wood: 100 },
  turn: 7,
  availableActions: ["build", "attack", "trade"],
};

Lunar.loadContext(gameContext);
```

#### Goal Execution:



```java
const goal = {
  description: "Build a fortress to protect resources",
  subgoals: [
    { action: "GATHER_RESOURCES", conditions: { wood: 200, stone: 100 } },
    { action: "BUILD_FORTRESS", conditions: { location: [50, 75], resourcesSpent: { wood: 150, stone: 100 } } },
  ],
};

Lunar.executeGoal(goal);
```

#### Dynamic Monitoring:



```java
// Monitoring agent's actions and reasoning
Lunar.on("action:start", (data) => {
  console.log(`🔄 Agent action started: ${data.action}`);
});

Lunar.on("action:complete", (data) => {
  console.log(`✅ Action completed: ${data.action.type} with result: ${data.result}`);
});
```
