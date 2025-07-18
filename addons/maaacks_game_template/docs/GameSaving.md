# Game Saving

> [!IMPORTANT]  
> The save system doesn't follow the same conventions as other systems.  
> It is subject to change.  

> [!WARNING]  
> The save system relies on resource files, which are vulnerable to having malicious scripts injected into them.  
> Please discourage players from sharing their save files. Do not use this for cloud saving, either.  
> A safer save system is planned.  


The templates and plugin suite aim to keep most class definitions within the addon. These are not usually expected change. Unlike the other classes, the `GameState` and `LevelState` are defined for the developer to edit to their needs.

## Usage

The `GlobalState` static class keeps the state saved to a resource. The developer is responsible for making sure `GlobalState.save()` gets called when they want the state saved to the disk.  

### Game State

The `GameState` class represents the state of a single playthrough of the game. It currently stores the current level, the max level reached, and the state of each level currently visited.

It is currently expected to be used as a singleton, too.


### Level State

The `LevelState` class represents the state of a single level in a playthrough of the game. It currently stores whether the tutorial has been read, and a color, if the player has set one in the example levels.  It can be used to store the states of many other level specific features.

From within the `_ready()` method of a level scene, call `GameState.get_level_state(scene_file_path)` to get the last saved `LevelState`, or a new one, and then set the state of the level from that. When a state of the level changes that is intended to be preserved, save it into the level state, and call `GlobalState.save()`.

Examples are provided allowing the player to save the level background color, and keeping the tutorial message from popping up more than once per playthrough.