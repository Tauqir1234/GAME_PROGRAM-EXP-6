# GAME_PROGRAM-EXP-6  
## AI Random Roam with Chase – Unreal Engine

### **Aim**
To create an AI character in Unreal Engine that roams randomly within a NavMesh area and chases the player when they come within a certain range, using **Behavior Trees**, **Blackboard**, and **AI Perception**.

---

## **Procedure**

### **1. Setup Navigation**
- Add a **NavMeshBoundsVolume** to your level and scale it to cover the roamable area.
- Press **P** to confirm the green navigation area is visible (indicating navigable space).

---

### **2. Create AI Character**
- Create a Blueprint character (e.g., `BP_AIEnemy`) with:
  - A skeletal mesh  
  - An `AIController` class
- Create an AI Controller Blueprint (e.g., `BP_AIController`) and assign it to the character.

---

### **3. Enable AI Perception**
In `BP_AIController`:
- Add an **AIPerception** component.
- Configure a **Sight Sense**:
  - Detection range  
  - Lose-sight range  
  - Peripheral vision angle
- Bind **OnPerceptionUpdated** to update a blackboard value:  
  - `CanSeePlayer` (bool)  
  - `PlayerActor` (object)

---

### **4. Set Up Blackboard**
Create a **Blackboard** with the following keys:

| Key Name       | Type   |
|----------------|--------|
| TargetLocation | Vector |
| PlayerActor    | Object |
| CanSeePlayer   | Bool   |

---

### **5. Create Behavior Tree (`BT_AI`)**

**Structure:**

```
Root
└── Selector
    ├── Sequence (Chase Player)
    │   ├── Blackboard Check: CanSeePlayer == true
    │   └── Move To: PlayerActor
    └── Sequence (Random Roam)
        ├── Task: Find Random Location → TargetLocation
        └── Move To: TargetLocation
```

---

### **6. Custom Task: Find Random Location**

Create a new `BTTask_BlueprintBase`:

Use:

```cpp
UNavigationSystemV1::GetRandomReachablePointInRadius()


---

```
### 7. Test the AI

1. Add a **Player Character** to the level.  
2. Place the **AI Enemy** in the map and assign:
   - Its **AI Controller**
   - Its **Behavior Tree**
3. Press **Play**:
   - The AI **roams randomly** when the player is far.
   - The AI **chases the player** when the player enters its sight range.
## OUTPUT:
<img width="1031" height="731" alt="image" src="https://github.com/user-attachments/assets/e61f241d-da6f-4aad-a732-b47467044694" />
<img width="1032" height="429" alt="image" src="https://github.com/user-attachments/assets/fe4fb30e-0e6b-4681-a08e-3707190f681c" />
<img width="1011" height="384" alt="image" src="https://github.com/user-attachments/assets/4109d7df-6535-4254-8666-3fed0677aede" />

## Result:
The AI character roams randomly within a defined area. When the player enters its sight range, the AI stops roaming and begins to chase the player until the player is out of sight, after which it resumes roaming.
