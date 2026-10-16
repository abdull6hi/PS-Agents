# ICS 3202: Artificial Intelligence, Practical Exercise 3

## Designing a searching agent

Group members:

- Abdullahi Osman - 152386
- Adan Siba - 191224
- Daniel Ndumbe - 190374

Agent: Self-driving trailer
Environment: Kenya's highway network
Initial state: Nairobi
Goal state: Kisumu

---

## 1. Introduction

This exercise looks at a self-driving trailer travelling from Nairobi to Kisumu. We describe the agent and its environment with the PEAS framework, model the road network as a graph, and search that graph for the shortest route.

---

## 2. Question 1: PEAS framework

| PEAS element | Description |
|---|---|
| Performance measure | Reach Kisumu safely, avoid collisions and cargo damage, obey traffic rules, and keep distance, fuel use, and delivery time low. |
| Environment | Kenyan roads, other vehicles, pedestrians, road signs, junctions, weather, traffic, and roadworks. |
| Actuators | Steering, accelerator, brakes, gears, indicators, lights, horn, and wipers. |
| Sensors | Cameras, radar, GPS, speedometer, LiDAR, motion sensors, and digital maps. |

### 2.1 Environment classification

- Fully vs partially observable: partially observable. The sensors cannot show the trailer everything on the road at all times, for example a vehicle around a bend or a pothole under standing water.
- Deterministic vs stochastic: stochastic. Other drivers, accidents, and sudden road conditions can change what an action leads to, and the trailer cannot control them.
- Episodic vs sequential: sequential. Each decision changes the trailer's later states and the actions open to it.
- Static vs dynamic: dynamic. Traffic, road conditions, and weather can change while the agent is still deciding what to do.
- Single-agent vs multi-agent: multi-agent. Drivers and pedestrians act in the same environment and affect the trailer's decisions.

---

## 3. Question 2: Road network and graph

We represent the selected towns and roads as a graph. Each town is a node, and each road is an edge labelled with its distance in kilometres. Real roads are two-way, so each road stands for two directed edges with the same cost. The diagram below draws only the direction from Nairobi towards Kisumu, since the return edges never lead towards the goal.

### 3.1 Problem formulation and search

- Initial state: Nairobi
- Goal state: Kisumu
- State space: the towns in the road network
- Actions: driving along a road from the current town to a connected town
- Goal test: is the current town Kisumu?
- Path cost function: total road distance from Nairobi to the current town
- Transition model: driving along a chosen road takes the trailer to the town at its other end
- Optimal solution: the route from Nairobi to Kisumu with the smallest total distance

### 3.2 Abstraction of the road network

We simplify the road network by treating towns as states and direct roads as edges. Road curvature, lanes, traffic, and weather do not change which route is shortest, so the model leaves them out and keeps only the towns and the distances between them.

---

## 4. Directed graph and search tree

### 4.1 Directed graph

<img width="600" height="701" alt="Graph1 drawio" src="https://github.com/user-attachments/assets/61a9d12b-5b7e-416a-80de-524e0a21248e" />


### 4.2 Search tree

The search tree starts at Nairobi and expands every route towards Kisumu. Each edge shows its distance in km, and each leaf shows the total path cost of that route.

<img width="456" height="782" alt="Graph2 drawio" src="https://github.com/user-attachments/assets/f4de2f38-fd92-4977-8002-042bcc2d15d8" />


## 5. Comparing routes and finding the optimal path

### 5.1 Route comparison

| Route | Path | Calculation | Total distance (km) |
|---|---|---|---|
| 1 | Nairobi → Naivasha → Nakuru → Molo → Kericho → Kisumu | 88 + 71 + 47 + 60 + 83 | **349** |
| 2 | Nairobi → Narok → Bomet → Kisii → Kisumu | 142 + 86 + 68 + 83 | 379 |
| 3 | Nairobi → Naivasha → Nakuru → Eldoret → Kapsabet → Kericho → Kisumu | 88 + 71 + 156 + 48 + 74 + 83 | 520 |

### 5.2 Distance for the optimal path

| Segment | Distance (km) |
|---|---|
| d(Nairobi, Naivasha) | 88 |
| d(Naivasha, Nakuru) | 71 |
| d(Nakuru, Molo) | 47 |
| d(Molo, Kericho) | 60 |
| d(Kericho, Kisumu) | 83 |

Path cost = 88 + 71 + 47 + 60 + 83 = 349 km

### 5.3 Optimal path

Route 1 (Nairobi → Naivasha → Nakuru → Molo → Kericho → Kisumu) is the optimal route. At 349 km it has the lowest path cost of the three routes, 30 km shorter than Route 2 and 171 km shorter than Route 3.

---

## 6. Evidence of groupwork

<img width="1600" height="900" alt="WhatsApp Image 2026-10-16 at 13 57 48" src="https://github.com/user-attachments/assets/ad871fe9-9bb3-49a5-b896-87a03da2de84" />
