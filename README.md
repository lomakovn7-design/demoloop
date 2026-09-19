<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Apple Demo Loop Mockup</title>
  <style>
    :root {
      --bg-color: #f2f2f7;
      --card-bg: rgba(255, 255, 255, 0.8);
      --accent: #007aff;
      --text: #1c1c1e;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background-color: var(--bg-color);
      color: var(--text);
      margin: 0;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }

    .device-selector {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      background: #e5e5ea;
      padding: 4px;
      border-radius: 12px;
    }

    .device-btn {
      border: none;
      background: transparent;
      padding: 8px 16px;
      border-radius: 8px;
      font-weight: 600;
      font-size: 14px;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .device-btn.active {
      background: #ffffff;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .demo-card {
      width: 100%;
      max-width: 360px;
      background: var(--card-bg);
      backdrop-filter: blur(20px);
      border-radius: 24px;
      padding: 24px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.08);
      text-align: center;
      box-sizing: border-box;
    }

    .mascot {
      width: 100px;
      height: 100px;
      margin: 0 auto 16px;
      background: #e1f0ff;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 48px;
    }

    h1 {
      font-size: 22px;
      margin: 0 0 6px;
      font-weight: 700;
    }

    p.subtitle {
      color: #8e8e93;
      font-size: 14px;
      margin: 0 0 20px;
    }

    .controls-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 20px;
    }

    .action-btn {
      border: 1px solid rgba(0,0,0,0.1);
      background: #ffffff;
      padding: 12px;
      border-radius: 12px;
      font-size: 14px;
      font-weight: 600;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      cursor: pointer;
    }

    .log-window {
      background: #ffffff;
      border-radius: 12px;
      padding: 12px;
      font-family: monospace;
      font-size: 11px;
      text-align: left;
      color: #3a3a3c;
      height: 90px;
      overflow-y: auto;
      border: 1px solid rgba(0,0,0,0.05);
    }
  </style>
</head>
<body>

  <div class="device-selector">
    <button class="device-btn active" onclick="setDevice('iPhone', '📱')">iPhone</button>
    <button class="device-btn" onclick="setDevice('iPad', '📱')">iPad</button>
    <button class="device-btn" onclick="setDevice('MacBook', '💻')">MacBook</button>
  </div>

  <div class="demo-card">
    <div class="mascot" id="deviceIcon">📱</div>
    <h1 id="titleText">iPhone Demo Loop</h1>
    <p class="subtitle" id="subtitleText">Интерактивный режим демонстрации Apple</p>

    <div class="controls-grid">
      <button class="action-btn" onclick="addLog('Старт демонстрации...')">▶️ Старт</button>
      <button class="action-btn" onclick="addLog('Демонстрация остановлена')">⏹ Стоп</button>
      <button class="action-btn" onclick="addLog('Пауза')">⏸ Пауза</button>
      <button class="action-btn" onclick="addLog('Открыты настройки')">⚙️ Настройки</button>
    </div>

    <div class="log-window" id="logBox">
      <div>[System] Инициализация демо-режима...</div>
    </div>
  </div>

  <script>
    function setDevice(name, icon) {
      document.querySelectorAll('.device-btn').forEach(btn => btn.classList.remove('active'));
      event.target.classList.add('active');
      
      document.getElementById('deviceIcon').innerText = icon;
      document.getElementById('titleText').innerText = name + ' Demo Loop';
      document.getElementById('subtitleText').innerText = 'Режим демонстрации для ' + name;
      
      addLog('Переключено на ' + name);
    }

    function addLog(message) {
      const logBox = document.getElementById('logBox');
      const time = new Date().toLocaleTimeString();
      logBox.innerHTML += `<div>[${time}] ${message}</div>`;
      logBox.scrollTop = logBox.scrollHeight;
    }
  </script>

</body>
</html>
