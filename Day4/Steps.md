	1. git init
	2. git commit -am "initial commit"
2. Add index.html
3. Link style.css & game.js
4. Create a HTML5 canvas element
5. Add the css styles
	```css
* {

box-sizing: border-box;

margin: 0;

padding: 0;

}


#canvas {

border: 1px solid black;

position: absolute;

z-index: 200;

top: 50%;

left: 50%;

translate: -50% -50%;

background-image: url('./sprites/background-day.png');

background-repeat: no-repeat;

background-size: cover;

background-position: center;

}
```

6. Make the Game class in game.js
	```JavaScript
class Game {

constructor(canvas, ctx) {

this.canvas = canvas;

this.ctx = ctx;

this.isGameOver = false;

this.score = 0;

this.highScore = JSON.parse(localStorage.getItem('highscore'));

this.height = canvas.height;

this.width = canvas.width;

this.gameFrame = 0;

this.staggerFrames = 5;

this.bird = new Bird(this);

  

this.numberOfObstacles = 4;

this.obstaclePool = [];

this.obstacleTimer = 0;

this.obstacleInterval = 1200;

  

this.createObstaclePool();

  

this.start();

window.addEventListener("resize", () => {

this.resize(Background.width, Background.height);

});

window.addEventListener("click", () => {

this.bird.fly();

});

}

  

// collisionDetection(rect1, rect2) {

// if (rect1.x > rect2.x + rect2.width ||

// rect1.y > rect2.y + rect2.height ||

// rect1.x + rect1.width < rect2.x ||

// rect1.y + rect1.height < rect2.y

// ) {

// return false;

// } else {

// return true;

// }

// }

collisionDetection(bird, obstacle) {

// Top part of the obstacle

const topObstacle = {

x: obstacle.x,

y: obstacle.y,

width: obstacle.width,

height: obstacle.height

};

  

// Bottom part of the obstacle (after the gap)

const bottomObstacle = {

x: obstacle.x,

y: obstacle.y + obstacle.height + obstacle.gapHeight,

width: obstacle.width,

height: obstacle.height

};

  

// Check collision with top obstacle

const collisionWithTop = (

bird.x < topObstacle.x + topObstacle.width &&

bird.x + bird.sw > topObstacle.x &&

bird.y < topObstacle.y + topObstacle.height &&

bird.y + bird.sh > topObstacle.y

);

  

// Check collision with bottom obstacle

const collisionWithBottom = (

bird.x < bottomObstacle.x + bottomObstacle.width &&

bird.x + bird.sw > bottomObstacle.x &&

bird.y < bottomObstacle.y + bottomObstacle.height &&

bird.y + bird.sh > bottomObstacle.y

);

  

if (collisionWithTop || collisionWithBottom) {

this.isGameOver = true;

}

  

return collisionWithTop || collisionWithBottom;

}

  

calculateHighScore() {

if (this.score > this.highScore) {

this.highScore = this.score;

localStorage.setItem('highscore', JSON.stringify(this.highScore));

}

}

  

drawScoreText() {

this.ctx.save();

this.ctx.fillStyle = 'white';

this.ctx.font = '60px "Tiny5"';

  

const scoreText = `${this.score} ${this.highScore}`;

const scoreTextWidth = this.ctx.measureText(scoreText).width;

  
  

const scoreX = (this.width / 2) - (scoreTextWidth / 2);

const scoreY = this.height * .1;

  

this.ctx.fillText(scoreText, scoreX, scoreY);

this.ctx.restore()

}

  

createObstaclePool() {

for (let i = 0; i < this.numberOfObstacles; i++) {

this.obstaclePool.push(new Obstacle(this));

}

}

getObstacles() {

for (let i = 0; i < this.numberOfObstacles; i++) {

if (this.obstaclePool[i].available) return this.obstaclePool[i];

}

return null;

}

handleObstacles(deltaTime) {

if (this.obstacleTimer < this.obstacleInterval) {

this.obstacleTimer += deltaTime;

} else {

this.obstacleTimer = 0;

const obstacle = this.getObstacles();

if (obstacle) {

obstacle.start();

}

}

}

  

start() {

this.resize(Background.width, Background.height);

this.gameOver = false;

this.score = 0;

}

  

gameOver() {

return this.isGameOver;

}

  

resize(width, height) {

this.canvas.width = width;

this.canvas.height = height;

this.width = width;

this.height = height;

}

render(deltaTime) {

this.handleObstacles(deltaTime);

this.obstaclePool.forEach((obstacle) => {

obstacle.update(deltaTime);

obstacle.draw();

});

this.bird.update(deltaTime);

this.bird.draw();

this.drawScoreText()

}

}
```

7. Create Obstacle class.
	```js
	class Obstacle {
    constructor(game) {
        this.game = game;
        this.image = PipeImage;
        this.width = this.image.width;
        this.height = this.image.height;
        this.gapHeight = this.game.bird.sh * 3;  // Adjust gap height based on bird's size
        this.x = this.game.width + this.width;  // Start obstacle off-screen
        this.y = Math.floor(Math.random() * - this.height * .75) + 0;
        this.speedX = -2;
        this.available = true;
    }

    start() {
        this.available = false;
        this.x = this.game.width + this.width;
        this.y = Math.floor(Math.random() * - this.height * .75) + 0;
        // console.log('start')
    }

    restart() {
        this.available = true;
        // console.log('restart');
    }

    update(deltaTime) {
        if (!this.available) {
            this.x += this.speedX * (deltaTime / 10);
            // console.log('update', this.x)
            if (this.x <= 0 - this.width) {
                this.game.score++;
                this.restart();
            }

            if (this.game.collisionDetection(this.game.bird, this)) {
                this.game.bird.y = this.game.height;
            }
        }
    }

    draw() {
        if (!this.available) {
            const ctx = this.game.ctx;

            ctx.save();

            ctx.translate(this.x + this.width / 2, this.y + this.height / 2);
            ctx.rotate(Math.PI);
            ctx.drawImage(this.image, -this.width / 2, -this.height / 2, this.width, this.height);

            ctx.restore();

            ctx.beginPath();
            ctx.fillStyle = 'blue';
            ctx.drawImage(this.image, this.x, this.y + this.height + this.gapHeight, this.width, this.height);
            ctx.fill();
            ctx.closePath();
        }
    }

}
```

8. Learn what is object pool method
	```js
	this.numberOfObstacles = 4;
        this.obstaclePool = [];
        this.obstacleTimer = 0;
        this.obstacleInterval = 1200;
    this.createObstaclePool();
    
createObstaclePool() {

for (let i = 0; i < this.numberOfObstacles; i++) {

this.obstaclePool.push(new Obstacle(this));

}

}

getObstacles() {

for (let i = 0; i < this.numberOfObstacles; i++) {

if (this.obstaclePool[i].available) return this.obstaclePool[i];

}

return null;

}

handleObstacles(deltaTime) {

// console.log(deltaTime, 'sljf')

if (this.obstacleTimer < this.obstacleInterval) {

this.obstacleTimer += deltaTime;

} else {

this.obstacleTimer = 0;

const obstacle = this.getObstacles();

if (obstacle) {

obstacle.start();

}

}

}

this.handleObstacles(deltaTime);

this.obstaclePool.forEach((obstacle) => {

obstacle.update(deltaTime);

obstacle.draw();

});
```

9. Create Bird class
	```js
	class Bird {
    constructor(game) {
        this.game = game;
        this.image = BirdImage;
        this.x = this.game.width * 0.25;
        this.y = this.game.height * 0.5;
        this.frameX = 0;
        // sw = source width
        this.sw = 45;
        this.sh = 45;
        this.sy = 0;
        this.speedY = 0;
        this.gravity = 0.35;
        this.lift = -5;
    }
    fly() {
        this.speedY = this.lift;
    }
    update(deltaTime) {
        this.speedY += this.gravity;
        this.y += this.speedY * deltaTime / 10;

        // Constraints
        if (this.y + this.sh >= this.game.height) {
            this.y = this.game.height - this.sh;
            this.speedY = 0;
            this.frameX = 0;
        }
        if (this.y <= 0) {
            this.y = 0;
            this.speedY = 0;
        }
    }
    draw() {
        this.game.ctx.save();

        this.game.ctx.beginPath();
        this.game.ctx.fillStyle = "yellow";
        this.game.ctx.drawImage(this.image, this.frameX * this.sw, this.sy, this.sw, this.sh, this.x, this.y, this.sw, this.sh);
        if (this.game.gameFrame % this.game.staggerFrames == 0) {
            if (this.frameX < 2) {
                this.frameX++;
            } else {
                this.frameX = 0;
            }
        }
        this.game.gameFrame++;
        this.game.ctx.fill();
        this.game.ctx.restore();
    }
}
```
10. Learn about sprite sheet animation
	```js
	this.frameX = 0;
        // sw = source width
        this.sw = 45;
        this.sh = 45;
        this.sy = 0;
        
	this.game.ctx.drawImage(this.image, this.frameX * this.sw, this.sy, this.sw, this.sh, this.x, this.y, this.sw, this.sh);
        if (this.game.gameFrame % this.game.staggerFrames == 0) {
            if (this.frameX < 2) {
                this.frameX++;
            } else {
                this.frameX = 0;
            }
        }
        this.game.gameFrame++;
```

11. Implement collision detection
	```js
	// collision detection for two rectangles
	collisionDetection(rect1, rect2) {

if (rect1.x > rect2.x + rect2.width ||

rect1.y > rect2.y + rect2.height ||

rect1.x + rect1.width < rect2.x ||

rect1.y + rect1.height < rect2.y

) {

return false;

} else {

return true;

}

}


// Collision detection for our case.
collisionDetection(bird, obstacle) {

// Top part of the obstacle

const topObstacle = {

x: obstacle.x,

y: obstacle.y,

width: obstacle.width,

height: obstacle.height

};

  

// Bottom part of the obstacle (after the gap)

const bottomObstacle = {

x: obstacle.x,

y: obstacle.y + obstacle.height + obstacle.gapHeight,

width: obstacle.width,

height: obstacle.height

};

  

// Check collision with top obstacle

const collisionWithTop = (

bird.x > topObstacle.x + topObstacle.width ||

bird.x + bird.sw < topObstacle.x ||

bird.y > topObstacle.y + topObstacle.height ||

bird.y + bird.sh < topObstacle.y

);

  

// Check collision with bottom obstacle

const collisionWithBottom = (

bird.x > bottomObstacle.x + bottomObstacle.width ||

bird.x + bird.sw < bottomObstacle.x ||

bird.y > bottomObstacle.y + bottomObstacle.height ||

bird.y + bird.sh < bottomObstacle.y

);

  

if (!collisionWithTop || !collisionWithBottom) {

this.isGameOver = true;

}

  

return !collisionWithTop || !collisionWithBottom;

}
```

