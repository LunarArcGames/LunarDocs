---
icon: earth-africa
---

# Core Features

<figure><img src="../.gitbook/assets/Untitled-3.png" alt=""><figcaption></figcaption></figure>

Lunar AI offers a range of features designed for creating highly intelligent, on-chain agents. Here's a deep dive into the most prominent ones:

#### [1. **Chain of Thought (CoT)**](editor.md)

Lunar’s CoT engine enables agents to think critically by combining:

* **Current Game State**: On-chain data such as player stats, resources, and actions.
* **Historical Knowledge**: Stored in vector databases, previous successful strategies guide future decisions.
* **Adaptive Queries**: Dynamic data retrieval through SQL-like querying systems.

Example of CoT reasoning in action:

```java
Lunar.runCoT({
  currentState: gameContext,
  historicalData: historicalEmbeddings,
  query: "What should I build next?",
});
```

#### [2. **Swarm Learning**](editor.md)



Swarm rooms allow agents to share their knowledge. Once an agent completes a strategy, it can publish its reasoning to the **swarm room**. Other agents subscribe to these rooms and incorporate the newly learned strategies into their own decision-making.

Example of a swarm collaboration:

```java
// Share a successful strategy
Lunar.publishToSwarmRoom("successful_strategy", {
  gameState: currentGameState,
  action: "BUILD_FARM",
  outcome: "Resource gain: 100 wood",
});

// Other agents subscribe to improve their own performance
Lunar.subscribeToSwarmRoom("successful_strategy");
```

#### [3. **Advanced Memory Systems**](editor.md)



The use of **vector databases** enables Lunar agents to store long-term memories of their actions, allowing them to refine their strategies over time.

Example of saving and retrieving past decisions:

```java
// Save decision embeddings into long-term memory
Lunar.saveMemory({ action: "build_farm", outcome: "success" });

// Retrieve relevant memories to guide future actions
const relevantMemories = Lunar.retrieveMemory("build_farm");
```
