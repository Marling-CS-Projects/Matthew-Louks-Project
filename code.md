# Code

```
import kaboom from "kaboom"

// initialize context
kaboom({
    background: [100, 155, 255],
})

// load assets
loadPedit("player", "/sprites/player.pedit")
loadPedit("enemy", "/sprites/enemy.pedit")
loadPedit("platform", "/sprites/platform.pedit")
loadPedit("spike", "/sprites/spike.pedit")

scene("start", () => {
    add([
        text("Mathematical Platformer - Press any key to start. Make sure your screen is not too large. Otherwise, please stop the game, resize the screen and press run. This text should be 4 lines", { //text for start screen
            width: width(), //sets the text to wrap to the next line
            font: "sans-serif",
        }),
    ])
    onKeyPress(() => {
        go("difficulty"); //when any key is pressed, the difficulty screen is shown
    })
})

scene("difficulty", () => {
    add([
        text("Press 1 for easy, 2 for medium, or 3 for hard", {
            width: width(),
            font: "sans-serif"
        }),
    ])
    onKeyPress("1", () => { //difficulty = number of enemies
        enemyCount = 1;
    })
    onKeyPress("2", () => {
        enemyCount = 2;
    })
    onKeyPress("3", () => {
        enemyCount = 3;
    })
    onKeyPress(() => {
        go("instructions"); //"instructions" = instruction screen
    })
})

scene("instructions", () => {
    add([
        text("Press the left and right arrow keys to move left and right. Press the up arrow key to jump. OR: Press the A and D keys to move left and right. Press the W key to jump. Press P to pause and space to unpause. Press space to continue", {
            width: width(),
            font: "sans-serif"
        })
    ])
    onKeyPress("space", () => {
        go("game");
    })
})

go("start");

let score = 0;
scene("game", () => {
    onKeyPress("p", () => {
        debug.paused = true;
        onKeyPress("space", () => {
            debug.paused = false;
        })
    })
    // add sprites to screen
    const player = add([
	   // list of components
	   sprite("player"),
	   pos(80, 150),
	   area(),
       body(),
        {
            speed: 0,
            acceleration: 10,
            max_speed: 200,
        },
    ])

    //sets gravity value
    setGravity(500)

    //sets key bindings
    onKeyDown("left", () => {
        player.speed = Math.max(
            player.speed - player.acceleration,
            -player.max_speed
        );
        player.move(player.speed, 0)
    })

    onKeyDown("a", () => {
        player.speed = Math.max(
            player.speed - player.acceleration,
            -player.max_speed
        );
        player.move(player.speed, 0)
    })

    onKeyDown("right", () => {
        player.speed = Math.min(
            player.speed + player.acceleration,
            player.max_speed
        );
        player.move(player.speed, 0)
    })

    onKeyDown("d", () => {
        player.speed = Math.min(
            player.speed + player.acceleration,
            player.max_speed
        );
        player.move(player.speed, 0)
    })

    onKeyDown("up", () => {
        if (player.isGrounded()) {
            player.jump(360)
        }
    })

    onKeyDown("w", () => {
        if (player.isGrounded()) {
            player.jump(360)
        }
    })

    onKeyRelease(() => {
        player.speed = 0
    })
    
    addLevel([ //adds a floor by means of a level structure
        "              ",
        "              ",
        "              ",
        "^            ^",
        "==============",
    ], {
        tileWidth: 50, //sets width of a floor tile
        tileHeight: 50, //sets height of a floor tile
        tiles: {
            "=": () => [
                sprite("platform"),
                area(), //gives the tiles colliders to detect player
                body({isStatic: true}), //static (cannot be moved)
            ],
            "^": () => [
                sprite("spike"),
                area(),
                body(),
               "danger",
            ]
        }
    })

    for (let i = 0; i < 3; i++) { //generates three platforms
        const x = rand(0, width()) //generates at a random x-position
        add([
            sprite("platform"), //uses the 'platform' sprite
            pos(x, 50),
            area(),
            body({isStatic: true}),
        ])
    }
    for (let i = 0; i < 3; i++) { //same at different y-position
        const x = rand(0, width())
        add([
            sprite("platform"),
            pos(x, 100),
            area(),
            body({isStatic: true}),
        ])
    }
    for (let i = 0; i < 3; i++) { //same again, at different y-pos
        const x = rand(0, width())
        add([
            sprite("platform"),
            pos(x, 150),
            area(),
            body({isStatic: true}),
        ])
    }

    let firstNumber = randi(1, 11);
    let secondNumber = randi(1, 11);

    add([ //adds the first number
        text(firstNumber, {
            font: "sans-serif",
        }), //generates a random number between 1-10
        pos(50, 50), //sets the position
        { value: firstNumber }, //sets the value of the variable
    ])

    add([ //adds the second number
        text(secondNumber, {
            font: "sans-serif",
        }),
        pos(150, 50),
        { value: secondNumber },
    ])

    let operation = randi(1, 4) //generates random number between 1-3
    if (operation === 1) {
        operationText = "+";
    } else if (operation === 2) {
        operationText = "-";
    } else if (operation === 3) {
        operationText = "*";
    }

    add([
        text(operationText, {
            font: "sans-serif",
        }), //displays the operation
        pos(100, 50), //positioned between the two numbers
        { value: operationText },
    ])

    add([
        text("Score: " + score, {
            font: "sans-serif",
        }), //Shows the score
        pos(100, 225),
        { value: score },
    ])
 
    if (operation === 1) { //for addition
        answer = firstNumber + secondNumber;
    } else if (operation === 2) { //for subtraction
        answer = firstNumber - secondNumber;
    } else if (operation === 3) { //for multiplication
        answer = firstNumber * secondNumber;
    }

    const z = rand(0, width())
    const w = rand(10, 25)
    const a = rand(0, 255);
    const b = rand(0, 255);
    const c = rand(0, 255);
    add([
        text(answer, {
            font: "sans-serif",
        }),
        pos(z, w), //adds the text at a random width position
        area(),
        color(a, b, c), //gives the text a random colour
        "correct",
        { value: answer },
    ])

    for (let i = 0; i < 3; i++) {
        let wrongAnswer = randi(1, 101); //generates a random number between 1 and 100
        if (wrongAnswer === answer) {
            i -= 1;
        }
        const z = rand(0, width());
        const w = rand(10, 25);
        const a = rand(0, 255);
        const b = rand(0, 255);
        const c = rand(0, 255);
        if (wrongAnswer !== answer) {
            add([
                text(wrongAnswer, {
                    font: "sans-serif",
                }),
                pos(z, w),
                area(),
                color(a, b, c),
                "danger", //shows that this will kill the player if touched
            ])
        }
    }

    scene("game over", () => {
        add([
            text("GAME OVER! Press T to try again, or space to go to the start menu", {
                width: width(),
                font: "sans-serif",
            }),
        ])
        onKeyPress("space", () => {
            go("start"); //to go to the start screen again
        })
        onKeyPress("t", () => {
            go("game"); //to restart
        })
    })
    player.onCollide("correct", () => {
        score += 1;
        if (score === 10) {
            go("win"); //if you reach 10 points, you win
        } else {
            go("game"); //if you hit the correct answer, you get another question and answer set
        }
    })
    scene("win", () => {
        score = 0; //resets the score for the next game
        add([
            text("You got 10 questions correct. YOU WIN! Press T to try again, or space to go to the start menu", {
                width: width(),
                font: "sans-serif",
            })
        ])
        onKeyPress("space", () => {
            go("start");
        })
        onKeyPress("t", () => {
            go("game");
        })
    })
    player.onCollide("danger", () => {
        score = 0; //resets the score for the next game
        go("game over"); //if you hit danger, you lose and go to the 'game over' screen
    })
    player.onUpdate(() => {
        if (player.pos.y >= 250) { //if the player goes below a certain y-position, game over
            score = 0;
            go("game over");
        }
    })
    try {
        for (let i = 0; i < enemyCount; i++) { //to spawn enemies on the level
            x = rand(150, width());
            y = rand(0, 150);
            add([
                sprite("enemy"),
                pos(x, y), //random position
                area(),
                body(),
                path(),
                "danger",
            ])
        }
    }
    catch(err) {
        go("difficulty");
    }
    function path(speed = 100, dir = 1) { //generates the 'path' function with speed and direction
        return {
            id: "path",
            require: [ "pos", "area" ],
            add() {
                this.on("collide", (obj, col) => { //when an enemy collides with an object...
                    if (col.isLeft() || col.isRight()) {
                        dir = -dir //...the enemy's direction is reversed
                    }
                })
            },
            update() {
                this.move(speed * dir, 0)
            },
        }
    }
})
```
