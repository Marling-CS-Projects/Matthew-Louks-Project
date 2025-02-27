# 2.1 Design Frame

## Systems Diagram

<figure><img src="../.gitbook/assets/Screen Shot 2023-05-19 at 14.48.37.png" alt=""><figcaption></figcaption></figure>

This diagram shows the different parts of the game that I will focus on creating. I have split each section into smaller sub-sections. Throughout the development stage, I will pick one or two of these sections to focus on at a time to gradually build up and piece together the game. I have broken the project down this way as it roughly corresponds to the success criteria.

## Usability Features

Usability is an important aspect to my game as I want it to be accessible to all. There are 5 key points of usability to create the best user experience that I will be focusing on when developing my project. These are:

### Effective

Users can achieve the goal with completeness and accuracy. To do this, I will make it easy for the players to realise that they need to reach a goal in order to complete a level. I will make this goal clear to see so there is no confusion over where the players need to go.

#### Aims

* Create a clear goal to reach to determine the end of a level

### Efficiency

The speed and accuracy to which a user can complete the goal. To do this, I will create a menu system which is easy to navigate through in order for to find what you are looking for. The information which is more important can be found with less clicks.

#### Aims

* Create a menu system that is quick and easy to navigate through
* Create a controls system that isn't too complicated but allows the player to do multiple actions

### Engaging

The solution is engaging for the user to use. To do this, I will create some levels to keep the players engaged and allow them to have fun while playing the game. Using vector style art will also make the game nicer to look at than blocks, so will draw more people in, keeping them engaged.

#### Aims

* Create a series of levels to work through
* Incorporate a style of game art the suits the game

### Error Tolerant

The solution should have as few errors as possible and if one does occur, it should be able to correct itself. To do this, I will write my code to manage as many different game scenarios as possible so that it will not crash when someone is playing it.

#### Aims

* The game doesn't crash
* The game does not contain any bugs that damage the user experience

### Easy To Learn

The solution should be easy to use and not be over complicated. To do this, I will create simple controls for the game. I will make sure that no more controls are added than are needed in order to keep them as simple as possible for the players.

#### Aims

* Create a list of controls for the game
* Create an in-level guide that helps players learn how to play the game

## Pseudocode for the Game

### Pseudocode for game

Here is basic pseudocode for Kaboom.js. This pseudocode loads the Kaboom library and adds a sprite for the player.

```
load Kaboom
add player
    sprite
    position
    area
    body
```

### Pseudocode for a level

Here is pseudocode for a level in Kaboom. This is just an example of what the layout of a level could look like.

<pre><code>constant level

"                  "
"   A    A    A    "
"   =    =    =    "
"@  Q O     E  O   "
<strong>
</strong>define symbol
<strong>
</strong>@ = player
sprite
scale
origin

Q = question
sprite
scale
origin

A = answer
sprite
scale
origin

E = enemy
sprite
scale
origin

O = obstacle
sprite
scale
origin

= = platform
sprite
scale
origin
</code></pre>
