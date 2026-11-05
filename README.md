# Mizan for Garry's Mod

Mizan is a server-side anti-cheat for Garry's Mod (GMod) servers. It catches aimbots, silent aim, triggerbots, anti-aim,
bunny hop scripts, fake lag and server crashers by how players aim, move and time their commands on your server. Players
install nothing. Its fog of war stops your server sending a player the positions of enemies they can't see, so a
wallhack or ESP has nothing to draw.

Mizan is in early access, free, and opening to Garry's Mod communities one at a time.
[Register your community](https://mizan.ac/dashboard/new) to get it. The module isn't in this repository: you download it
from your community's dashboard, built for your server and carrying its key.

[mizan.ac/anti-cheat](https://mizan.ac/anti-cheat) ·
[Compared with other anti-cheats](https://mizan.ac/anti-cheat/compare) ·
[False flags](https://mizan.ac/anti-cheat/false-flags) ·
[Discord](https://discord.gg/fRbk43tKcV)

## How it decides

A small module on your server reads what the game already receives from each player and sends it to Mizan's detection
service. The module makes no judgements itself, so there's nothing on your server for a cheat to find or switch off.

On the service, AI models trained on real play score each fight by how the view moves against its target before, during
and after the shot. Beside them, algorithmic detectors test what a hand on a mouse can and can't do, and whether the
numbers the game sends add up. A case opens only when two independent kinds of measurement agree, unless an exact check
of the game's own numbers fails. Each detector alarms only when a reading is at least 10,000 times likelier from a cheat
than from real players' recorded play. Headshot rates and kill counts are never an input: good players have high ones
too.

Your staff see each case with a 3D replay, on the dashboard and in Discord, and decide before anyone is banned. Bans go
through your admin mod (SAM, ULX, sAdmin, ServerGuard, xAdmin, xAdmin 2, Lyn, D3A, FAdmin) or a ban command of your own. Mizan also reads hundreds of public ban lists, so a
player banned on other communities is known when they join.

## What it detects

37 cheat features, described by what each does in a game. How each is found isn't published, because cheat
makers read this too.

### Aim, sight and shooting

| Cheat | What it does |
|---|---|
| Aimbot | Turns the player's aim onto an enemy's hitbox, by setting the angles outright or by faking mouse input. |
| Silent aim | Aims each shot at an enemy while the player's own screen and crosshair stay where they were. |
| pSilent | Perfect silent aim: changes the aim only in the command that fires and holds it back, so not even a spectator sees it snap. |
| Triggerbot | Fires the moment an enemy's hitbox is under the crosshair. |
| Rapid fire | Sends a burst of extra commands that tap attack, so a semi-automatic weapon fires like an automatic. |
| Double tap | Saves up ticks, then spends them in one burst to fire a second shot before the weapon is ready (tickbase shifting). |
| No recoil | Takes the weapon's recoil off the aim of every shot, so a spray stays on target. |
| No spread | Works out each bullet's random spread and aims against it, so every shot lands where the crosshair points. |
| Backtrack | Rewrites the shot's tick so the server's lag compensation checks where the enemy stood a moment ago. |
| Engine prediction | Runs the game's movement prediction first, so the aimbot shoots from where the player will be this tick. |

### Movement and view

| Cheat | What it does |
|---|---|
| Anti-aim | Sends fake and real pitch and yaw, fixed, jittering or spinning (a spinbot), so enemies aim at the wrong place. |
| Desync | A desynculator: knocks the player's commands out of step with the server's clock, so where they stand and where they can be hit stop matching. |
| Movement fix | Turns the movement keys with the angles the cheat sends, so silent aim and anti-aim never change where the player walks. |
| Fake duck | Flicks crouch on and off every other command, so the player looks crouched while shooting from standing height. |
| Air stuck | Stops sending movement, so the player hangs frozen in place, even in mid-air. |
| Bhop | A bunny hop script: presses jump the instant the player lands, so they never lose speed. |
| Auto strafe | Steers left and right in the air for the player to build speed on every jump, in legit, directional and rage modes. |

### Time and lag

| Cheat | What it does |
|---|---|
| Fake lag | Holds back up to a dozen or so commands and sends them at once, so other players see the cheater jump between spots. |
| Fake latency | Answers the server with old packet acknowledgements, so the player's ping looks higher and lag compensation lets them hit further back in time. |
| Reduce latency | Shaves the delay the game builds into the player's connection, so they see and shoot first. |
| Slow motion | Sends fewer commands than the game runs, so the server moves the cheater in slow motion. |
| Warp | Charges up held-back ticks, then releases them at once to cover a long distance in an instant. |
| Sequence freezing | Holds the connection's packet count still while the player keeps moving, then lets it jump forward. |

### Taunts and spam

| Cheat | What it does |
|---|---|
| Loop taunt | Restarts a taunt the moment it ends, so it plays forever. |
| Taunt camera block | Keeps the first-person view during a taunt, so the player can still see and aim. |
| E spammer | Presses Use on every command, spamming doors, buttons and anything else it reaches. |
| Flashlight spammer | Switches the flashlight on and off on every command, flashing it and spamming its click. |
| Noise maker | Makes noise for everyone nearby, over and over. |

### Hiding the cheat

| Cheat | What it does |
|---|---|
| Patched mouse movement | Rewrites the mouse movement in each command to match the aim the cheat set, so it looks like it came from a hand. |
| Patched key input | Rewrites the key presses in each command to match the buttons the cheat pressed, so they look typed. |
| Caught Lua errors | Catches errors from the cheat's Lua scripts so they never show in the console or reach the server. |
| Blocked console commands | Refuses the commands the server runs on the player's game, such as connect, disconnect and say_team. |
| Blocked gestures | Stops the gestures the server plays on the player's model. |
| Restored ConVars | Puts the game settings the cheat changed back as they were, so they read as untouched. |

### The server itself

| Cheat | What it does |
|---|---|
| Game events | Fakes game events the player never caused. |
| Server laggers | Server crashers: flood the server with oversized voice data, file requests or string commands until it lags or crashes. |
| Network exploits | Sends fake net messages to addons for free money, items or admin. |

## Install

1. On your community's dashboard at [mizan.ac](https://mizan.ac), open Downloads, choose the server and its platform, and
   download the module.
2. Extract it into the folder that holds `garrysmod/`. This adds the module, its settings and the server's key, and loads
   Mizan whenever the server starts.
3. Load it from the server console without a restart, with the command the dashboard shows:

   ```
   plugin_load lua/bin/<loader for your platform>
   ```

4. Run `mizan_status` in the console. The server shows as Connected on its dashboard page within seconds.

Servers already running the module update themselves.

## Requirements

A Garry's Mod dedicated server that can load binary modules, on Linux or Windows, 32-bit or 64-bit. Garry's Mod's x86-64
branch is 64-bit; a default install is 32-bit.

## Help

Setting up, questions and false flags: [Discord](https://discord.gg/fRbk43tKcV) or contact@mizan.ac. Please don't post
SteamIDs or player details in a public issue. Security reports follow [our policy](https://mizan.ac/security).
