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


### Division of labor

1. Felipe:

1.1.  User input: everything that is written in terminal. E.g.: filename.cub
- Positive scenario:
	```shell
	%> ./cub3D mapname.cub
	<this is where the game starts
```
- Negative scenario:
```shell
%> ./cub3D stupidfilename
Error
Your file sucks
```


1.2. Parsing: everything inside the `.cub` file:
- Check for coordinates information (name, sprite path)
- RGB values: make sure that they are within 0 or 255. Anything else but this range leads to error
- Actual map: floodfill using the zeroes to find if the map is walled-off. Any kind of misconfiguration will be considered an error, such as extra map islands, weird characters, empty lines, and etc.

```
               111111111111111
               111111111000001
               1100000000000011111
                111100000N00000000011
               11111111111111111111
```

1.3. Memory management
- be sure that memory on my end will be dealt properly  at the beginning and end.

1.4. Choose sprites
- Sprites that can be animated

2. Alex
1.1. Link MLX42 in Makefile
1.2. 2D minimap
1.3. Player movement
1.4. Raycasting algorithm
1.5. Texture
1.6. Game testing