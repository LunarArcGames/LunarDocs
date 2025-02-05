---
icon: wrench
---

# How Lunar AI Works

Lunar AI is built with **flexibility** and **modularity** at its core. You can customize and extend its behavior for any on-chain game or decentralized application by defining **Context**, **Actions**, and **Goals**.

<figure><img src="../docs/.gitbook/assets/Landing%20(1).png" alt=""><figcaption></figcaption></figure>

#### [1. Defining Game Context](publish-your-docs.md)

Context is the foundation of any agent's decision-making process. It describes the game state, rules, and available actions. In Lunar AI, context is represented as a structured **JSON** object.

Example context for a decentralized strategy game:

```java
{
  "gameState": {
    "playerID": "0xabcdef1234567890",
    "resources": {
      "gold": 500,
      "wood": 150,
      "stone": 80
    },
    "turn": 5,
    "availableActions": ["build", "attack", "trade"]
  },
  "gameRules": {
    "maxTurns": 20,
    "victoryCondition": "controlCastle"
  }
}
```

This context object allows the agent to understand the current game environment, the player's resources, and the rules it must follow.

#### [2. Registering Complex Actions](../docs.md)

In Lunar AI, actions are the tasks the agent can perform. These actions can be registered with intricate parameters and validation rules, ensuring that the agent always makes **valid** decisions on-chain.

For example, registering an action to build a resource structure:

```java
// Register a complex action to execute a transaction on Solana blockchain
Lunar.registerAction(
  "BUILD_STRUCTURE",
  solanaBuildAction,
  {
    description: "Build a resource structure on the Solana blockchain",
    example: {
      contractAddress: "0xabcdef1234567890",
      entryPoint: "build",
      calldata: {
        structureType: "farm",
        location: [45, 75],
        resourcesSpent: { wood: 50, stone: 30 },
      },
    },
    validationSchema: Joi.object({
      structureType: Joi.string().valid("farm", "mine", "warehouse").required(),
      location: Joi.array().length(2).items(Joi.number()).required(),
      resourcesSpent: Joi.object({
        wood: Joi.number().min(0).required(),
        stone: Joi.number().min(0).required(),
      }).required(),
    }),
  },
);
```

In this example, we are registering an action that builds a farm in the game world. The action is validated using **Joi** to ensure it is well-formed and meets the game rules.

#### [3. Setting Up Goals and Strategies](publish-your-docs.md)

Goals represent long-term objectives for your agent, which it will attempt to accomplish autonomously. Lunar AI utilizes **Chain of Thought (CoT)** processing, breaking down complex goals into achievable steps.

Example: A goal to gather resources and build a defensive structure:

```java
const goal = {
  description: "Gather resources and build a defensive structure.",
  subgoals: [
    {
      action: "GATHER_RESOURCES",
      conditions: {
        resources: { wood: 100, stone: 50 },
      },
    },
    {
      action: "BUILD_DEFENSE",
      conditions: {
        location: [10, 20],
        resourcesSpent: { wood: 50, stone: 30 },
      },
    },
  ],
};

Lunar.setGoal(goal);
```

The agent will attempt to fulfill this goal by first gathering the required resources, then building the defense. Each subgoal is treated as an individual action that the agent can perform.

#### [4. Advanced Event Handling and Progress Monitoring](publish-your-docs.md)

Lunar AI provides event-driven architecture, allowing you to subscribe to critical actions and monitor the agent's progress in real-time.

```java
// Track agent's reasoning process
Lunar.on("thinking:start", ({ query }) => {
  console.log(`Agent is considering: ${query}`);
});

// Capture when actions are completed
Lunar.on("action:complete", ({ action, result }) => {
  console.log(`Action is taken:`, { action: action.type, result });
});
```

With these events, you can monitor every phase of the agent’s journey, from initial thought processing to final execution.
