#### LEARN PHASER: BASICS

# Keyboard Events

Only some games exclusively use the mouse to play. Plenty of browser games, especially those with more complex gameplay, require keyboard input. Before, we assigned mouse events to specific GameObjects. This helped us tell if a mouse cursor was hovering over, or clicking on, an object in our game. Where mouse clicks take place at a specific point in our game with x and y coordinates, a keyboard offers a different interface without that positional information. So our keyboard handlers will handle any keypress that happens while our game is in focus — for this reason, they won’t be registered as events to particular GameObjects in our game.

The first way of adding a keypress handler is by calling this.input.keyboard.on(). This takes two arguments: first, the name of the event — something like 'keydown-A' for the A keypress. Next, the function to be called when handling the keypress. We can pass a function we’ve defined elsewhere, but unless you’re duplicating functionality (say to avoid replicating the same code for a keyboard and a gamepad) it’s fine to define an anonymous function. Here’s how that would look:

```js
const gameState = {};

function create() {
  gameState.circle = this.add.circle(30, 30, 10, 0xFF0000);
  this.input.keyboard.on('keydown-W', function() {
    gameState.circle.fillColor = 0xFFFF00;
  });
}

```

This code creates a red circle and then, when a W is pressed on the keyboard, the circle turns yellow.

createCursorKeys()
Another way of adding a keyboard event listener is by using a shortcut that Phaser offers, createCursorKeys(). This creates an object that maps the names of some usual cursor keys (UP, DOWN, LEFT, RIGHT, SHIFT, and SPACE) to a cursor object that we can use to detect when they’ve been pressed. We can save those as a property in our gameState object and then check if they’re pressed within our update() function.


```js
const gameState = {};

function create() {
  gameState.circle = this.add.circle(50, 50, 20, 0xFF0000);
  gameState.cursors = this.input.keyboard.createCursorKeys();
}

function update() {
  if (gameState.cursors.left.isDown) {
    // move the circle left!
    gameState.circle.x -= 3;
  }
}

const config = { scene: { create, update }};
const game = new Phaser.Game(config);


```
Above, we created a cursors property for our gameState and assigned the result of .createCursorKeys() to it. In our update() method we checked if the left key is being pressed by checking if gameState.cursors.left.isDown is truthy. If the left button is pressed, we move the circle to the left.

