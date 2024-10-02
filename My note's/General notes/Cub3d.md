- No map limits;
- Does not need to be square;
- Collisions?
- No exit is necessary;

| **Task**          | **What to do**                           | **Responsible** |
| ----------------- | ---------------------------------------- | --------------- |
| Parsing           | Make sure that the map is valid          |                 |
| Graphics          | Put images and window up                 |                 |
| Ray-casting logic | Weird math so the player can see in-game |                 |

### Map

1. The map will be composed of **only** six characters:
	- 0 for empty spaces;
	- 1 for walls;
	- N, S, E, or W for orientation of the view of the character;
2. The map is closed off/surrounded by walls
3. There can be empty spaces and should be rendered however we see fit
