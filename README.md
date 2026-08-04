# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process

## Aim

To identify a real-world sequential decision-making problem and represent it formally as a Markov Decision Process by defining its states, actions, rewards, transitions, and Python representation.

---

## Problem Statement

### Problem Description

A self-driving delivery robot is used to deliver medicines and other items inside a hospital. The robot must travel from the hospital pharmacy to a specific patient room while avoiding obstacles such as people, medical equipment, and blocked paths.

At each location, the robot has to make a decision about which direction to move. The robot receives a positive reward when it reaches the destination and negative rewards for taking longer paths, hitting obstacles, or making unnecessary movements.

Since the robot makes decisions sequentially and each action affects its next state, the problem can be represented as a Markov Decision Process (MDP).

---

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

---

## State Space

The state represents the current location of the delivery robot inside the hospital.

For simplicity, the hospital is represented using a small grid.

$$
S = \{
S_1, S_2, S_3, S_4, S_5, S_6
\}
$$

Where:

- $S_1$ = Pharmacy
- $S_2$ = Main Corridor
- $S_3$ = Reception Area
- $S_4$ = Emergency Corridor
- $S_5$ = Patient Room Corridor
- $S_6$ = Patient Room (Destination)

The robot starts from $S_1$ and its goal is to reach $S_6$.

---

## Sample State

A sample state is:

$$
S_2 = \text{Main Corridor}
$$

This means that the robot is currently located in the main corridor of the hospital.

---

## Action Space

The robot can perform the following actions:

$$
A = \{
\text{Forward},
\text{Left},
\text{Right},
\text{Stop}
\}
$$

Where:

- **Forward** = Move forward
- **Left** = Turn and move left
- **Right** = Turn and move right
- **Stop** = Stop at the current location

---

## Sample Action

A sample action is:

$$
A = \text{Forward}
$$

This means that the robot chooses to move forward from its current location.

---

## Transition Probability

The transition probability represents the probability of moving from the current state to the next state after taking an action.

The general form is:

$$
P(s'|s,a)
$$

For example, if the robot is at the Main Corridor ($S_2$) and chooses the **Forward** action, it may move to the Patient Room Corridor ($S_5$).

For example:

$$
P(S_5|S_2,\text{Forward}) = 0.9
$$

This means there is a 90% probability that the robot reaches $S_5$ after choosing Forward from $S_2$.

The remaining probability may represent unexpected obstacles or movement failure.

---

## Reward Function

The reward function provides feedback to the robot for each action.

$$
R(s,a,s')
$$

The rewards are defined as follows:

| Situation | Reward |
|---|---:|
| Reaching the patient room | +100 |
| Moving to a normal location | -1 |
| Taking a longer/unnecessary path | -5 |
| Hitting an obstacle | -50 |
| Stopping unnecessarily | -2 |

The robot tries to maximize its total reward while reaching the destination safely.

---

## Discount Factor

The discount factor $\gamma$ determines how much importance the robot gives to future rewards.

For this problem:

$$
\gamma = 0.9
$$

A value of 0.9 means that future rewards are important, but immediate rewards have slightly higher importance.

---

## Graphical Representation

The MDP can be represented as a directed graph where:

- States are represented as nodes.
- Actions are represented as arrows.
- Rewards are written on the transitions.
- Transition probabilities are shown on the arrows.

Example:

```text
        Forward
S1 ----------------> S2
 |                   |
 | Right             | Forward
 |                   |
 v                   v
S3 ----------------> S5
        Right         |
                      | Forward
                      v
                     S6
                (Destination)
---
```
## Python Representation

```
# Representation of Hospital Delivery Robot as an MDP

states = {
    "S1": "Pharmacy",
    "S2": "Main Corridor",
    "S3": "Reception Area",
    "S4": "Emergency Corridor",
    "S5": "Patient Room Corridor",
    "S6": "Patient Room"
}

actions = {
    "S1": ["Forward", "Right"],
    "S2": ["Forward", "Left", "Right"],
    "S3": ["Forward", "Right"],
    "S4": ["Forward", "Left"],
    "S5": ["Forward", "Left", "Right"],
    "S6": ["Stop"]
}

transitions = {
    ("S1", "Forward"): {"S2": 0.9, "S3": 0.1},
    ("S2", "Forward"): {"S5": 0.9, "S4": 0.1},
    ("S3", "Forward"): {"S4": 0.9, "S2": 0.1},
    ("S4", "Forward"): {"S5": 0.9, "S4": 0.1},
    ("S5", "Forward"): {"S6": 0.9, "S5": 0.1}
}

rewards = {
    ("S1", "Forward", "S2"): -1,
    ("S2", "Forward", "S5"): -1,
    ("S3", "Forward", "S4"): -1,
    ("S4", "Forward", "S5"): -1,
    ("S5", "Forward", "S6"): 100
}

gamma = 0.9

print("States:", states)
print("Actions:", actions)
print("Transition Probabilities:", transitions)
print("Rewards:", rewards)
print("Discount Factor:", gamma)
```



Use Python dictionaries to represent the MDP.


```python
# MDP Representation using Python
# print("Name: Suresh S")
# print("Register Number: 212223040215")

```
---
## Output

<img width="895" height="403" alt="Screenshot 2026-08-04 155428" src="https://github.com/user-attachments/assets/74793b2d-b68f-4ed8-ad76-6332c527e735" />



---

## Result

The hospital delivery robot problem was successfully represented as a Markov Decision Process by defining its state space, action space, transition probabilities, reward function, and discount factor. The MDP representation can be used to determine an optimal sequence of actions that enables the robot to reach the patient room safely and efficiently.


---

