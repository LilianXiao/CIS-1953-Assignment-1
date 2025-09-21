# CIS 1953 Unreal Engine HW

# Assignment 1 notes:
**Issues I've been working through**
* For the longest time was struggling with debugging hit events (projectile collisions were either behaving abnormally or failing to spawn, despite having ignore actor, so used overlap events instead and that fixed the issue...this kinda goes hand in hand with my attempt at purely physics-based projectiles, which weren't working due to this issue, so I just used projectile movement
* Getting this bug: Blueprint Runtime Error: "Accessed None trying to read (real) property K2Node_DynamicCast_AsBP_First_Person_Character in not an UClass". Node:  SpawnActor BP Moving Target Graph:  EventGraph Function:  Execute Ubergraph BP Target Spawner Blueprint:  BP_TargetSpawner
* It's absolutely to do with this in my BP_TargetSpawner:
<img width="826" height="175" alt="image" src="https://github.com/user-attachments/assets/90bb98d8-e658-43b5-a561-ec61d780f565" />

* It doesn't actually affect any functionality in the game, so I assume this could be some nuanced casting complication?
* projectile refuses to destroy when colliding with environment props.  This includes objs I imported myself and also basic unreal primitives, but I've set basically all of them to blockall in collision presets and also checked generate overlap events in case, and the projectiles do not destroy.
See this in BP_Projectile:
<img width="598" height="223" alt="image" src="https://github.com/user-attachments/assets/d519e863-d1ed-40fe-80e5-6ce79054e84a" />

* Actually just fixed the strange collision behavior mentioned above:
<img width="702" height="204" alt="image" src="https://github.com/user-attachments/assets/a8604989-18e6-43ae-8645-4cfedb8a60a6" />

* Since I wanted to avoid the projectile colliding and destroying on the invisible target box while simultaneously keeping overlap -> destroy behavior for other things like moving targets + environment, this somehow solves the issue.  Originally I'd just cast it to my target spawner and destroy actor if cast failed, but while this avoided the first issue, the projectiles still wouldn't destroy upon colliding with anything.


* The reason I made the cast to my trigger box bp was because the projectiles were destroying on the invisible box, and once I did this it prevented this behavior.

**General notes:**
* I decided to have some fun with the environment and imported some objs I modeled, including the pillars, the target prisms (kinda looks like the prisms from the sims haha), and the hornet model (she is the indicator for the trigger box :D)
