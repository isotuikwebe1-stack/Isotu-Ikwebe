<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>5 Minutes Till Midnight</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      background: #0a0a0d;
      color: #fff;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      overflow: hidden;
    }
    #menuScreen {
      position: absolute;
      background: rgba(15, 15, 20, 0.95);
      border: 2px solid #333;
      padding: 30px;
      border-radius: 12px;
      text-align: center;
      z-index: 100;
      box-shadow: 0 0 30px rgba(0,0,0,0.9);
      max-width: 400px;
      width: 90%;
    }
    h1 { color: #ff4444; margin-top: 0; letter-spacing: 2px; }
    .select-group { margin: 20px 0; }
    button {
      background: #ff4444;
      color: white;
      border: none;
      padding: 12px 24px;
      font-size: 16px;
      font-weight: bold;
      border-radius: 6px;
      cursor: pointer;
      width: 100%;
      margin-top: 10px;
    }
    button:hover { background: #cc0000; }
    #ui {
      display: flex;
      gap: 20px;
      font-size: 16px;
      background: rgba(0,0,0,0.85);
      padding: 12px 24px;
      border-radius: 8px;
      border: 1px solid #444;
      margin-bottom: 10px;
    }
    canvas {
      border: 2px solid #333;
      box-shadow: 0 0 25px rgba(0,0,0,0.9);
      background: #121810;
      cursor: crosshair;
    }
    #controls {
      margin-top: 10px;
      font-size: 14px;
      color: #aaa;
      text-align: center;
    }
  </style>
</head>
<body>

  <!-- CHARACTER SELECTION MENU -->
  <div id="menuScreen">
    <h1>5 MINUTES TILL MIDNIGHT</h1>
    <p>Survive the Nigerian village until dawn breaks.</p>
    <div class="select-group">
      <label>Choose Character Gender:</label><br><br>
      <select id="genderSelect" style="padding: 8px; width: 100%; font-size: 14px;">
        <option value="male">Male Survivor</option>
        <option value="female">Female Survivor</option>
      </select>
    </div>
    <button onclick="startGame()">ENTER VILLAGE</button>
  </div>

  <!-- IN-GAME HUD -->
  <div id="ui">
    <div>Time Left: <span id="timer" style="color:#ff4444; font-weight:bold;">05:00</span></div>
    <div>Cowries: <span id="coins" style="color:#ffd700;">0</span></div>
    <div>Status: <span id="stateText" style="color:#00ffcc;">Normal</span></div>
    <div>Dane Gun: <span id="gunStatus" style="color:#ffcc00;">Ready</span></div>
  </div>

  <canvas id="gameCanvas" width="800" height="600"></canvas>
  <div id="controls">WASD / Arrows to Move | Click Left Mouse to Fire Dane Gun (Stuns Monster)</div>

  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    const timerEl = document.getElementById('timer');
    const coinsEl = document.getElementById('coins');
    const stateTextEl = document.getElementById('stateText');
    const gunStatusEl = document.getElementById('gunStatus');

    let gameTime = 300; // 5 Minutes
    let cowries = 0;
    let gameOver = false;
    let gameStarted = false;
    let timerInterval;

    const player = {
      x: 400,
      y: 520,
      radius: 12,
      speed: 3,
      gender: 'male',
      isHidden: false,
      isProtected: false,
      hasGunLoaded: true,
      gunCooldown: 0
    };

    const monster = {
      x: 100,
      y: 100,
      radius: 16,
      speed: 1.8,
      state: 'PATROL', // PATROL, CHASE, STUNNED
      targetX: 100,
      targetY: 100,
      stunTimer: 0
    };

    const cassavaFields = [
      { x: 80, y: 350, width: 140, height: 120 },
      { x: 580, y: 350, width: 140, height: 120 }
    ];

    const churchSanctuary = { x: 340, y: 60, width: 120, height: 100 };
    const mosqueSanctuary = { x: 100, y: 60, width: 120, height: 100 };

    let bullets = [];
    const keys = {};

    window.addEventListener('keydown', e => keys[e.key] = true);
    window.addEventListener('keyup', e => keys[e.key] = false);

    canvas.addEventListener('click', (e) => {
      if (!gameStarted || gameOver || !player.hasGunLoaded) return;

      const rect = canvas.getBoundingClientRect();
      const mouseX = e.clientX - rect.left;
      const mouseY = e.clientY - rect.top;

      const angle = Math.atan2(mouseY - player.y, mouseX - player.x);
      bullets.push({ x: player.x, y: player.y, dx: Math.cos(angle) * 7, dy: Math.sin(angle) * 7 });

      player.hasGunLoaded = false;
      player.gunCooldown = 5; // 5-second reload time
      gunStatusEl.textContent = "Reloading...";
      gunStatusEl.style.color = "#ff4444";
    });

    function startGame() {
      player.gender = document.getElementById('genderSelect').value;
      document.getElementById('menuScreen').style.display = 'none';
      gameStarted = true;

      timerInterval = setInterval(() => {
        if (gameOver) return;
        if (gameTime > 0) {
          gameTime--;
          let mins = Math.floor(gameTime / 60);
          let secs = gameTime % 60;
          timerEl.textContent = `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;

          if (gameTime < 60 && monster.state !== 'STUNNED') monster.speed = 2.3;

          // Reload Cooldown
          if (!player.hasGunLoaded) {
            player.gunCooldown--;
            if (player.gunCooldown <= 0) {
              player.hasGunLoaded = true;
              gunStatusEl.textContent = "Ready";
              gunStatusEl.style.color = "#ffcc00";
            }
          }
        } else {
          endGame(true);
        }
      }, 1000);

      update();
    }

    function update() {
      if (gameOver || !gameStarted) return;

      // 1. Player Controls
      let moveX = 0, moveY = 0;
      if (keys['w'] || keys['W'] || keys['ArrowUp']) moveY -= 1;
      if (keys['s'] || keys['S'] || keys['ArrowDown']) moveY += 1;
      if (keys['a'] || keys['A'] || keys['ArrowLeft']) moveX -= 1;
      if (keys['d'] || keys['D'] || keys['ArrowRight']) moveX += 1;

      player.x += moveX * player.speed;
      player.y += moveY * player.speed;

      player.x = Math.max(player.radius, Math.min(canvas.width - player.radius, player.x));
      player.y = Math.max(player.radius, Math.min(canvas.height - player.radius, player.y));

      // 2. Bullets
      for (let i = bullets.length - 1; i >= 0; i--) {
        let b = bullets[i];
        b.x += b.dx;
        b.y += b.dy;

        let distToMonster = Math.hypot(b.x - monster.x, b.y - monster.y);
        if (distToMonster < monster.radius) {
          monster.state = 'STUNNED';
          monster.stunTimer = 4; // Stunned for 4 seconds
          bullets.splice(i, 1);
          continue;
        }

        if (b.x < 0 || b.x > canvas.width || b.y < 0 || b.y > canvas.height) {
          bullets.splice(i, 1);
        }
      }

      // 3. Environment Detection
      player.isHidden = cassavaFields.some(field =>
        player.x > field.x && player.x < field.x + field.width &&
        player.y > field.y && player.y < field.y + field.height
      );

      let inChurch = (player.x > churchSanctuary.x && player.x < churchSanctuary.x + churchSanctuary.width &&
                      player.y > churchSanctuary.y && player.y < churchSanctuary.y + churchSanctuary.height);

      let inMosque = (player.x > mosqueSanctuary.x && player.x < mosqueSanctuary.x + mosqueSanctuary.width &&
                      player.y > mosqueSanctuary.y && player.y < mosqueSanctuary.y + mosqueSanctuary.height);

      player.isProtected = inChurch || inMosque;

      if (player.isProtected) {
        stateTextEl.textContent = "PROTECTED (Sanctuary)";
        stateTextEl.style.color = "#00ffff";
      } else if (player.isHidden) {
        stateTextEl.textContent = "HIDDEN (Cassava)";
        stateTextEl.style.color = "#55ff55";
      } else {
        stateTextEl.textContent = "EXPOSED";
        stateTextEl.style.color = "#ff4444";
      }

      // 4. Monster AI
      if (monster.state === 'STUNNED') {
        monster.stunTimer -= 0.016;
        if (monster.stunTimer <= 0) monster.state = 'PATROL';
      } else {
        let distToPlayer = Math.hypot(player.x - monster.x, player.y - monster.y);

        if (!player.isHidden && !player.isProtected && distToPlayer < 260) {
          monster.state = 'CHASE';
        } else if (player.isHidden || player.isProtected) {
          monster.state = 'PATROL';
        }

        if (monster.state === 'CHASE') {
          let angle = Math.atan2(player.y - monster.y, player.x - monster.x);
          monster.x += Math.cos(angle) * monster.speed;
          monster.y += Math.sin(angle) * monster.speed;
        } else {
          let distToTarget = Math.hypot(monster.targetX - monster.x, monster.targetY - monster.y);
          if (distToTarget < 10) {
            monster.targetX = Math.random() * (canvas.width - 100) + 50;
            monster.targetY = Math.random() * (canvas.height - 100) + 50;
          }
          let angle = Math.atan2(monster.targetY - monster.y, monster.targetX - monster.x);
          monster.x += Math.cos(angle) * (monster.speed * 0.6);
          monster.y += Math.sin(angle) * (monster.speed * 0.6);
        }

        if (distToPlayer < (player.radius + monster.radius) && !player.isProtected) {
          endGame(false);
        }
      }

      draw();
      requestAnimationFrame(update);
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Draw Church
      ctx.fillStyle = "#1e3d59";
      ctx.fillRect(churchSanctuary.x, churchSanctuary.y, churchSanctuary.width, churchSanctuary.height);
      ctx.strokeStyle = "#00ffff";
      ctx.strokeRect(churchSanctuary.x, churchSanctuary.y, churchSanctuary.width, churchSanctuary.height);
      ctx.fillStyle = "#ffffff";
      ctx.fillText("CHURCH", churchSanctuary.x + 35, churchSanctuary.y + 55);

      // Draw Mosque
      ctx.fillStyle = "#1b4d3e";
      ctx.fillRect(mosqueSanctuary.x, mosqueSanctuary.y, mosqueSanctuary.width, mosqueSanctuary.height);
      ctx.strokeStyle = "#00ffaa";
      ctx.strokeRect(mosqueSanctuary.x, mosqueSanctuary.y, mosqueSanctuary.width, mosqueSanctuary.height);
      ctx.fillStyle = "#ffffff";
      ctx.fillText("MOSQUE", mosqueSanctuary.x + 35, mosqueSanctuary.y + 55);

      // Draw Cassava Fields
      cassavaFields.forEach(field => {
        ctx.fillStyle = "#2d5a27";
        ctx.fillRect(field.x, field.y, field.width, field.height);
        ctx.fillStyle = "#88cc88";
        ctx.fillText("Cassava Field", field.x + 30, field.y + 65);
      });

      // Draw Bullets
      ctx.fillStyle = "#ffff00";
      bullets.forEach(b => {
        ctx.beginPath();
        ctx.arc(b.x, b.y, 3, 0, Math.PI * 2);
        ctx.fill();
      });

      // Draw Player (Male / Female color differentiation)
      ctx.beginPath();
      ctx.arc(player.x, player.y, player.radius, 0, Math.PI * 2);
      let baseColor = player.gender === 'male' ? "#3388ff" : "#ff66cc";
      ctx.fillStyle = player.isHidden ? "rgba(255, 255, 255, 0.4)" : baseColor;
      ctx.fill();
      ctx.closePath();

      // Draw Juju Monster
      ctx.beginPath();
      ctx.arc(monster.x, monster.y, monster.radius, 0, Math.PI * 2);
      if (monster.state === 'STUNNED') ctx.fillStyle = "#888888";
      else if (monster.state === 'CHASE') ctx.fillStyle = "#ff0000";
      else ctx.fillStyle = "#aa0000";
      ctx.fill();
      ctx.closePath();
    }

    function endGame(survived) {
      gameOver = true;
      clearInterval(timerInterval);
      ctx.fillStyle = "rgba(0,0,0,0.85)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      if (survived) {
        cowries += 150;
        coinsEl.textContent = cowries;
      }

      ctx.fillStyle = survived ? "#00ffcc" : "#ff3333";
      ctx.font = "28px Arial";
      ctx.textAlign = "center";
      ctx.fillText(survived ? "DAWN BROKE! YOU SURVIVED!" : "THE JUJU CAUGHT YOU!", canvas.width / 2, canvas.height / 2);
      ctx.font = "18px Arial";
      ctx.fillStyle = "#ffffff";
      ctx.fillText(survived ? "+150 Cowrie Coins Earned!" : "Refresh page to try again.", canvas.width / 2, canvas.height / 2 + 40);
    }
  </script>
</body>
</html>
