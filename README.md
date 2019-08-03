# Canvas - Code Along



<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">1</h2>

### Create the project and the file structure



```bash
mkdir eternal_enemies && cd eternal_enemies
mkdir src css

touch index.html src/main.js src/game.js src/player.js src/enemy.js css/style.css
```







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">2</h2>

### Create basic HTML skeleton

##### `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Canvas Code Along</title>
  <link rel="stylesheet" href="./css/style.css">
</head>
<body>
  <script src="./src/main.js"></script>
  <script src="./src/game.js"></script>
  <script src="./src/player.js"></script>
  <script src="./src/enemy.js"></script>
</body>
</html>
```



<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">3</h2>

### Add the following CSS styles

##### `style.css`

```css
/* ---- reset ---- */

html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}

body {
  margin: 0;
  padding: 0;
}


/* ---- typography ---- */

body {
  color: #111;
  font-family: Helvetica, Arial, sans-serif;
  font-size: 16px;
  line-height: 147%;
}

p {
  margin: 0;
}



/* ---- layout ---- */

html, body {
  height: 100%;
}

.container {
  margin: 0 20px;
}

@media (min-width: 768px) {
  .container {
    max-width: 728px;
    margin: 0 auto;
  }
}


/* ---- components ---- */

.game {
  text-align: center;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.game header {
  height: 50px;
  display: flex;
  align-items: center;
}

.game .lives {
  flex: 1;
}

.game .score {
  flex: 1;
}

.game .label {
  font-weight: bold;
}

.game .value {
  font-style: italic;
}

.game .canvas-container {
  flex: 1;
}

```







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">4</h2>

### Create the functions for building and appending DOM elements 



##### `main.js`

```js
'use strict';

// Creates DOM elements from a string representation
function buildDom() {};

// Runs on initial start and contains calls all other functions that manage the game
function main() {
  var game; // instance of the Game
  var splashScreen; // Start Screen
  var gameOverScreen;

    
  // -- splash screen

  function createSplashScreen() {};

  function removeSplashScreen() {};

    
  // -- game screen

  function createGameScreen() {};

  function removeGameScreen() {};

    
  // -- game over screen

  function createGameOverScreen(score) {};

  function removeGameOverScreen() {};

    
  // -- Setting the game state 

  function startGame() {};

  function gameOver() {};

    
  // -- initialize Splash screen on initial start
  createSplashScreen();
}

// Runs the function `main` once all resources are loaded
window.addEventListener('load', main);
```





<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">5</h2>

Notice that we called the `createSplashScreen` at the end of `main`, therefore lets create that function.







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">6</h2>

### Create functions:

### `buildDom` 

### `createSplashScreen` 

### `removeSplashScreen`



##### `main.js`

```js
// buildDom
function buildDom(htmlString) {
  var div = document.createElement('div');
  div.innerHTML = htmlString;
  return div.children[0];
};
```



```js
// createSplashScreen() - inside main()

  // -- splash screen

  function createSplashScreen() {
    splashScreen = buildDom(`
    <main>
      <h1>Eternal Enemies</h1>
      <button>Start</button>
    </main>
  `);
      
    document.body.appendChild(splashScreen);

    var startButton = splashScreen.querySelector('button');
    startButton.addEventListener('click', function() {
      console.log('You clicked Start!');
        
      // Here we start the game 
    });
  };
```



```js
// removeSplashScreen() - inside main()

  function removeSplashScreen() {
    splashScreen.remove();
  };
```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">7</h2>

### Create `main.js` functions:

### `createGameScreen`

### `removeGameScreen` 

### `startGame`



##### `main.js`

```js
// createGameScreen() - inside main()
  
  // -- game screen

  function createGameScreen() {
    var gameScreen = buildDom(`
    <main class="game container">
      <header>
        <div class="lives">
          <span class="label">Lives:</span>
          <span class="value"></span>
        </div>
        <div class="score">
          <span class="label">Score:</span>
          <span class="value"></span>
        </div>
      </header>
      <div class="canvas-container">
        <canvas></canvas>
      </div>
    </main>
  `);

    document.body.appendChild(gameScreen);
    return gameScreen;
  }

```



```js
// removeGameScreen() - inside main()
  
  function removeGameScreen() {
    game.removeGameScreen();
  }

```



```js
// removeGameScreen() - inside main()

  function startGame() {
    removeSplashScreen();
    // we also need to add clearing of the gameOverScreen

    var gameScreen = createGameScreen();
  }

```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">8</h2>

### Now we can update `startButton` to  call `startGame` when it is clicked.



##### `main.js`

```js
  function createSplashScreen() {

    ...
      ...

    var startButton = splashScreen.querySelector('button');
    //startButton.addEventListener('click', function() {
      //console.log('You clicked Start!');
    //});
    startButton.addEventListener('click', startGame); // <- UPDATE
  }

```











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">9</h2>

### Create a Game constructor 

##### Game constructor is used to create objects that will represent each game played.



##### `game.js`

```js
function Game() {
  this.canvas = null;
  this.ctx = null;
  this.enemies = [];
  this.player = null;
  this.gameIsOver = false;
  this.gameScreen = null;
}


// Create `ctx`, a `player` and start the Canvas loop
Game.prototype.start = function() {};

Game.prototype.startLoop = function() {};

Game.prototype.checkCollisions = function() {};

Game.prototype.updateGameStats = function() {};

Game.prototype.passGameOverCallback = function(callback) {};

Game.prototype.gameOver = function() {};

Game.prototype.removeGameScreen = function() {};


```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">10</h2>

### Create instance of the `Game` in the `startGame()`



##### `main.js`

```js
function startGame() {
  removeSplashScreen();
  // also later we need to add clearing of the gameOverScreen

  //var gameScreen = createGameScreen();
  game = new Game();						//  <- UPDATE
  game.gameScreen = createGameScreen();		//  <- UPDATE

  // Start the game
  // End the game
}

```











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">11</h2>

### Create the `Game.prototype.start` method



##### `game.js`

```js
Game.prototype.start = function() {
  
  // Save reference to canvas and container. Create ctx
  this.canvasContainer = document.querySelector('.canvas-container');
  this.canvas = this.gameScreen.querySelector('canvas');
  this.ctx = this.canvas.getContext('2d');

  // Save reference to the score and lives elements
  this.livesElement = this.gameScreen.querySelector('.lives .value');
  this.scoreElement = this.gameScreen.querySelector('.score .value');

  // Set the canvas dimensions to match the parent
  this.containerWidth = this.canvasContainer.offsetWidth;
  this.containerHeight = this.canvasContainer.offsetHeight;
  this.canvas.setAttribute('width', this.containerWidth);
  this.canvas.setAttribute('height', this.containerHeight);


  // Create a new player for the current game
  this.player = {};

    
  // Add event listener for moving the player
  // ..
    
    
  // Start the canvas requestAnimationFrame loop
  this.startLoop();
};

```













<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">12</h2>

### Add `game.start()` method

### to the `main.js`  `startGame()`



##### `main.js`

```js
function startGame() {
  removeSplashScreen();
  // later we need to add clearing of the gameOverScreen

  game = new Game();
  game.gameScreen = createGameScreen();

  game.start();		//  <-- UPDATE
  // End the game
}

```













<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">13</h2>

### Create the `Player` constructor



##### `player.js`

```js
'use strict';

function Player(canvas, lives) {
  this.canvas = canvas;
  this.ctx = this.canvas.getContext('2d');
  this.lives = lives;
  this.size = 100;
  this.x = 50;
  this.y = canvas.height / 2;
  this.direction = 0;
  this.speed = 5;
}

Player.prototype.setDirection = function(direction) {};

Player.prototype.didCollide = function(enemy) {};

Player.prototype.handleScreenCollision = function() {};

Player.prototype.removeLife = function() {};

Player.prototype.draw = function() {};

```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">14</h2>

### Create methods for player:

### `setDirection`  

### `handleScreenCollision`

### `removeLife` 

### `draw` 



##### `player.js`

```js
// setDirection()

Player.prototype.setDirection = function(direction) {
  // +1 down  -1 up
  if (direction === 'up') this.direction = -1;
  else if (direction === 'down') this.direction = 1;
};

```



```js
// handleScreenCollision()

Player.prototype.handleScreenCollision = function() {
  this.y = this.y + this.direction * this.speed;
  var screenTop = 0;
  var screenBottom = this.canvas.height;

  if (this.y > screenBottom) this.direction = -1;
  else if (this.y < screenTop) this.direction = 1;
};

```



```js
// removeLife()

Player.prototype.removeLife = function() {
  this.lives -= 1;
};

```



```js
// draw()

Player.prototype.draw = function() {
  this.ctx.fillStyle = '#66D3FA';
  // fillRect(x, y, width, height)
  this.ctx.fillRect(
    this.x,
    this.y,
    this.size,
    this.size,
  );
};

```











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">15</h2>

### Update method in `game.js` - `Game.prototype.start()`



##### 1. Create Player instance 

##### 2. Create `handleKeyDown` function

##### 2.  Add event listener, with callback - `handleKeyDown` 

##### 3.  Bind event callback  `handleKeyDown` 



##### `game.js`

```js
// start()

Game.prototype.start = function() {
  
...
	...
		...
 

  // this.player = {};
  this.player = new Player();		//	<-- UPDATE
    
    
  // Event listener callback function
  this.handleKeyDown = function(event) {
      
    if (event.key === 'ArrowUp') {
      console.log('UP');
      this.player.setDirection('up');  
    } 
    else if (event.key === 'ArrowDown') {
      console.log('DOWN');
      this.player.setDirection('down');
    }
  };
    
  // Add event listener for moving the player
  document.body.addEventListener(
      'keydown', 
      this.handleKeyDown.bind(this)
  );
  // Any function provided to eventListener 
  // is always called by window (this === window)!
  // So, we have to bind `this` to the `game` object,
  // to prevent it from pointing to the `window` object
    
    
  // Start the canvas requestAnimationFrame loop
  this.startLoop();
};

```











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">16</h2>

### If we try starting the game, we can press UP and DOWN keys, 

### but we will not see the player ? 

### Why is that?



...



### Because we are missing the game loop!













<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">17</h2>

### Before we create the loop, let's create the last constructor we will need - for the enemy



##### `enemy.js`

```js
'use strict';

function Enemy(canvas, y, speed) {
  this.canvas = canvas;
  this.ctx = canvas.getContext('2d');
  this.size = 20;
  this.x = canvas.width + this.size;
  this.y = y;
  this.speed = speed;
}

Enemy.prototype.draw = function() {};

Enemy.prototype.updatePosition = function() {};

Enemy.prototype.isInsideScreen = function() {};

```















<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">18</h2>

### Create the `Enemy` methods :

### `draw`

### `updatePosition`

### `isInsideScreen`



##### `enemy.js`

```js
// draw()

Enemy.prototype.draw = function() {
  this.ctx.fillStyle = '#FF6F27';
  // fillRect(x, y, width, height)
  this.ctx.fillRect(
    this.x,
    this.y,
    this.size,
    this.size,
  );
};

```



```js
// updatePosition()

Enemy.prototype.updatePosition = function() {
  this.x = this.x - this.speed;
};

```



```js
// isInsideScreen()

Enemy.prototype.isInsideScreen = function() {
  // if x plus half of its size is smaller then 0 return
  return this.x + this.size / 2 > 0;
};

```













<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">19</h2>

### Let's create the game loop



##### `game.js`

```js
// startLoop()

Game.prototype.startLoop = function() {
  var loop = function() {
    console.log('in loop');
      
    // EVERYTHING HAPPENS HERE !

    if (!this.gameIsOver) {
      window.requestAnimationFrame(loop);
    }
  }.bind(this);

// As loop function will be continuously invoked by
// the `window` object- `window.requestAnimationFrame(loop)`
// we have to bind the function so that value of `this` is 
// pointing to the `game` object, like this:
// var loop = (function(){}).bind(this);

  window.requestAnimationFrame(loop);
};

```







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">20</h2>

### We can now test the loop by checking the `console` in the browser.











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">21</h2>

### Let's line out by using comments `//`, step by step what operations will be happening in the loop.





<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">22</h2>

## `TEAM ACTIVITY`

#### Separate group in teams and give 10 minutes to come up when will each function be called, to ensure old things are cleared from canvas and new updated player and enemies are rendered on each loop call.



### [Team Activity gist with the task](https://gist.github.com/ross-u/6768a8dadceb70198a4bbea1dff4d15c)











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">23</h2>

### Lets now write these comments in our `loop` function



```js
Game.prototype.startLoop = function() {
  var loop = function() {
    
// 1. UPDATE THE STATE OF PLAYER AND ENEMIES
  
    // 0. Our player was already created - via `game.start()`

    // 1. Create new enemies randomly

    // 2. Check if player had hit any enemy (check all enemies)

    // 3. Check if player is going off the screen

    // 4. Move existing enemies

    // 5. Check if any enemy is going of the screen


// 2. CLEAR THE CANVAS


// 3. UPDATE THE CANVAS
    // Draw the player

    // Draw the enemies

// 4. TERMINATE LOOP IF GAME IS OVER
    if (!this.gameIsOver) {
      window.requestAnimationFrame(loop);
    }
  }.bind(this);

  // As loop function will be continuously invoked by
  // the `window` object- `window.requestAnimationFrame(loop)`
  // we have to bind the function so that value of `this` is
  // pointing to the `game` object, like this:
  // var loop = (function(){}).bind(this);

  window.requestAnimationFrame(loop);
};


```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">24</h2>

### Let's now write the code for each comment

##### `game.js`

```js
Game.prototype.startLoop = function() {
  var loop = function() {
// 1. UPDATE THE STATE OF PLAYER AND ENEMIES

    // 0. Our player was already created - via `game.start()`

    // 1. Create new enemies randomly
    if (Math.random() > 0.98) {
      var randomY = this.canvas.height * Math.random();
      var newEnemy = new Enemy(this.canvas, randomY, 5);
      this.enemies.push(newEnemy);
    }

    // 2. Check if player had hit any enemy (check all enemies)
    this.checkCollisions();

    // 3. Check if player is going off the screen
    this.player.handleScreenCollision();

    // 4. Move existing enemies
    // 5. Check if any enemy is going of the screen
    this.enemies = this.enemies.filter(function(enemy) {
      enemy.updatePosition();
      return enemy.isInsideScreen();
    });

      
// 2. CLEAR THE CANVAS
   this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);

      
// 3. UPDATE THE CANVAS
    // Draw the player
    this.player.draw();

    // Draw the enemies
    this.enemies.forEach(function(enemy) {
      enemy.draw();
    });

// 4. TERMINATE LOOP IF GAME IS OVER
    if (!this.gameIsOver) {
      window.requestAnimationFrame(loop);
    }
      
  }.bind(this);

  // As loop function will be continuously invoked by
  // the `window` object- `window.requestAnimationFrame(loop)`
  // we have to bind the function so that value of `this` is
  // pointing to the `game` object, like this:
  // var loop = (function(){}).bind(this);

  window.requestAnimationFrame(loop);
};

```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">25</h2>

#### If we run the game now, we will see that all works fine, except for the collisions (which we didn't implement yet).











<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">26</h2>

### Implement the `player` and `enemies` collision checking



##### Our loop is calling the `checkCollisions` but we don't have any functionality in that function. Let's update it.



##### `game.js`

```js
// checkCollisions()

Game.prototype.checkCollisions = function() {
  
  this.enemies.forEach( function(enemy) {
    
    if ( this.player.didCollide(enemy) ) {

      this.player.removeLife();
      console.log('lives', this.player.lives);
      
      // Move the enemy off screen to the left
      enemy.x = 0 - enemy.size;

      if (this.player.lives === 0) {
        this.gameOver();
      }
    }
  }, this);
  // We have to bind `this`
  // as array method callbacks have a default `this` of undefined.
};

```







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">27</h2>

### Implement the `didColide()` method in `player.js` checking the player sides for collision.



##### `player.js`

```js
Player.prototype.didCollide = function(enemy) {
  var playerLeft = this.x;
  var playerRight = this.x + this.size;
  var playerTop = this.y;
  var playerBottom = this.y + this.size;

  var enemyLeft = enemy.x;
  var enemyRight = enemy.x + enemy.size;
  var enemyTop = enemy.y;
  var enemyBottom = enemy.y + enemy.size;

  // Check if the enemy intersects any of the player's sides
  var crossLeft = enemyLeft <= playerRight && enemyLeft >= playerLeft;
    
  var crossRight = enemyRight >= playerLeft && enemyRight <= playerRight;
  
  var crossBottom = enemyBottom >= playerTop && enemyBottom <= playerBottom;
  
  var crossTop = enemyTop <= playerBottom && enemyTop >= playerTop;

  if ((crossLeft || crossRight) && (crossTop || crossBottom)) {
    return true;
  }
  return false;
};

```







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">28</h2>

### Implement the `gameOver()` method 





##### `game.js`

```js
// gameOver()

Game.prototype.gameOver = function() {
  this.gameIsOver = true;
    
  console.log('GAME OVER');
  // Call the gameOver function from `main` to show the Game Over Screen
  //...
};

```





<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">29</h2>

### In order to get access to the function from the `main.js` we will pass it as a callback to our `game` object when new game is created.



##### `main.js`

```js
// main.js	startGame()

function startGame() {
  removeSplashScreen();
  removeGameOverScreen();

  game = new Game();
  game.gameScreen = createGameScreen();

  game.start();
  // End the game
  game.passGameOverCallback( function() {		//	<-- UPDATE
    gameOver();
  });
}

```



```js
// main.js	gameOver()

  // -- game over
  function gameOver(score) {
    removeGameScreen();
    createGameOverScreen();
  }

```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">30</h2>

### Create the `removeGameScreen()` method in `game.js`, which removes the entire game DOM element



##### `game.js`

```js
//	game.js	 removeGameScreen()

Game.prototype.removeGameScreen = function() {
  this.gameScreen.remove();
};

```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">31</h2>

### Create a `createGameOverScreen` method and add event listener for restarting and creating a new game



##### `main.js`

```js
function createGameOverScreen(score) {
  gameOverScreen = buildDom(`
    <main>
      <h1>Game over</h1>
      <p>Your score: <span></span></p>
      <button>Restart</button>
  	</main>
  `);

  var button = gameOverScreen.querySelector('button');
  button.addEventListener('click', startGame);

  var span = gameOverScreen.querySelector('span');
  span.innerText = score;

  document.body.appendChild(gameOverScreen);
}

```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">32</h2>

### If we try to restart the game we will see that Game Over screen is not being removed.

### We need to implement the `removeGameOverScreen()` method in `main.js`.



##### `main.js`

```js
// main.js	removeGameOverScreen()

function removeGameOverScreen() {
  if (gameOverScreen) {
    gameOverScreen.remove();
  }
}

```



```js
// main.js	startGame()

function startGame() {
  removeSplashScreen();
  removeGameOverScreen();	//		<--  UPDATE

  game = new Game();
  game.gameScreen = createGameScreen();

  game.start();
  game.passGameOverCallback(gameOver);
}


```









<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">33</h2>

### For the end implement the game statuses - `lives` remaining and the `score`.







### Implement `updateGameStats()` method and call it on each loop iteration



##### `game.js`

```js
// 	game.js		updateGameStats()

Game.prototype.updateGameStats = function() {
  this.score += 1;
  this.livesElement.innerHTML = this.player.lives;
  this.scoreElement.innerHTML = this.score;
};

```



```js
// 	game.js		startLoop()

Game.prototype.startLoop = function() {
  var loop = function() {

   ...
   
   		...
   
   			...
   
    // 4. TERMINATE LOOP IF GAME IS OVER
    if (!this.gameIsOver) {
      window.requestAnimationFrame(loop);
    }

    //  5. Update Game data/stats
    this.updateGameStats();					//	<- UPDATE
      
  }.bind(this);

  // As loop function will be continuously invoked by
  // the `window` object- `window.requestAnimationFrame(loop)`
  // we have to bind the function so that value of `this` is
  // pointing to the `game` object, like this:
  // var loop = (function(){}).bind(this);

  window.requestAnimationFrame(loop);
};

```







<h2 style="background-color: #66D3FA; color: white; display: inline; padding: 10px; border-radius: 10;">34</h2>

### Implement the proper score rendering on the Game Over screen



##### `main.js`

```js
// main.js		startGame()

function startGame() {
  removeSplashScreen();
  // later we need to add clearing of the gameOverScreen
  removeGameOverScreen();

  game = new Game();
  game.gameScreen = createGameScreen();

  game.start();
  // End the game
  game.passGameOverCallback( function() {		// <-- UPDATE
    gameOver(game.score);					// <-- UPDATE
  });
}

```



```js
// main.js		gameOver()

function gameOver(score) {
  removeGameScreen();
  createGameOverScreen(score);
}

```







<h2 style="background-color: green; color: white; display: inline; padding: 10px; border-radius: 10;">THE END</h2>

### MISSION ACCOMPLISHED! :heavy_check_mark: :thumbsup:

### WELL DONE !  :rocket: :confetti_ball: :rocket: :confetti_ball: