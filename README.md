<h1>Exp-No 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 
<h3>Name: Shanthosh G          </h3>
<h3>Register Number:  2305003008          </h3>

<H2>Aim:</H2>
<p>
    To solve  Wumpus World Problem using Python demonstrating Inferences from Propositional Logic
</p>

<h2>Problem Description</h2>

<h3>Wumpus World</h3>

The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

**Example Wumpus Map:**

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)


### SAMPLE PROGRAM
```python

# Wumpus World Representation
# This is a python program that uses propositional logic sentences to check which rooms are safe. 
# It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world.
#The logical agent can take four actions: Up, Down, Left and Right.
#These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.

wumpus=[["Save","Breeze","PIT","Breeze"],
        ["Smell","Save","Breeze","Save"],
        ["WUMPUS","GOLD","PIT","Breeze"],
        ["Smell","Save","Breeze","PIT"]]
row=0
column=0
arrow=True
player=True
score=0
while(player):
    choice=input("press u to move up\npress d to move down\npress l to move left\npress r to move right\n")
    if choice == "u":
        if row != 0:
            row-=1
        else:
            print("move denied")
        
        print("current location: ",wumpus[row][column],"\n")
    elif choice == "d" :
        if row!=3:
            row+=1
        else:
            print("move denied")
        
        print("current location: ",wumpus[row][column],"\n")
    elif choice == "l" :
        if column!=0:
            column-=1
        else:
            print("move denied")
        
        print("current location: ",wumpus[row][column],"\n")
    elif choice == "r" :
        if column!=3:
            column+=1
        else:
            print("move denied")
        
        print("current location: ",wumpus[row][column],"\n")
    else:
        print("move denied")

    if wumpus[row][column]=="Smell" and arrow != False:
        arrow_choice=input("do you want to throw an arrow-->\npress y to throw\npress n to save your arrow\n")
        if arrow_choice == "y":
            arrow_throw=input("press u to throw up\npress d to throw down\npress l to throw left\npress r to throw right\n")
            if arrow_throw == "u":
                if wumpus[row-1][column] == "WUMPUS":
                    print("wumpus killed!")
                    score+=1000
                    print("score: ",score)
                    wumpus[row-1][column] = "Save"
                    wumpus[1][0]="Save"
                    wumpus[3][0]="Save"
                else:
                    print("arrow wasted...")
                    score-=10
                    print("score: ",score)
            elif arrow_throw == "d":
                if wumpus[row+1][column] == "WUMPUS":
                    print("wumpus killed!")
                    score+=1000
                    print("score: ",score)
                    wumpus[row+1][column] = "Save"
                    wumpus[1][0]="Save"
                    wumpus[3][0]="Save"
                else:
                    print("arrow wasted...")
                    score-=10
                    print("score: ",score)
            elif arrow_throw == "l":
                if wumpus[row][column-1] == "WUMPUS":
                    print("wumpus killed!")
                    score+=1000
                    print("score: ",score)
                    wumpus[row][column-1] = "Save"
                    wumpus[1][0]="Save"
                    wumpus[3][0]="Save"
                else:
                    print("arrow wasted...")
                    score-=10
                    print("score: ",score)
            elif arrow_throw == "r":
                if wumpus[row][column+1] == "WUMPUS":
                    print("wumpus killed!")
                    score+=1000
                    print("score: ",score)
                    wumpus[row][column+1] = "Save"
                    wumpus[1][0]="Save"
                    wumpus[3][0]="Save"
                else:
                    print("arrow wasted...")
                    score-=10
                    print("score: ",score)
                
            
            arrow=False
    if wumpus[row][column] == "WUMPUS" :
        score-=1000
        print("\nWumpus here!!\n You Die\nAnd your score is: ",score
              ,"\n")
        break
    if(wumpus[row][column]=='GOLD'):
        score+=1000
        print("GOLD FOUND!You won....\nYour score is: ",score,"\n")
        break
    if(wumpus[row][column]=='PIT'):
        score-=1000
        print("Ahhhhh!!!!\nYou fell in pit.\nAnd your score is: ",score,"\n")
        break
```
</p>

### SAMPLE INPUT AND OUTPUT:

<img width="841" height="688" alt="image" src="https://github.com/user-attachments/assets/4cd581b3-e569-420f-880c-d11fa23938b6" />

## WUMPUS PROBLEM:

<img width="320" height="320" alt="image" src="https://github.com/user-attachments/assets/20a34e7e-9036-41b5-b49c-a2cd657057f6" />

## PROGRAM:

```python
# -----------------------------
#   WUMPUS WORLD - MOVE INPUT
# -----------------------------

# World representation based on your image map
world = {
    (1,4): ["Stench"],
    (2,4): ["Breeze"],
    (3,4): ["Pit"],
    (4,4): [],

    (1,3): ["Wumpus"],
    (2,3): ["Breeze", "Stench", "Gold"],
    (3,3): ["Pit"],
    (4,3): ["Breeze"],

    (1,2): ["Stench"],
    (2,2): [],
    (3,2): ["Breeze"],
    (4,2): ["Pit"],

    (1,1): ["Start"],
    (2,1): ["Breeze"],
    (3,1): [],
    (4,1): ["Breeze"]
}

# Player state
player_pos = [1, 1]   # start
has_gold = False
arrow = True
alive = True
won = False

def sense():
    """Print percepts in the current cell."""
    cell = tuple(player_pos)
    items = world.get(cell, [])

    print("\nYou sense:")
    if "Wumpus" in items:
        print("  💀 A terrible stench fills the air... WUMPUS is here!")
    if "Pit" in items:
        print("  🕳 A wind echoes… it's a PIT!")
    if "Breeze" in items:
        print("  🌬 Gentle breeze whispers danger.")
    if "Stench" in items:
        print("  💀 Faint stench nearby.")
    if "Gold" in items:
        print("  ✨ Something glitters... GOLD!")

def move(dir):
    """Move player if possible."""
    x, y = player_pos

    if dir == "W": y += 1
    elif dir == "S": y -= 1
    elif dir == "A": x -= 1
    elif dir == "D": x += 1

    # bounds check (1 to 4)
    if x < 1 or x > 4 or y < 1 or y > 4:
        print("🚧 You hit a wall. Can't go there.")
        return False

    player_pos[0], player_pos[1] = x, y
    return True

def check_death():
    """Check if the player died."""
    global alive, won
    items = world.get(tuple(player_pos), [])

    if "Pit" in items:
        print("💀 You fell into a PIT. Game over.")
        alive = False
    if "Wumpus" in items:
        print("💀 The WUMPUS devours you. Game over.")
        alive = False

def shoot():
    """Shoot arrow upward (toward y+ direction) as per your map."""
    global arrow

    if not arrow:
        print("❌ You already used your arrow.")
        return

    arrow = False
    print("🏹 You shoot an arrow upward...")

    # Ray passes through same x, increasing y
    ax = player_pos[0]
    ay = player_pos[1]

    for y in range(ay+1, 5):
        if "Wumpus" in world.get((ax, y), []):
            print("🎯 *thunk* You hear a scream. WUMPUS is dead!")
            world[(ax, y)].remove("Wumpus")
            return

    print("🪶 The arrow flies into the darkness and vanishes...")

# -----------------------------
#   GAME LOOP
# -----------------------------

print("=== WUMPUS WORLD ===")
print("Controls: W/A/S/D to move, F to shoot, Q to quit")

while alive and not won:
    print(f"\nYou are at {tuple(player_pos)}")
    sense()

    # Check for gold
    if "Gold" in world.get(tuple(player_pos), []) and not has_gold:
        choice = input("Pick up GOLD? (y/n): ").lower()
        if choice == "y":
            has_gold = True
            print("✨ You picked up the GOLD!")

    cmd = input("Your move (W/A/S/D/F/Q): ").upper()

    if cmd == "Q":
        break

    elif cmd in ["W", "A", "S", "D"]:
        moved = move(cmd)
        if moved:
            check_death()

    elif cmd == "F":
        shoot()

    # win condition (return with gold)
    if has_gold and tuple(player_pos) == (1,1):
        print("🏆 You escaped with the GOLD! You win!")
        won = True

if not alive:
    print("☠ Thanks for playing.")

```

## OUTPUT:
<img width="933" height="933" alt="image" src="https://github.com/user-attachments/assets/07d25db0-8071-4b98-ae9a-9f0818492761" />

## RESULT:

Thus,the program to solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic has been executed succesfully.
