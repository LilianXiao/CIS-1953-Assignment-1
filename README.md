# CIS 1953 Unreal Engine HW

#Assignment 2 notes:
**Issues I've been working through**
* Been trying to figure out how to modularize everything by making them components.  In the meantime the functionality I have looks pretty spaghetti, though I tried to implement everything that I could
* To make the ui I used widget bps, though I should have used widget components (?)
* Because I haven't figured out components yet, my projectile logic is still built into my first person character.  So I ended up doing my UI updating in there as well.  It works enough for the health + on death functionality, but the ammo is cooked!!!!!!!!!!!!!!  Couldn't use the set timer by event node because I didn't implement these as separate components....will have to tough that out....

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
* You may notice the projectiles colliding and destroying close to the hornet model; this is only due to the weird collision box unreal put on the model, not because of the trigger box or anything else lol

**General notes:**
* I decided to have some fun with the environment and imported some objs I modeled, including the pillars, the target prisms (kinda looks like the prisms from the sims haha), and the hornet model (she is the indicator for the trigger box :D)
