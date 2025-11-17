# GAME_PROGRAM-EX-7
## AI Roaming and Player Chasing Using Behavior Trees, Blackboard, and AI Perception

## Aim
To create an AI character in Unreal Engine that roams randomly within a NavMesh area and chases the player when they enter a detection range, using Behavior Trees, Blackboard, and AI Perception.

## Steps

### 1. Setup Navigation
- Add a **NavMeshBoundsVolume** to the level.
- Resize it to cover the entire roamable area.
- Press **P** to ensure the navigation mesh appears (green area).

### 2. Create the AI Character
- Create a Character Blueprint (e.g., **BP_AIEnemy**).
- Assign a skeletal mesh and animations as needed.
- Create an **AI Controller Blueprint** (e.g., **BP_AIController**).
- Assign this AI Controller to the AI character inside Class Defaults.

### 3. Enable AI Perception
- Open **BP_AIController**.
- Add an **AIPerception** component.
- Add a **Sight Sense** and configure:
  - Sight radius
  - Lose sight radius
  - Peripheral vision angle
- Bind **OnPerceptionUpdated**.
- Update Blackboard values from perception:
  - **PlayerActor** (Object)
  - **CanSeePlayer** (Bool)

### 4. Create Blackboard
Create a Blackboard asset with the following keys:

- **TargetLocation** (Vector)
- **PlayerActor** (Object)
- **CanSeePlayer** (Bool)

### 5. Create Behavior Tree (BT_AI)
The behavior tree should perform two actions:

1. **Chase Player**  
   - If **CanSeePlayer = true**, move to **PlayerActor**.

2. **Random Roam**  
   - If **CanSeePlayer = false**, find a random location and move there.


### 6. Custom Task: Find Random Location
Create a **BTTask_BlueprintBase**.

In the task:
- Use  
  `UNavigationSystemV1::GetRandomReachablePointInRadius()`
- Store the result in the **TargetLocation** Blackboard key.

### 7. Testing the AI
- Place the AI character in the level.
- Assign:
  - **BP_AIController**
  - **BT_AI** (Behavior Tree)
- Press Play:
  - AI roams when the player is not detected.
  - AI chases the player when sighted.
  - AI resumes roaming after losing sight.

## Output
<img width="1038" height="527" alt="image" src="https://github.com/user-attachments/assets/ef0465aa-1933-4d40-ae19-c069ef7d4089" />
<img width="1027" height="427" alt="image" src="https://github.com/user-attachments/assets/32426d1f-b94b-41e7-936b-1bf56e37ab2f" />
<img width="1030" height="401" alt="image" src="https://github.com/user-attachments/assets/65235676-4d0f-4fca-a757-bbc7591007dd" />


The AI roams randomly within the defined navigation area and switches to chase mode when the player enters its sight range.

## Result
The AI character successfully roams in the NavMesh area and chases the player when detected. When the player is no longer visible, it returns to its roaming behavior.
