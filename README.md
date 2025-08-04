<h1>Merhaba 👋</h1>  
<p>Ben <strong>sene25</strong></p>


<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Top Sektirme Oyunu</title>
  <style>
    canvas {
      background: #f0f0f0;
      display: block;
      margin: 50px auto;
      border: 2px solid #000;
    }
  </style>
</head>
<body>
  <canvas id="game" width="400" height="600"></canvas>
  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");

    let x = canvas.width / 2;
    let y = canvas.height / 2;
    let dy = 2;
    let gravity = 0.4;
    let bounce = -8;
    const radius = 20;

    function drawBall() {
      ctx.beginPath();
      ctx.arc(x, y, radius, 0, Math.PI * 2);
      ctx.fillStyle = "red";
      ctx.fill();
      ctx.closePath();
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawBall();

      dy += gravity;
      y += dy;

      if (y + radius > canvas.height) {
        y = canvas.height - radius;
        dy = bounce;
      }

      requestAnimationFrame(draw);
    }

    canvas.addEventListener("click", function(e) {
      const rect = canvas.getBoundingClientRect();
      const mx = e.clientX - rect.left;
      const my = e.clientY - rect.top;
      const dist = Math.sqrt((mx - x) ** 2 + (my - y) ** 2);

      if (dist < radius) {
        dy = bounce;
      }
    });

    draw();
  </script>
</body>
</html>
