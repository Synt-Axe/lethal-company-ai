
# Lethal Company Ship Command AI
This script is able to do some of the ship command role responsibilities in Lethal Company, namely communicating map information to the player via the walkie-talkie, and countering dogs and giants using the radar booster and the drop ship. This script runs in complete Vanilla, meaning it needs to have control over a separate instance of the game to function. It also has a basic command system so the player can control it via the in-game text chat. 

This script was made as a part of the YouTube video ["AI Learns To Play Lethal Company"](https://youtu.be/poZt_KjCwV4).

## How to use?
Video Tutorial: https://youtu.be/hxgGS1V1P40
### Step 1: Clone the repository.
```bash
git clone https://github.com/Synt-Axe/lethal-company-ai.git
```
Or download the code directly as a [zip file](https://github.com/Synt-Axe/lethal-company-ai/archive/refs/heads/main.zip).
### Step 2: Setup the Python Environment.

Note: The code was tested on Python version 3.9.5

1. Enter the code directory.
```
cd lethal-company-ai
```

2. Create a virtual environment.
```
python -m venv lcenv
```

3. Activate the environment.
```
source lcenv/bin/activate # Linux
.\lcenv\Scripts\activate # Windows 
```

4. Install pip and ipykernel.
```
python -m pip install --upgrade pip
pip install ipykernel
```

5. Add the environment to ipykernel.
```
python -m ipykernel install --user --name=lcenv
```

6. Install the rest of the dependencies.
```
pip install -r requirements.txt
```

7. Run jupyter notebook.
```
python -m notebook
```

### Step 3(Optional): Install VB-Audio. (For Vocal Communications)
Install [VB-Audio](https://vb-audio.com/Cable/index.htm). And set it to be your input and output device.

### Step 4: Setup the Script Parameters.
Follow the instruction in [A0_Initialization.ipynb](https://github.com/Synt-Axe/lethal-company-ai/blob/main/A0_Initialization.ipynb).

### Step 5: Run the AI!
You can now run any of the 3 AIs. Note that the easiest one to start with is [AI2_HotAndCold.ipynb](https://github.com/Synt-Axe/lethal-company-ai/blob/main/AI2_HotAndCold.ipynb).


## How it works?

### Map Detection
The way the script works is by applying colour masks to the map screenshot to capture the necessary information. There are mainly 3 masks:

- A loot mask (captures yellow objects)

- An enemy mask (captures circular red objects)

- A player mask (captures the blue cursor that shows where the player is looking)

For the enemies, the red color mask is not enough since it will capture turrets, vents and closed doors too. So the script removes any object that is not circular, leaving only the enemies.

For the player mask, the script uses the center of the cursor mass, in relation with the screenshot center to detect where the player is looking, and then based on that calculates the direction of the loot and the enemies.

I originally tried to use a TensorFlow object detection model, but later ditched the idea for the much easier masks approach. Since luckily for me, Zeekers made the map so colourful.

### Communication
Something that was also very challenging is how to communicate the information to the player efficiently. I mainly experimented with 2 approaches:

#### 1- Voice Chat

#### Pros:

- More fun and "human".
- Faster in some cases, since it can be done while the AI is in the terminal. (Text chat requires the AI to leave the terminal to send it)

#### Cons:

- Noisy. In many cases I found it hard to hear properly inside the facility because of the continuous updates from the AI.
- Requires the AI to look out for dogs. This causes more delay, since the AI has to check the map twice, once for the player and once for himself to check for dogs.
- If you don't focus while the AI is saying the info, you don't get to hear it again.

#### 2- Text Chat

#### Pros:

- Quite
- It's written, so you can look it it multiple times and you don't have to take it in all at once.

#### Cons:

- Has a minimum ~2.5 second delay since that's how long it takes the AI to leave the terminal and send the message. Unless you make the AI look at the map in the ship map outside the terminal, but I found that to be impractical for many reasons.
- The text chat only allows 4 lines per message, and only shows a total of 4 messages on the screen, so that limits how much info you can send at once. For example I was really annoyed that "The Grid" AI had to send the info on two messages instead of one.

### How to Improve It?
#### I think the following are the best improvements that people can apply to the AI in the future:
- Identifying turrets, mines and doors, and operating them. (Will have to learn to read the letters and numbers)
- Memorise the path of the player from the entrance/fire exit so it can lead the player back in case they get lost. This could potentially be something the AI excels in more than a human player could.
- Identify different enemies based on the red dot size. This is something I originally wanted to include in the AI, but did not get the chance to do so. One thing that makes this challenging is that I observed the enemies change their dot size when they get close to the map edge, which might make this approach inconsistent.

## Community Contributions
### [AutomaticSignals Mod](https://thunderstore.io/c/lethal-company/p/TestAccount666/AutomaticSignals/) by [Test-Account666](https://github.com/Test-Account666)
A mod that turns the signal translator into a robotic teammate that can warn you about enemies, open doors, deactivate turrets, teleport you back to the ship, and more.

### [Easy Installer](https://github.com/zselybence/Lethal-Company-AI-Installer) by [zselybence](https://github.com/zselybence)
A script that automatically sets up the Python environment and installs the dependencies.

## License

[MIT](https://github.com/Synt-Axe/lethal-company-ai/blob/main/LICENSE)
