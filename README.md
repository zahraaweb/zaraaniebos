<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Adventure With You</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #fff0f5;
      font-family: 'Comic Sans MS', cursive;
      overflow: hidden;
      text-align: center;
    }
    h1 {
      margin-top: 50px;
      color: #ff69b4;
      font-size: 2.5rem;
    }
    #message {
      font-size: 1.5rem;
      color: #d81b60;
      margin-top: 30px;
    }
    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 1;
    }
    audio {
      display: none;
    }
  </style>
</head>
<body>

<h1>Our Adventure Together...</h1>
<div id="message">Click anywhere to start the magic!</div>

<canvas id="canvas"></canvas>

<audio id="bgm" autoplay loop>
  <source src="https://www.bensound.com/bensound-music/bensound-sunny.mp3" type="audio/mpeg">
</audio>

<script>
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');
  const bgm = document.getElementById('bgm');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  let hearts = [];
  const messages = [
    "Dari zahra untuk zahra!",
    "I love your smile!",
    "You light up my world!",
    "You are my sunshine!",
    "You’re the Zahra in my life, the one who makes everything better.",
    "Your laughter is my favorite sound!",
    "You're my ride or die!",
    "You're my best adventure!",
    "Every day with you is a blessing!"
  ];
  let clickCount = 0;

  window.addEventListener('resize', () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  });

  window.addEventListener('click', (e) => {
    createHeart(e.clientX, e.clientY);
    showMessage();
    clickCount++;
    if (clickCount === 10) {
      setTimeout(() => {
        alert("Will you be my partner forever?");
      }, 300);
    }
  });

  function createHeart(x, y) {
    hearts.push({ x, y, size: 30, alpha: 1, speedY: Math.random() * 1 + 1 });
  }

  function showMessage() {
    const msg = messages[Math.floor(Math.random() * messages.length)];
    document.getElementById('message').innerText = msg;
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    hearts.forEach((heart, index) => {
      ctx.globalAlpha = heart.alpha;
      ctx.fillStyle = "#ff69b4";
      ctx.beginPath();
      ctx.moveTo(heart.x, heart.y);
      ctx.bezierCurveTo(heart.x + 20, heart.y - 20, heart.x + 40, heart.y + 10, heart.x, heart.y + 40);
      ctx.bezierCurveTo(heart.x - 40, heart.y + 10, heart.x - 20, heart.y - 20, heart.x, heart.y);
      ctx.fill();
      heart.y -= heart.speedY;
      heart.alpha -= 0.005;
      if (heart.alpha <= 0) {
        hearts.splice(index, 1);
      }
    });
    requestAnimationFrame(animate);
  }

  animate();
</script>

</body>
</html>