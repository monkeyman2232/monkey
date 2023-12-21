2. JavaScript Code (script.js):

JavaScript
// Get a reference to the canvas element
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

// Game objects
const ball = {
  x: canvas.width / 2,
  y: canvas.height / 2,
  radius: 10,
  dx: 4,
  dy: 4,
};

const paddle1 = {
  x: 0,
  y: canvas.height / 2 - 50,
  width: 10,
  height: 100,
};

const paddle2 = {
  x: canvas.width - 10,
  y: canvas.height / 2 - 50,
  width: 10,
  height: 100,
};

// Score
let score1 = 0;
let score2 = 0;

// Function to draw objects
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height); // Clear the canvas

  // Draw ball
  ctx.fillStyle = "red";
  ctx.beginPath();
  ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
  ctx.fill();

  // Draw paddles
  ctx.fillStyle = "blue";
  ctx.fillRect(paddle1.x, paddle1.y, paddle1.width, paddle1.height);
  ctx.fillRect(paddle2.x, paddle2.y, paddle2.width, paddle2.height);

  // Draw score
  ctx.font = "24px Arial";
  ctx.fillStyle = "black";
  ctx.fillText(score1, 50, 50);
  ctx.fillText(score2, canvas.width - 50, 50);
}

// Function to update game objects
function update() {
  // Ball movement
  ball.x += ball.dx;
  ball.y += ball.dy;

  // Wall collision
  if (ball.y + ball.radius > canvas.height || ball.y - ball.radius < 0) {
    ball.dy *= -1;
  }

  // Paddle collision
  if (
    ball.x + ball.radius > paddle1.x &&
    ball.x - ball.radius < paddle1.x + paddle1.width &&
    ball.y + ball.radius > paddle1.y &&
    ball.y - ball.radius < paddle1.y + paddle1.height
  ) {
    ball.dx *= -1;
  } else if (
    ball.x + ball.radius > paddle2.x &&
    ball.x - ball.radius < paddle2.x + paddle2.width &&
    ball.y + ball.radius > paddle2.y &&
    ball.y - ball.radius < paddle2.y + paddle2.height
  ) {
    ball.dx *= -1;
  }

  // Scorekeeping
  if (ball.x + ball.radius > canvas.width) {
    score1++;
    ball.x = canvas.width / 2;
    ball.y = canvas.height / 2;
  } else if (ball.x - ball.radius < 0) {
    score2++;
    ball.x = canvas.width / 2;
    ball.y = canvas.height / 2;
  }
}

// Keyboard controls
document.addEventListener("keydown", function (event) {
  // Paddle 1 controls
  if (event.code === "KeyW") {
    paddle1.y -= 10;
  } else if (event.code === "KeyS
