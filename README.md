# Maze game

## Game explained

The goal of the game is to score as many points as you can in 2mins!

You will play in pairs, holding the box by the strings to get the ball from one goal to the other.

After 2 minutes, the players will be given their score and the new game can start. 

## Let's see how the score tracking works

Get a ``||input:pin P1 is pressed||`` block and place it in the value slot of ``||logic:if then||``.

Then add a ``||basic:show number 1||`` to show "1" when the goal is hit.

``|Download|`` the code to your microbit.

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        basic.showNumber(1)
    }
})
```
## Connect the cables

Next connect one cable to GND, the other to pin 1.

Touch the 2 cables together. 

You should see a tick mark displayed on the microbit. 

You can try that with a marble wrapped in foil to make sure it works.

## Score!

Let's create a new variable called ``||variable:score||``.

We need to set the value of the ``||variable: set score to 0||`` when the game starts.

And each time the pin is pressed, we need to increase the score by 1. 

We can do that with ``||variable: change score by 1||``.

Instead of showing the number one, let's show the current score.

Replace ``||basic:show number 1||`` with ``||basic: show number score||``

``|Download|`` the code and see if the number increases each time the cables touch.

```blocks
let score = 0
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        score += 1
        basic.showNumber(score)
    }
})
```

## Now repeat for the other goal

Repeat the exercise for pin 2 so that you have both gates working. 

Download the code to the microbit and check that the score is increasing when you connect the cables to pin 2.

You can see an example in the hint below.
```blocks
let score = 0
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        score += 1
        basic.showNumber(score)
    }
    if (input.pinIsPressed(TouchPin.P2)) {
        score += 1
        basic.showNumber(score)
    }
})
```

## Alternating sides

To make it more challenging let's require that a different goal is hit each time.

Create a new variable``||variable: side||`` and ``||variable: set side to 1||``

Draw an arrow to indicate which side needs to be hit first ``||basic:show leds||`` with an arrow pointing right.

```blocks
let score = 0
let side = 1
basic.showLeds(`
    . . # . .
    . . . # .
    # # # # #
    . . . # .
    . . # . .
    `)
```

## Handling goals

First add ``||logic: if side = 1||`` to the block containing if ``||logic: if pin P1 is pressed||``

Then ``||variable: set side to 2||``.

Repeate for the other side. Add ``||logic: if side = 2||`` to the block containing if ``||logic: if pin P2 is pressed||``

And ``||variable: set side to 1||``.

Now to score, the players will need to hit opposing goals!

```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        if (side == 1) {
            score += 1
            basic.showNumber(score)
            side = 2
        }
    }
    if (input.pinIsPressed(TouchPin.P2)) {
        if (side == 2) {
            score += 1
            basic.showNumber(score)
            side = 1
        }
    }
})
```

## Directions

To show which side needs to be hit next, show an arrow after scoring.

Add a ``||basic: pause (ms) 2000||`` after ``||basic: show number score||``

Then display an arrow pointing left ``||basic: show leds||``.

``|Download|`` the code and confirm that it works as expected.

If it does, let's repeat for the other side. Don't forget to flip the arrow!

Check the hint below!
```blocks
basic.forever(function () {
    if (input.pinIsPressed(TouchPin.P1)) {
        if (side == 1) {
            score += 1
            basic.showNumber(score)
            side = 2
            basic.pause(2000)
            basic.showLeds(`
                . . # . .
                . # . . .
                # # # # #
                . # . . .
                . . # . .
                `)
        }
    }
    if (input.pinIsPressed(TouchPin.P2)) {
        if (side == 2) {
            score += 1
            basic.showNumber(score)
            side = 1
            basic.pause(2000)
            basic.showLeds(`
                . . # . .
                . . . # .
                # # # # #
                . . . # .
                . . # . .
                `)
        }
    }
})
```

## Adding a time limit

At this point you have a working game already, but to make it more exciting let's add a time limit.

To make it more fair, let's have it start once a button is pressed.

Start with ``||input:on button A pressed||``. You can play a melody to indicate that the game is starting at this point. 

Create a new variable ``||variable: time_left||`` and set it's value ``||variable: time_left to 1||``.

Add a ``||basic: pause (ms) 120000||``. This will give the players 2minutes to score as high as they can.

Next let's indicate that the game finished and ``||basic: show number score||``.

You might want to play a sound here!

```blocks
let score = 0
let time_left = 0
let side = 1
basic.showLeds(`
    . . # . .
    . . . # .
    # # # # #
    . . . # .
    . . # . .
    `)

input.onButtonPressed(Button.A, function () {
    time_left = 1

    basic.pause(12000)
    time_left = 0
    basic.showNumber(score)
})
```


## Cleaning up

To avoid confusing players, let's move the arrow from ``||basic:on start||`` to after the button A is pressed.

Instead let's show a message to our players that they need to press A. ``||show string Press A!||``

Check the hint below!
```blocks
let score = 0
let time_left = 0
let side = 1
basic.showString("Press A!")

input.onButtonPressed(Button.A, function () {
    time_left = 1
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
    basic.pause(12000)
    time_left = 0
    basic.showNumber(score)
})
```

## Stop the scoring after time is up

Think about how to stop the players from scoring any more once the time is up.

```blocks
basic.forever(function () {
    if (time_left = 1) {
        if (input.pinIsPressed(TouchPin.P1)) {
            if (side == 1) {
                score += 1
                basic.showNumber(score)
                side = 2
                basic.pause(2000)
                basic.showLeds(`
                . . # . .
                . # . . .
                # # # # #
                . # . . .
                . . # . .
                `)
            }
        }
        if (input.pinIsPressed(TouchPin.P2)) {
            if (side == 2) {
                score += 1
                basic.showNumber(score)
                side = 1
                basic.pause(2000)
                basic.showLeds(`
                . . # . .
                . . . # .
                # # # # #
                . . . # .
                . . # . .
                `)
            }
        }
    }

})

```

## Enjoy the game
Let's see how high you can score!

Swap the mazes with other students, see if theirs is easier or harder.

Check the hint below!
```blocks
input.onButtonPressed(Button.A, function () {
    time_left = 1
    basic.showLeds(`
        . . # . .
        . . . # .
        # # # # #
        . . . # .
        . . # . .
        `)
    basic.pause(120000)
    time_left = 0
    music._playDefaultBackground(music.builtInPlayableMelody(Melodies.PowerDown), music.PlaybackMode.InBackground)
    basic.showNumber(Score)
})
let time_left = 0
let Score = 0
Score = 0
let Side = 1
music._playDefaultBackground(music.builtInPlayableMelody(Melodies.PowerUp), music.PlaybackMode.InBackground)
basic.showString("Press A!")
basic.forever(function () {
    if (time_left == 1) {
        if (input.pinIsPressed(TouchPin.P1)) {
            if (Side == 1) {
                music._playDefaultBackground(music.builtInPlayableMelody(Melodies.JumpUp), music.PlaybackMode.InBackground)
                Score += 1
                basic.showNumber(Score)
                Side = 2
                basic.pause(2000)
                basic.showLeds(`
                    . . # . .
                    . # . . .
                    # # # # #
                    . # . . .
                    . . # . .
                    `)
            }
        }
        if (input.pinIsPressed(TouchPin.P2)) {
            if (Side == 2) {
                music._playDefaultBackground(music.builtInPlayableMelody(Melodies.JumpUp), music.PlaybackMode.InBackground)
                Score += 1
                basic.showNumber(Score)
                Side = 1
                basic.pause(2000)
                basic.showLeds(`
                    . . # . .
                    . . . # .
                    # # # # #
                    . . . # .
                    . . # . .
                    `)
            }
        }
    }
})

```


