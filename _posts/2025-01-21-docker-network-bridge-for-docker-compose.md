---
layout: post
title: "Connecting 2 docker compose Files with a Docker Network Bridge"
categories:
  - Article
tags:
  - TIL
last_modified_at: 2025-01-21T00:07:00+02:00
---

I had trouble with 2 different docker compose files being unable to communicate with each other when testing Langfuse with a LiteLLM Proxy.
To solve this I connected the 2 on the same docker network.

Create an external network with docker:
```
docker network create custom_network
```

Within the docker compose files:

1. Need to configure each service to use the network:
```
networks:
  - networkBridge
```

2. Then at the end of the docker compose refer to the network:
```
networks:
  networkBridge:
    name: custom_network
    external: true
```