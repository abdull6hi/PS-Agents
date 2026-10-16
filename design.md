# ICS 3202: Artificial Intelligence — Practical Exercise 3

## Designing a Searching Agent

**Group members:**

- Abdullahi Osman - 152386
- Adan Siba - 191224
- Daniel Ndumbe - 190374

**Agent:** Self-driving trailer
**Environment:** Kenya's highway network
**Initial state:** Nairobi
**Goal state:** Kisumu

---

## 1. Introduction

This exercise considers a self-driving trailer travelling from Nairobi to Kisumu. The PEAS framework is used to describe the agent and its environment. The road network is then represented as a graph, and a search method is used to identify the shortest route in the selected network.

---

## 2. Question 1: PEAS Framework

| PEAS element | Description |
|---|---|
| **Performance measure** | Reach Kisumu safely, avoid collisions and cargo damage, obey traffic rules, and reduce distance, fuel use, and delivery time. |
| **Environment** | Kenyan roads, other vehicles, pedestrians, road signs, junctions, weather, traffic, and roadworks. |
| **Actuators** | Steering, accelerator, brakes, gears, indicators, lights, horn, and wipers. |
| **Sensors** | Cameras, radar, GPS, speedometer, LiDAR, motion sensors, and digital maps. |

### 2.1 Agent Environment Classification

- **Fully observable vs partially observable:** The environment is **partially observable**, because the trailer's sensors cannot provide complete information about every aspect of the road environment at all times.
- **Deterministic vs stochastic:** The environment is **stochastic**, because the outcome of an action may be affected by factors beyond the agent's control, such as other drivers, accidents, and unexpected road conditions.
- **Episodic vs sequential:** The environment is **sequential**, because the agent's current decisions affect subsequent states and available actions.
- **Static vs dynamic:** The environment is **dynamic**, because traffic, road, and weather conditions may change while the agent is deciding which action to take.
- **Single-agent vs multi-agent:** The environment is **multi-agent**, because other road users such as drivers and pedestrians also act within the same environment and influence the trailer's decisions.

---

## 3. Question 2: Road Network and Graph

The selected towns and road links are represented as a graph. Each town is a node, and each road is an edge labelled with its distance in kilometres. Roads are two-way in reality, so each road represents two directed edges with the same cost. In the diagram below, only the edge in the direction of travel from Nairobi towards Kisumu is drawn, because the return edges never lead towards the goal.

### 3.1 Problem Formulation and Search

- **Initial state:** Nairobi
- **Goal state:** Kisumu
- **State space:** The towns in the road network
- **Available actions:** Road connections that allow the trailer to travel from its current town to another town
- **Goal test:** Checks whether the current state is Kisumu
- **Path cost function:** Total road distance travelled from Nairobi to the current town
- **Transition model:** Moving along a selected road leads to the connected town
- **Optimal solution:** A valid route from Nairobi to Kisumu with minimum total road distance

### 3.2 Abstraction of the Road Network

- The real-world road network is simplified by representing towns as states and direct road connections as edges.
- Details that do not affect the choice of route, such as road curvature, lanes, traffic, and weather, are left out of the model. Only the towns and the distances between them are kept.

---

## 4. Directed Graph and Search Tree Representation

### 4.1 Directed Graph

<img width="600" height="701" alt="Graph1 drawio" src="https://github.com/user-attachments/assets/61a9d12b-5b7e-416a-80de-524e0a21248e" />


### 4.2 Search Tree

The search tree starts at Nairobi and expands every route towards Kisumu. Each edge is labelled with its distance in km, and each leaf shows the total path cost of that route.

<img width="456" height="782" alt="Graph2 drawio" src="https://github.com/user-attachments/assets/f4de2f38-fd92-4977-8002-042bcc2d15d8" />


## 5. Alternative Routes Comparison and Optimal Path Determination

### 5.1 Route Comparison Table

| Route | Path | Calculation | Total distance (km) |
|---|---|---|---|
| 1 | Nairobi → Naivasha → Nakuru → Molo → Kericho → Kisumu | 88 + 71 + 47 + 60 + 83 | **349** |
| 2 | Nairobi → Narok → Bomet → Kisii → Kisumu | 142 + 86 + 68 + 83 | 379 |
| 3 | Nairobi → Naivasha → Nakuru → Eldoret → Kapsabet → Kericho → Kisumu | 88 + 71 + 156 + 48 + 74 + 83 | 520 |

### 5.2 Distance Calculation for Optimal Path

| Segment | Distance (km) |
|---|---|
| d(Nairobi, Naivasha) | 88 |
| d(Naivasha, Nakuru) | 71 |
| d(Nakuru, Molo) | 47 |
| d(Molo, Kericho) | 60 |
| d(Kericho, Kisumu) | 83 |

Path cost = 88 + 71 + 47 + 60 + 83 = **349 km**

### 5.3 Optimal Path

Based on the path cost function, the optimal route for the searching agent is Route 1 (Nairobi → Naivasha → Nakuru → Molo → Kericho → Kisumu), with a total distance of **349 km**. It has the lowest path cost of the three routes compared.

---

## 6. Evidence of Groupwork

<img width="1600" height="900" alt="WhatsApp Image 2026-10-16 at 13 57 48" src="https://github.com/user-attachments/assets/ad871fe9-9bb3-49a5-b896-87a03da2de84" />
