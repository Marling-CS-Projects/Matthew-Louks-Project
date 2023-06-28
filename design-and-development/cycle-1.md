# 2.2.1 Cycle 1

## Design

### Objectives

For my project, I am using Kaboom.js. Kaboom is a popular Javascript programming library that I thought would be good because it has many resources, and it is not as complicated to use as some other programming libraries and languages out there.

For cycle 1, my aim is to create sprites for the player's character and for any platforms, enemies and obstacles, and get them to appear on the game screen. I will try to make the sprites look aesthetically pleasing, and I will distinguish everything by using different colours (see [Success Criteria](../analysis/1.5-success-criteria.md)).

* [x] Create a player sprite
* [x] Create sprites for enemies, obstacles and platforms
* [x] Get the sprites to appear on the game screen

### Usability Features

Non-functional: There will be colours to distinguish everything from one another. It will be obvious as to what is what: the player will be green, enemies will be red, etc. (Engaging, Easy to learn)

### Key Variables

| Variable Name | Use                      |
| ------------- | ------------------------ |
| kaboom        | Loads the Kaboom assets. |
| loadPedit     | Loads a .pedit file.     |

### Pseudocode

```
import kaboom

kaboom

loadPedit player
loadPedit enemy
loadPedit platform
loadPedit spike

add sprite player
    position
    area

add sprite enemy
    position
    area

add sprite platform
    position
    area

add sprite spike
    position
    area
```

## Development

### Outcome

There were problems with managing to get the .pedit sprites to show up initially, but I have now managed to get it to work. At this stage, I have made basic code snippets for displaying the sprites on the game screen.



Code:

```
import kaboom from "kaboom"

// initialize context
kaboom()

// load assets
loadPedit("player", "/sprites/player.pedit")
loadPedit("enemy", "/sprites/enemy.pedit")
loadPedit("platform", "/sprites/platform.pedit")
loadPedit("spike", "/sprites/spike.pedit")

// add a character to screen
add([
	// list of components
	sprite("player"),
	pos(80, 40),
	area(),
])

add([
    sprite("enemy"),
    pos(120, 40),
    area(),
])

add([
    sprite("platform"),
    pos(160, 40),
    area(),
])

add([
    sprite("spike"),
    pos(200, 40),
    area(),
])
```

### Challenges

Initially the game screen game me an error message that the 'player' sprite could not be found. This is because I was using 'loadSprite' instead of 'loadPedit'. When I used 'loadPedit' instead, the code worked as I wanted it to.

## Testing

### Tests

| Test | Instructions      | What I expect            | What actually happens                            | Pass/Fail |
| ---- | ----------------- | ------------------------ | ------------------------------------------------ | --------- |
| 1    | Run initial code  | My sprites would show up | Error message - player sprite could not be found | Fail      |
| 2    | Run improved code | My sprites would show up | My sprites show up                               | Pass      |

### Evidence

![](<../.gitbook/assets/image (4) (1) (1) (1).png>)
