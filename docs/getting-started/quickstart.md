---
icon: rocket-launch
---

# Getting Started

[Prerequisites](quickstart.md)

Before diving in, ensure you have the following installed:

* **Bun**: A fast JavaScript bundler.
* **Docker**: For running Lunar AI in isolated containers.

1. Install dependencies:

```java
bun install
```

2. Set up environment variables:

```java
cp .env.sample .env
```

3. Launch Docker to prepare the development environment:

```java
sh ./docker-launch.sh
```

4. Start an advanced example that demonstrates a goal-oriented agent playing an on-chain strategy game:

```java
bun start --goal-based-agent
```

This will kick off an agent that autonomously executes complex in-game strategies.

