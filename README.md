# <!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0" />
  <title>Math Adventure Ultra - Pro UI</title>
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #6c5ce7;
      --secondary: #a29bfe;
      --success: #00b894;
      --danger: #ff7675;
      --warning: #f1c40f;
      --white: #ffffff;
      --gray: #b2bec3;
    }

    body {
      font-family: 'Kanit', sans-serif;
      margin: 0; background: #f0f2f5;
      display: flex; align-items: center; justify-content: center;
      height: 100vh; overflow: hidden;
    }

    .screen {
      position: absolute; width: 100%; max-width: 480px;
      padding: 20px; box-sizing: border-box; text-align: center;
      transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275), opacity 0.3s;
    }

    .hidden { display: none !important; opacity: 0; transform: scale(0.9); }

    .card {
      background: var(--white); padding: 30px 25px;
      border-radius: 35px; box-shadow: 0 20px 50px rgba(0,0,0,0.1);
      border-bottom: 8px solid #dfe6e9;
    }

    /* --- ปรับปรุงช่องพิมคำตอบ (New Input UI) --- */
    .input-wrapper { margin: 25px 0; position: relative; }
    
    input[type="text"] {
      width: 100%; padding: 20px; font-size: 2.2rem;
      border: 4px solid #edeff2; border-radius: 25px;
      text-align: center; color: var(--primary); font-weight: 600;
      background: #fcfdff; transition: all 0.3s; outline: none;
      box-sizing: border-box;
    }

    input[type="text"]:focus {
      border-color: var(--secondary); background: #fff;
      box-shadow: 0 0 20px rgba(108, 92, 231, 0.15);
      transform: translateY(-2px);
    }

    /* --- สไตล์ปุ่ม --- */
    .btn-group { display: flex; gap: 10px; justify-content: center; margin-top: 15px; }
    
    button {
      background: var(--primary); color: white; border: none;
      padding: 18px 25px; border-radius: 20px; font-size: 1.1rem;
      font-weight: 600; cursor: pointer; transition: 0.2s;
      box-shadow: 0 6px 0 #5849c4; font-family: 'Kanit';
      flex: 1; /* ให้ปุ่มกางเท่ากัน */
    }

    button.secondary {
      background: var(--gray); box-shadow: 0 6px 0 #636e72;
    }

    button:hover { filter: brightness(1.1); transform: translateY(-2px); }
    button:active { transform: translateY(3px); box-shadow: 0 2px 0 #5849c4; }

    /* --- องค์ประกอบอื่นๆ --- */
    .info-box { text-align: left; background: #f8f9ff; padding: 20px; border-radius: 20px; margin-bottom: 20px; }
    .question-box { font-size: 3.5rem; font-weight: 600; margin: 20px 0; color: #2d3436; }
    .timer-bar { width: 100%; height: 12px; background: #eee; border-radius: 10px; overflow: hidden; margin-bottom: 10px; }
    #timer-fill { height: 100%; background: var(--primary); width: 100%; }
  </style>
</head>
<body id="mainBody">

  <div id="intro" class="screen">
    <div class="card">
      <div style="font-size: 4rem;">🎮</div>
      <h1>Math Adventure</h1>
      <p style="color:#636e72">ยินดีต้อนรับสู่โลกแห่งตัวเลข!</p>
      <div class="info-box">
        <b>เนื้อหาที่ต้องเจอ:</b>
        <ul style="margin: 10px 0; padding-left: 20px; font-size: 0.9rem;">
          <li>การบวก ลบ และคูณเลขพื้นฐาน</li>
          <li>ระบบเวลาที่ท้าทายความเร็ว</li>
          <li>การเก็บสถิติเพื่อพัฒนาตนเอง</li>
        </ul>
      </div>
      <button onmouseenter="playSfx(800)" onclick="changeScreen('mathTips1')">เข้าสู่คำแนะนำ</button>
    </div>
  </div>

  <div id="mathTips1" class="screen hidden">
    <div class="card">
      <h2>📖 ขั้นตอนการเล่น</h2>
      <div class="info-box">
        1. พิมพ์คำตอบลงในช่อง <b>"ตัวเลข"</b><br>
        2. กด <b>"ส่งคำตอบ"</b> หรือปุ่ม <b>Enter</b><br>
        3. ตอบให้ทันก่อน <b>"แถบเวลา"</b> จะหมด<br>
        4. เกมจะเล่นทั้งหมด 20 ข้อ
      </div>
      <div class="btn-group">
        <button onmouseenter="playSfx(800)" class="secondary" onclick="changeScreen('intro')">ย้อนกลับ</button>
        <button onmouseenter="playSfx(800)" onclick="changeScreen('mathTips2')">ถัดไป ➡️</button>
      </div>
    </div>
  </div>

  <div id="mathTips2" class="screen hidden">
    <div class="card">
      <h2>🔥 ระบบคะแนน</h2>
      <div class="info-box">
        • <b>ถูก:</b> +10 คะแนน<br>
        • <b>ผิด:</b> -5 คะแนน<br>
        • <b>Combo:</b> ตอบถูกต่อเนื่องจะได้คะแนนคูณเพิ่ม!<br>
        • <b>สถิติ:</b> มีการบันทึกคะแนนสูงสุดในเครื่อง
      </div>
      <div class="btn-group">
        <button onmouseenter="playSfx(800)" class="secondary" onclick="changeScreen('mathTips1')">ย้อนกลับ</button>
        <button onmouseenter="playSfx(800)" onclick="changeScreen('mode')" style="background:var(--success); box-shadow:0 6px 0 #009476;">เลือกโหมด ✅</button>
      </div>
    </div>
  </div>

  <div id="mode" class="screen hidden">
    <div class="card">
      <h1>เลือกระดับ</h1>
      <button onmouseenter="playSfx(800)" onclick="startGame('easy')" style="background:var(--success); box-shadow:0 6px 0 #009476; width:100%;">ง่าย (1-20)</button>
      <button onmouseenter="playSfx(800)" onclick="startGame('medium')" style="background:var(--warning); box-shadow:0 6px 0 #d4ac0d; width:100%;">ปานกลาง (เลข 2 หลัก)</button>
      <button onmouseenter="playSfx(800)" onclick="startGame('hard')" style="background:var(--danger); box-shadow:0 6px 0 #d63031; width:100%;">ยาก (การคูณ)</button>
      <div class="btn-group">
        <button onmouseenter="playSfx(800)" class="secondary" onclick="changeScreen('mathTips2')" style="width:100%;">⬅️ ย้อนกลับไปหน้าคำแนะนำ</button>
      </div>
    </div>
  </div>

  <div id="game" class="screen hidden">
    <div class="card">
      <div class="timer-bar"><div id="timer-fill"></div></div>
      <div style="display:flex; justify-content:space-between; margin-bottom:10px; font-weight:bold;">
        <span>ข้อที่: <span id="qNum">1</span>/20</span>
        <span style="color:var(--primary)">คะแนน: <span id="score">0</span></span>
      </div>
      <div id="questionText" class="question-box">? + ?</div>
      
      <div class="input-wrapper">
        <input type="text" id="answerInput" inputmode="numeric" placeholder="?" autocomplete="off">
      </div>

      <button onmouseenter="playSfx(800)" onclick="checkAnswer()" style="width:100%; margin:0;">ส่งคำตอบ</button>
    </div>
  </div>

  <div id="result" class="screen hidden">
    <div class="card">
      <h1>เก่งมาก! 🏆</h1>
      <div id="finalScore" style="font-size:4rem; color:var(--primary); font-weight:bold;">0</div>
      <div id="statsSummary" style="text-align:left; background:#f8f9fa; padding:15px; border-radius:15px; margin:20px 0;"></div>
      <button onmouseenter="playSfx(800)" onclick="location.reload()">🏠 กลับหน้าหลัก</button>
    </div>
  </div>

  <script>
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    let currentScore = 0, currentQ = 0, correctAns = 0, timer, difficulty = 'easy';
    let combo = 0, correctCount = 0, totalTime = 0, startTime;

    function playSfx(freq, type = 'sine', duration = 0.1) {
      if (audioCtx.state === 'suspended') audioCtx.resume();
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.type = type; osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
      gain.gain.setValueAtTime(0.05, audioCtx.currentTime);
      gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + duration);
      osc.connect(gain); gain.connect(audioCtx.destination);
      osc.start(); osc.stop(audioCtx.currentTime + duration);
    }

    function changeScreen(id) {
      document.querySelectorAll('.screen').forEach(s => s.classList.add('hidden'));
      document.getElementById(id).classList.remove('hidden');
    }

    function startGame(mode) {
      difficulty = mode; currentScore = 0; currentQ = 0; combo = 0; correctCount = 0; totalTime = 0;
      changeScreen('game');
      nextQuestion();
    }

    function nextQuestion() {
      if (currentQ >= 20) { endGame(); return; }
      currentQ++;
      document.getElementById('qNum').textContent = currentQ;
      const input = document.getElementById('answerInput');
      input.value = ''; input.focus();
      
      let a, b, op = '+';
      if (difficulty === 'easy') { a = rand(1, 20); b = rand(1, 20); }
      else if (difficulty === 'medium') { a = rand(10, 99); b = rand(10, 50); op = Math.random() > 0.5 ? '+' : '-'; }
      else { a = rand(2, 12); b = rand(2, 12); op = '×'; }
      
      if (op === '-' && a < b) [a, b] = [b, a];
      correctAns = (op === '+') ? a + b : (op === '-') ? a - b : a * b;
      document.getElementById('questionText').textContent = `${a} ${op} ${b}`;
      
      startTime = Date.now();
      startTimer();
    }

    function rand(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }

    function startTimer() {
      clearInterval(timer);
      let timeLimit = difficulty === 'hard' ? 7 : 12;
      let timeLeft = timeLimit;
      const bar = document.getElementById('timer-fill');
      bar.style.transition = 'none'; bar.style.width = '100%';
      setTimeout(() => { bar.style.transition = `width ${timeLimit}s linear`; bar.style.width = '0%'; }, 50);
      timer = setInterval(() => { timeLeft--; if (timeLeft <= 0) processResult(false); }, 1000);
    }

    function checkAnswer() {
      const input = document.getElementById('answerInput');
      if (input.value.trim() === "") return;
      processResult(parseInt(input.value) === correctAns);
    }

    function processResult(isCorrect) {
      clearInterval(timer);
      totalTime += (Date.now() - startTime) / 1000;
      if (isCorrect) {
        combo++; correctCount++;
        currentScore += Math.round(10 * (1 + Math.min(combo, 10) * 0.1));
        playSfx(600 + (combo * 40), 'triangle', 0.15);
      } else {
        combo = 0; currentScore = Math.max(0, currentScore - 5);
        playSfx(150, 'sawtooth', 0.2);
      }
      document.getElementById('score').textContent = currentScore;
      setTimeout(nextQuestion, 600);
    }

    function endGame() {
      document.getElementById('finalScore').textContent = currentScore;
      document.getElementById('statsSummary').innerHTML = `
        🎯 ตอบถูกทั้งหมด: ${correctCount} / 20 ข้อ<br>
        ⚡ ความเร็วเฉลี่ย: ${(totalTime / 20).toFixed(2)} วินาที/ข้อ
      `;
      changeScreen('result');
    }

    document.getElementById('answerInput').addEventListener('keypress', (e) => { if (e.key === 'Enter') checkAnswer(); });
  </script>
</body>
</html>
