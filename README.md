<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Apple Store Demo Loop</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      overflow: hidden;
    }

    body, html {
      width: 100%;
      height: 100%;
      background-color: #000;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", "Helvetica Neue", sans-serif;
    }

    /* Фоновый холст для плавной генерации градиентов */
    canvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
      filter: blur(40px); /* Фирменный мягкий размытый эффект Apple */
      transform: scale(1.2); /* Избавляемся от белых краев из-за blur */
    }

    /* Оверлей с текстом и графикой */
    .overlay {
      position: relative;
      z-index: 2;
      color: #ffffff;
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      height: 80vh;
      width: 90%;
      pointer-events: none;
    }

    .header-logo {
      font-size: 3rem;
      font-weight: 600;
      letter-spacing: -0.02em;
      opacity: 0.9;
    }

    .main-title {
      font-size: 3.5rem;
      font-weight: 700;
      letter-spacing: -0.03em;
      background: linear-gradient(180deg, #FFFFFF 0%, rgba(255, 255, 255, 0.7) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      animation: pulseText 4s ease-in-out infinite alternate;
    }

    .footer-text {
      font-size: 1.2rem;
      font-weight: 400;
      opacity: 0.6;
      letter-spacing: 0.05em;
      text-transform: uppercase;
    }

    @keyframes pulseText {
      0% {
        transform: scale(0.98);
        opacity: 0.85;
      }
      100% {
        transform: scale(1.02);
        opacity: 1;
      }
    }
  </style>
</head>
<body>

  <!-- Холст для жидких переливающихся шаров -->
  <canvas id="demoCanvas"></canvas>

  <!-- Поверхностная эстетика в стиле Apple -->
  <div class="overlay">
    <div class="header-logo"></div>
    <div class="main-title">iPhone</div>
    <div class="footer-text">Нажмите, чтобы начать</div>
  </div>

  <script>
    const canvas = document.getElementById('demoCanvas');
    const ctx = canvas.getContext('2d');

    let width, height;

    function resize() {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resize);
    resize();

    // Создаем несколько светящихся сферы для симуляции жидкого градиента (Liquid Mesh Gradient)
    const blobs = [
      { x: 0, y: 0, r: 0, color: 'rgba(255, 45, 85, ', vx: 0.002, vy: 0.003, angle: 0 },   // Neon Pink
      { x: 0, y: 0, r: 0, color: 'rgba(88, 86, 214, ', vx: 0.003, vy: 0.002, angle: 2 },   // Purple
      { x: 0, y: 0, r: 0, color: 'rgba(0, 122, 255, ', vx: 0.001, vy: 0.004, angle: 4 },   // Apple Blue
      { x: 0, y: 0, r: 0, color: 'rgba(255, 149, 0, ', vx: 0.004, vy: 0.001, angle: 1 }    // Orange
    ];

    function animate() {
      ctx.fillStyle = '#000000';
      ctx.fillRect(0, 0, width, height);

      const baseRadius = Math.max(width, height) * 0.45;

      blobs.forEach((blob, index) => {
        // Синусоидальное движение по экрану
        blob.angle += 0.008;
        const x = width / 2 + Math.sin(blob.angle * blob.vx * 100) * (width * 0.35);
        const y = height / 2 + Math.cos(blob.angle * blob.vy * 100) * (height * 0.35);

        // Градиент свечения для каждой сферы
        const gradient = ctx.createRadialGradient(x, y, 0, x, y, baseRadius);
        gradient.addColorStop(0, blob.color + '0.85)');
        gradient.addColorStop(0.5, blob.color + '0.3)');
        gradient.addColorStop(1, 'rgba(0,0,0,0)');

        ctx.fillStyle = gradient;
        ctx.beginPath();
        ctx.arc(x, y, baseRadius, 0, Math.PI * 2);
        ctx.fill();
      });

      requestAnimationFrame(animate);
    }

    animate();
  </script>
</body>
</html>
 
