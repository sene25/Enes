<h1>Merhaba 👋</h1>  
<p>Ben <strong>sene25</strong></p>

<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Top Sektirme Oyunu</title>
  <style>
    body {
      margin: 0;
      background-color: #f0f0f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    canvas {
      border: 2px solid black;
      background-color: white;
    }
  </style>
</head>
<body>
  <canvas id="canvas" width="400" height="600"></canvas>

  <script>
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");

    let ball = {
      x: 200,
      y: 300,
      radius: 20,
      color: "red",
      dy: 0,
      gravity: 0.5,
      bounce: -10
    };

    function drawBall() {
      ctx.beginPath();
      ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
      ctx.fillStyle = ball.color;
      ctx.fill();
      ctx.closePath();
    }

    function update() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawBall();

      ball.dy += ball.gravity;
      ball.y += ball.dy;

      // Aşağı zıplama
      if (ball.y + ball.radius > canvas.height) {
        ball.y = canvas.height - ball.radius;
        ball.dy = ball.bounce;
      }

      requestAnimationFrame(update);
    }

    canvas.addEventListener("click", function (e) {
      let rect = canvas.getBoundingClientRect();
      let clickX = e.clientX - rect.left;
      let clickY = e.clientY - rect.top;

      let dx = clickX - ball.x;
      let dy = clickY - ball.y;
      let distance = Math.sqrt(dx * dx + dy * dy);

      if (distance < ball.radius) {
        ball.dy = ball.bounce;
      }
    });

    update();
  </script>
</body>
</html>
