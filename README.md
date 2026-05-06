[index.html](https://github.com/user-attachments/files/27433172/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kreker Games</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Rajdhani:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
        :root { --neon: #00e5ff; --green: #22c55e; --bg: #020617; --card: #0f172a; --border: rgba(0,229,255,0.15); }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; min-height: 100vh; }
        body::before { content: ''; position: fixed; inset: 0; background-image: linear-gradient(rgba(0,229,255,0.025) 1px, transparent 1px), linear-gradient(90deg, rgba(0,229,255,0.025) 1px, transparent 1px); background-size: 60px 60px; pointer-events: none; z-index: 0; }
        nav { position: sticky; top: 0; z-index: 100; display: flex; align-items: center; gap: 20px; padding: 0 40px; height: 56px; background: rgba(2,6,23,0.95); border-bottom: 1px solid var(--border); backdrop-filter: blur(12px); }
        .nav-logo { display: flex; align-items: center; gap: 10px; text-decoration: none; }
        .nav-logo-circle { width: 34px; height: 34px; border-radius: 50%; border: 2px solid var(--neon); display: flex; align-items: center; justify-content: center; font-family: 'Orbitron', sans-serif; font-size: 11px; color: var(--neon); box-shadow: 0 0 10px rgba(0,229,255,0.4); }
        .nav-logo-text { font-family: 'Orbitron', sans-serif; font-size: 14px; letter-spacing: 2px; color: white; }
        .nav-links { display: flex; gap: 4px; margin-left: 20px; }
        .nav-links a { color: #64748b; text-decoration: none; font-size: 13px; letter-spacing: 1px; padding: 6px 14px; border-radius: 4px; transition: color 0.2s, background 0.2s; text-transform: uppercase; }
        .nav-links a:hover { color: white; background: rgba(255,255,255,0.05); }
        .nav-links a.active { color: var(--neon); }
        .hero { position: relative; z-index: 1; text-align: center; padding: 80px 20px 60px; background: linear-gradient(to bottom, #0f172a 0%, var(--bg) 100%); }
        .hero h1 { font-family: 'Orbitron', sans-serif; font-size: clamp(2.2rem, 6vw, 4rem); font-weight: 900; letter-spacing: 5px; background: linear-gradient(135deg, #fff 30%, var(--neon)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 12px; }
        .hero p { color: #475569; font-size: 1rem; letter-spacing: 3px; text-transform: uppercase; }
        .main { position: relative; z-index: 1; max-width: 1100px; margin: 0 auto; padding: 0 24px 80px; }
        .section-title { font-family: 'Orbitron', sans-serif; font-size: 0.75rem; letter-spacing: 4px; color: #334155; text-transform: uppercase; margin-bottom: 20px; padding-bottom: 10px; border-bottom: 1px solid rgba(255,255,255,0.04); }
        .games-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 16px; margin-bottom: 60px; }
        .game-card { background: var(--card); border: 1px solid rgba(255,255,255,0.06); border-radius: 12px; overflow: hidden; cursor: pointer; transition: transform 0.2s, border-color 0.2s, box-shadow 0.2s; animation: fadeUp 0.4s ease both; }
        .game-card:hover { transform: translateY(-4px); border-color: var(--border); box-shadow: 0 8px 30px rgba(0,229,255,0.1); }
        @keyframes fadeUp { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }
        .game-thumb { width: 100%; aspect-ratio: 16/9; display: flex; align-items: center; justify-content: center; font-size: 2.5rem; position: relative; overflow: hidden; }
        .play-overlay { position: absolute; inset: 0; display: flex; align-items: center; justify-content: center; opacity: 0; background: rgba(0,0,0,0.45); transition: opacity 0.2s; }
        .game-card:hover .play-overlay { opacity: 1; }
        .play-btn-icon { width: 50px; height: 50px; border-radius: 50%; background: rgba(0,229,255,0.9); display: flex; align-items: center; justify-content: center; box-shadow: 0 0 20px rgba(0,229,255,0.5); }
        .play-btn-icon svg { margin-left: 3px; }
        .game-info { padding: 14px 16px; }
        .game-name { font-family: 'Orbitron', sans-serif; font-size: 0.85rem; letter-spacing: 1px; color: white; margin-bottom: 4px; }
        .game-genre { font-size: 0.78rem; color: #334155; letter-spacing: 1px; text-transform: uppercase; }
        .game-card.coming-soon { opacity: 0.4; cursor: default; pointer-events: none; }
        .coming-soon-badge { position: absolute; top: 8px; right: 8px; background: rgba(0,0,0,0.7); color: #475569; font-size: 10px; letter-spacing: 2px; padding: 3px 8px; border-radius: 3px; text-transform: uppercase; font-family: 'Orbitron', sans-serif; }
        .library-empty { text-align: center; padding: 40px; color: #1e293b; font-size: 0.9rem; letter-spacing: 2px; text-transform: uppercase; border: 1px dashed #0f172a; border-radius: 12px; }
        .library-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 12px; }
        .library-item { background: var(--card); border: 1px solid rgba(255,255,255,0.04); border-radius: 8px; overflow: hidden; cursor: pointer; transition: border-color 0.2s; }
        .library-item:hover { border-color: var(--border); }
        .library-thumb { width: 100%; aspect-ratio: 16/9; display: flex; align-items: center; justify-content: center; font-size: 1.6rem; }
        .library-info { padding: 10px 12px; }
        .library-name { font-family: 'Orbitron', sans-serif; font-size: 0.7rem; letter-spacing: 1px; color: #64748b; }
        .library-played { font-size: 0.7rem; color: #1e293b; letter-spacing: 1px; margin-top: 2px; }
        footer { position: relative; z-index: 1; text-align: center; padding: 30px; color: #1e293b; font-size: 0.8rem; letter-spacing: 2px; border-top: 1px solid rgba(255,255,255,0.03); }
        .overlay { display: none; position: fixed; inset: 0; z-index: 999; background: rgba(0,0,0,0.85); backdrop-filter: blur(6px); align-items: center; justify-content: center; }
        .overlay.open { display: flex; }
        .game-window { background: #0a1628; border: 1px solid var(--border); border-radius: 16px; overflow: hidden; width: min(560px, 95vw); box-shadow: 0 0 60px rgba(0,229,255,0.15); animation: popIn 0.2s ease; max-height: 90vh; overflow-y: auto; }
        @keyframes popIn { from { opacity: 0; transform: scale(0.93); } to { opacity: 1; transform: scale(1); } }
        .game-window-bar { display: flex; align-items: center; gap: 10px; padding: 12px 18px; background: rgba(15,23,42,0.9); border-bottom: 1px solid rgba(255,255,255,0.05); position: sticky; top: 0; z-index: 10; }
        .game-window-title { font-family: 'Orbitron', sans-serif; font-size: 12px; letter-spacing: 2px; color: var(--neon); }
        .window-close { margin-left: auto; background: none; border: none; color: #475569; font-size: 18px; cursor: pointer; line-height: 1; transition: color 0.2s; padding: 2px 6px; }
        .window-close:hover { color: white; }
        /* CLICKER */
        .click-game { display: flex; flex-direction: column; align-items: center; gap: 28px; padding: 50px 20px; }
        #clickBtn { width: 180px; height: 180px; border-radius: 50%; background: transparent; border: 3px solid var(--neon); color: var(--neon); font-family: 'Orbitron', sans-serif; font-size: 1.1rem; font-weight: 700; letter-spacing: 3px; cursor: pointer; box-shadow: 0 0 25px rgba(0,229,255,0.3), inset 0 0 25px rgba(0,229,255,0.05); transition: transform 0.08s, box-shadow 0.1s; user-select: none; position: relative; }
        #clickBtn::after { content: ''; position: absolute; inset: 8px; border-radius: 50%; border: 1px solid rgba(0,229,255,0.2); }
        #clickBtn:hover { box-shadow: 0 0 40px rgba(0,229,255,0.5), inset 0 0 30px rgba(0,229,255,0.1); }
        #clickBtn:active { transform: scale(0.91); }
        .counter-display { text-align: center; }
        .counter-number { font-family: 'Orbitron', sans-serif; font-size: 3.5rem; font-weight: 900; color: var(--neon); text-shadow: 0 0 20px rgba(0,229,255,0.5); transition: transform 0.08s; display: block; line-height: 1; }
        .counter-number.bump { transform: scale(1.18); }
        .counter-label { font-size: 0.75rem; letter-spacing: 4px; color: #334155; text-transform: uppercase; margin-top: 6px; }
        #resetBtn { background: none; border: 1px solid #1e293b; color: #334155; font-family: 'Rajdhani', sans-serif; font-size: 0.85rem; letter-spacing: 2px; padding: 8px 22px; border-radius: 6px; cursor: pointer; text-transform: uppercase; transition: color 0.2s, border-color 0.2s; }
        #resetBtn:hover { color: #475569; border-color: #334155; }
        /* SNAKE */
        .snake-container { display: flex; flex-direction: column; align-items: center; }
        .snake-modes { padding: 24px 20px; display: flex; flex-direction: column; align-items: center; gap: 20px; }
        .snake-modes h3 { font-family: 'Orbitron', sans-serif; font-size: 0.85rem; letter-spacing: 3px; color: var(--green); }
        .modes-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; width: 100%; }
        .mode-toggle { display: flex; align-items: center; gap: 10px; padding: 12px 14px; border-radius: 8px; border: 1px solid rgba(255,255,255,0.06); background: rgba(255,255,255,0.02); cursor: pointer; transition: border-color 0.2s, background 0.2s; user-select: none; }
        .mode-toggle.active { border-color: rgba(34,197,94,0.4); background: rgba(34,197,94,0.08); }
        .mode-dot { width: 14px; height: 14px; border-radius: 50%; border: 2px solid #334155; flex-shrink: 0; transition: background 0.2s, border-color 0.2s; }
        .mode-toggle.active .mode-dot { background: var(--green); border-color: var(--green); }
        .mode-name { font-family: 'Orbitron', sans-serif; font-size: 0.68rem; letter-spacing: 1px; color: #64748b; }
        .mode-toggle.active .mode-name { color: var(--green); }
        .mode-desc { font-size: 0.68rem; color: #1e293b; margin-top: 2px; }
        .mode-info { display: flex; flex-direction: column; }
        .start-snake-btn { font-family: 'Orbitron', sans-serif; font-size: 0.85rem; letter-spacing: 3px; padding: 14px 40px; border-radius: 8px; background: var(--green); color: #020617; border: none; cursor: pointer; font-weight: 700; box-shadow: 0 0 20px rgba(34,197,94,0.3); transition: box-shadow 0.2s, transform 0.1s; }
        .start-snake-btn:hover { box-shadow: 0 0 30px rgba(34,197,94,0.5); transform: scale(1.02); }
        .snake-game { display: none; flex-direction: column; align-items: center; padding: 16px; gap: 12px; }
        .snake-game.active { display: flex; }
        .snake-hud { display: flex; justify-content: space-between; align-items: center; width: 100%; padding: 0 4px; }
        .snake-score-val { font-family: 'Orbitron', sans-serif; font-size: 1.2rem; color: var(--green); }
        .snake-score-label { font-size: 0.65rem; letter-spacing: 3px; color: #334155; text-transform: uppercase; }
        .active-modes { display: flex; gap: 6px; flex-wrap: wrap; justify-content: flex-end; }
        .mode-badge { font-size: 0.6rem; letter-spacing: 1px; padding: 3px 7px; border-radius: 3px; background: rgba(34,197,94,0.1); color: var(--green); border: 1px solid rgba(34,197,94,0.2); font-family: 'Orbitron', sans-serif; }
        #snakeCanvas { border: 1px solid rgba(34,197,94,0.2); border-radius: 6px; box-shadow: 0 0 20px rgba(34,197,94,0.1); max-width: 100%; }
        .snake-controls { display: flex; gap: 8px; align-items: center; flex-wrap: wrap; justify-content: center; }
        .snake-btn { background: none; border: 1px solid #1e293b; color: #475569; font-family: 'Rajdhani', sans-serif; font-size: 0.8rem; letter-spacing: 1px; padding: 6px 16px; border-radius: 4px; cursor: pointer; text-transform: uppercase; transition: color 0.2s, border-color 0.2s; }
        .snake-btn:hover { color: #94a3b8; border-color: #334155; }
        .snake-info { font-size: 0.72rem; color: #1e293b; letter-spacing: 1px; }
        .snake-gameover { display: none; flex-direction: column; align-items: center; gap: 16px; padding: 40px 20px; text-align: center; }
        .snake-gameover.active { display: flex; }
        .gameover-title { font-family: 'Orbitron', sans-serif; font-size: 1.5rem; letter-spacing: 3px; color: #ef4444; }
        .gameover-score { font-family: 'Orbitron', sans-serif; font-size: 3rem; font-weight: 900; color: var(--green); }
        .gameover-label { font-size: 0.75rem; letter-spacing: 3px; color: #334155; text-transform: uppercase; }
        .gameover-best { font-size: 0.8rem; color: #475569; letter-spacing: 2px; }
    </style>
</head>
<body>
<nav>
    <a class="nav-logo" href="#"><div class="nav-logo-circle">KG</div><span class="nav-logo-text">KREKER GAMES</span></a>
    <div class="nav-links"><a href="#" class="active">Store</a><a href="#library">Library</a></div>
</nav>
<div class="hero"><h1>KREKER GAMES</h1><p>Play Instantly · No Downloads</p></div>
<div class="main">
    <div class="section-title">All Games</div>
    <div class="games-grid" id="gamesGrid"></div>
    <div class="section-title" id="library">Your Library</div>
    <div id="libraryContainer">
        <div class="library-empty" id="libraryEmpty">Play a game to add it to your library</div>
        <div class="library-grid" id="libraryGrid" style="display:none;"></div>
    </div>
</div>
<footer>&copy; 2026 Kreker Games Studio</footer>

<div class="overlay" id="overlay">
    <div class="game-window" id="gameWindow">
        <div class="game-window-bar">
            <span class="game-window-title" id="windowTitle">GAME</span>
            <button class="window-close" onclick="closeGame()">&#x2715;</button>
        </div>
        <div id="gameClicker" style="display:none;">
            <div class="click-game">
                <button id="clickBtn">CLICK</button>
                <div class="counter-display">
                    <span class="counter-number" id="counterNum">0</span>
                    <div class="counter-label">Times Clicked</div>
                </div>
                <button id="resetBtn">Reset</button>
            </div>
        </div>
        <div id="gameSnake" style="display:none;">
            <div class="snake-container">
                <div class="snake-modes" id="snakeModes">
                    <h3>Choose Modes</h3>
                    <div class="modes-grid" id="modesGrid"></div>
                    <button class="start-snake-btn" onclick="startSnake()">&#9654; PLAY</button>
                </div>
                <div class="snake-game" id="snakeGameArea">
                    <div class="snake-hud">
                        <div><div class="snake-score-val" id="snakeScore">0</div><div class="snake-score-label">Score</div></div>
                        <div class="active-modes" id="activeModesBadges"></div>
                    </div>
                    <canvas id="snakeCanvas" width="400" height="400"></canvas>
                    <div class="snake-controls">
                        <button class="snake-btn" onclick="togglePause()" id="pauseBtn">Pause</button>
                        <button class="snake-btn" onclick="resetSnake()">Menu</button>
                        <span class="snake-info">Arrow Keys / WASD</span>
                    </div>
                </div>
                <div class="snake-gameover" id="snakeGameover">
                    <div class="gameover-title">GAME OVER</div>
                    <div class="gameover-score" id="gameoverScore">0</div>
                    <div class="gameover-label">Score</div>
                    <div class="gameover-best" id="gameoverBest"></div>
                    <div style="display:flex;gap:10px;margin-top:8px;">
                        <button class="snake-btn" onclick="startSnake()">&#9654; Play Again</button>
                        <button class="snake-btn" onclick="resetSnake()">Menu</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
const GAMES = [
    { id: 'clicker', name: 'CLICKER', genre: 'Casual', color: '#001f2e', accent: '#00e5ff', icon: '&#128070;' },
    { id: 'snaker',  name: 'SNAKER',  genre: 'Arcade', color: '#001a0a', accent: '#22c55e', icon: '&#128013;' },
    { id: 'game2',   name: 'PUZZLE',  genre: 'Puzzle', color: '#1a0a2e', accent: '#a855f7', icon: '&#129513;', comingSoon: true },
    { id: 'game3',   name: 'RACER',   genre: 'Action', color: '#1a0800', accent: '#ff4500', icon: '&#127950;', comingSoon: true },
];

let library = JSON.parse(localStorage.getItem('kg-library') || '[]');

function renderStore() {
    const grid = document.getElementById('gamesGrid');
    grid.innerHTML = '';
    GAMES.forEach((g, i) => {
        const card = document.createElement('div');
        card.className = 'game-card' + (g.comingSoon ? ' coming-soon' : '');
        card.style.animationDelay = (i * 0.07) + 's';
        card.innerHTML = '<div class="game-thumb" style="background:' + g.color + '; color:' + g.accent + ';">' +
            '<span>' + g.icon + '</span>' +
            (g.comingSoon ? '<div class="coming-soon-badge">Soon</div>' : '') +
            '<div class="play-overlay"><div class="play-btn-icon"><svg width="18" height="18" viewBox="0 0 24 24" fill="#020617"><polygon points="5,3 19,12 5,21"/></svg></div></div>' +
            '</div><div class="game-info"><div class="game-name">' + g.name + '</div><div class="game-genre">' + g.genre + '</div></div>';
        if (!g.comingSoon) card.addEventListener('click', function() { openGame(g); });
        grid.appendChild(card);
    });
}

function renderLibrary() {
    const empty = document.getElementById('libraryEmpty');
    const grid = document.getElementById('libraryGrid');
    if (library.length === 0) { empty.style.display = 'block'; grid.style.display = 'none'; return; }
    empty.style.display = 'none'; grid.style.display = 'grid'; grid.innerHTML = '';
    library.forEach(function(id) {
        const g = GAMES.find(function(x) { return x.id === id; });
        if (!g) return;
        const item = document.createElement('div');
        item.className = 'library-item';
        item.innerHTML = '<div class="library-thumb" style="background:' + g.color + ';">' + g.icon + '</div><div class="library-info"><div class="library-name">' + g.name + '</div><div class="library-played">Played</div></div>';
        item.addEventListener('click', function() { openGame(g); });
        grid.appendChild(item);
    });
}

function addToLibrary(id) {
    if (!library.includes(id)) { library.push(id); localStorage.setItem('kg-library', JSON.stringify(library)); renderLibrary(); }
}

function openGame(g) {
    document.getElementById('windowTitle').textContent = g.name;
    document.getElementById('overlay').classList.add('open');
    document.getElementById('gameClicker').style.display = 'none';
    document.getElementById('gameSnake').style.display = 'none';
    if (g.id === 'clicker') { document.getElementById('gameClicker').style.display = 'block'; }
    else if (g.id === 'snaker') { document.getElementById('gameSnake').style.display = 'block'; resetSnake(); }
    addToLibrary(g.id);
}

function closeGame() { document.getElementById('overlay').classList.remove('open'); stopSnakeLoop(); }
document.getElementById('overlay').addEventListener('click', function(e) { if (e.target.id === 'overlay') closeGame(); });

// CLICKER
var clickCount = 0;
document.getElementById('clickBtn').addEventListener('click', function() {
    clickCount++;
    var el = document.getElementById('counterNum');
    el.textContent = clickCount;
    el.classList.remove('bump'); void el.offsetWidth; el.classList.add('bump');
    setTimeout(function() { el.classList.remove('bump'); }, 100);
});
document.getElementById('resetBtn').addEventListener('click', function() { clickCount = 0; document.getElementById('counterNum').textContent = 0; });

// SNAKE
var SNAKE_MODES = [
    { id: 'walls',  name: 'WALLS',       desc: 'Pass through walls' },
    { id: 'speed',  name: 'SPEED UP',    desc: 'Faster each apple' },
    { id: 'colors', name: 'COLOR SHIFT', desc: 'Colors change on eat' },
    { id: 'ghost',  name: 'GHOST',       desc: 'Pass through yourself' },
];
var activeModes = {};
var snakeLoop = null;
var snakeRunning = false;
var snakePaused = false;
var snake, dir, nextDir, food, score, currentSpeed;
var bgColor, snakeColor, foodColor;
var CELL = 20, COLS = 20, ROWS = 20;

function stopSnakeLoop() { clearTimeout(snakeLoop); snakeLoop = null; snakeRunning = false; }

function buildModesUI() {
    activeModes = {};
    SNAKE_MODES.forEach(function(m) { activeModes[m.id] = false; });
    var grid = document.getElementById('modesGrid');
    grid.innerHTML = '';
    SNAKE_MODES.forEach(function(m) {
        var el = document.createElement('div');
        el.className = 'mode-toggle';
        el.innerHTML = '<div class="mode-dot"></div><div class="mode-info"><div class="mode-name">' + m.name + '</div><div class="mode-desc">' + m.desc + '</div></div>';
        el.addEventListener('click', function() {
            activeModes[m.id] = !activeModes[m.id];
            el.classList.toggle('active', activeModes[m.id]);
        });
        grid.appendChild(el);
    });
}

function resetSnake() {
    stopSnakeLoop();
    document.getElementById('snakeModes').style.display = 'flex';
    document.getElementById('snakeGameArea').classList.remove('active');
    document.getElementById('snakeGameover').classList.remove('active');
    buildModesUI();
}

function startSnake() {
    stopSnakeLoop();
    document.getElementById('snakeModes').style.display = 'none';
    document.getElementById('snakeGameover').classList.remove('active');
    document.getElementById('snakeGameArea').classList.add('active');

    snake = [{ x: 10, y: 10 }];
    dir = { x: 1, y: 0 };
    nextDir = { x: 1, y: 0 };
    score = 0;
    currentSpeed = 150;
    bgColor = '#001a0a';
    snakeColor = '#22c55e';
    foodColor = '#ef4444';
    document.getElementById('snakeScore').textContent = 0;
    updateModeBadges();
    food = spawnFood();
    snakeRunning = true;
    snakePaused = false;
    document.getElementById('pauseBtn').textContent = 'Pause';

    var canvas = document.getElementById('snakeCanvas');
    var ctx = canvas.getContext('2d');
    drawSnake(ctx, canvas);
    snakeLoop = setTimeout(function tick() {
        if (!snakeRunning || snakePaused) return;
        dir = { x: nextDir.x, y: nextDir.y };
        var head = { x: snake[0].x + dir.x, y: snake[0].y + dir.y };
        if (activeModes.walls) { head.x = (head.x + COLS) % COLS; head.y = (head.y + ROWS) % ROWS; }
        else if (head.x < 0 || head.x >= COLS || head.y < 0 || head.y >= ROWS) { gameOver(); return; }
        if (!activeModes.ghost && snake.some(function(s) { return s.x === head.x && s.y === head.y; })) { gameOver(); return; }
        snake.unshift(head);
        if (head.x === food.x && head.y === food.y) {
            score++;
            document.getElementById('snakeScore').textContent = score;
            food = spawnFood();
            if (activeModes.speed) currentSpeed = Math.max(60, 150 - score * 5);
            if (activeModes.colors) {
                var sc = ['#22c55e','#00e5ff','#a855f7','#f59e0b','#ec4899'];
                snakeColor = sc[Math.floor(Math.random() * sc.length)];
                foodColor = sc[Math.floor(Math.random() * sc.length)];
                var bc = ['#001a0a','#001f2e','#1a0a2e','#1a0800'];
                bgColor = bc[Math.floor(Math.random() * bc.length)];
            }
        } else { snake.pop(); }
        drawSnake(ctx, canvas);
        snakeLoop = setTimeout(tick, currentSpeed);
    }, currentSpeed);
}

function drawSnake(ctx, canvas) {
    ctx.fillStyle = bgColor; ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.strokeStyle = 'rgba(34,197,94,0.05)'; ctx.lineWidth = 0.5;
    for (var i = 0; i <= COLS; i++) { ctx.beginPath(); ctx.moveTo(i*CELL,0); ctx.lineTo(i*CELL,canvas.height); ctx.stroke(); }
    for (var j = 0; j <= ROWS; j++) { ctx.beginPath(); ctx.moveTo(0,j*CELL); ctx.lineTo(canvas.width,j*CELL); ctx.stroke(); }
    ctx.fillStyle = foodColor; ctx.shadowBlur = 12; ctx.shadowColor = foodColor;
    ctx.beginPath(); ctx.arc(food.x*CELL+CELL/2, food.y*CELL+CELL/2, CELL/2-2, 0, Math.PI*2); ctx.fill();
    ctx.shadowBlur = 0;
    snake.forEach(function(seg, i) {
        ctx.globalAlpha = i === 0 ? 1 : Math.max(0.3, 1 - i/snake.length);
        ctx.fillStyle = snakeColor;
        ctx.shadowBlur = i === 0 ? 8 : 0; ctx.shadowColor = snakeColor;
        var p = i === 0 ? 1 : 2;
        ctx.beginPath(); ctx.roundRect(seg.x*CELL+p, seg.y*CELL+p, CELL-p*2, CELL-p*2, i===0?4:2); ctx.fill();
    });
    ctx.globalAlpha = 1; ctx.shadowBlur = 0;
}

function spawnFood() {
    var pos;
    do { pos = { x: Math.floor(Math.random()*COLS), y: Math.floor(Math.random()*ROWS) }; }
    while (snake.some(function(s) { return s.x===pos.x && s.y===pos.y; }));
    return pos;
}

function gameOver() {
    snakeRunning = false; clearTimeout(snakeLoop);
    document.getElementById('snakeGameArea').classList.remove('active');
    document.getElementById('snakeGameover').classList.add('active');
    document.getElementById('gameoverScore').textContent = score;
    var best = Math.max(score, parseInt(localStorage.getItem('snake-best')||'0'));
    localStorage.setItem('snake-best', best);
    document.getElementById('gameoverBest').textContent = 'Best: ' + best;
}

function togglePause() {
    snakePaused = !snakePaused;
    document.getElementById('pauseBtn').textContent = snakePaused ? 'Resume' : 'Pause';
    if (!snakePaused) {
        snakeRunning = true;
        var canvas = document.getElementById('snakeCanvas');
        var ctx = canvas.getContext('2d');
        snakeLoop = setTimeout(function tick() {
            if (!snakeRunning || snakePaused) return;
            dir = { x: nextDir.x, y: nextDir.y };
            var head = { x: snake[0].x + dir.x, y: snake[0].y + dir.y };
            if (activeModes.walls) { head.x = (head.x+COLS)%COLS; head.y = (head.y+ROWS)%ROWS; }
            else if (head.x<0||head.x>=COLS||head.y<0||head.y>=ROWS) { gameOver(); return; }
            if (!activeModes.ghost && snake.some(function(s){return s.x===head.x&&s.y===head.y;})) { gameOver(); return; }
            snake.unshift(head);
            if (head.x===food.x&&head.y===food.y) {
                score++; document.getElementById('snakeScore').textContent=score; food=spawnFood();
                if(activeModes.speed) currentSpeed=Math.max(60,150-score*5);
                if(activeModes.colors){var sc=['#22c55e','#00e5ff','#a855f7','#f59e0b','#ec4899'];snakeColor=sc[Math.floor(Math.random()*sc.length)];foodColor=sc[Math.floor(Math.random()*sc.length)];var bc=['#001a0a','#001f2e','#1a0a2e','#1a0800'];bgColor=bc[Math.floor(Math.random()*bc.length)];}
            } else { snake.pop(); }
            drawSnake(ctx, canvas);
            snakeLoop = setTimeout(tick, currentSpeed);
        }, currentSpeed);
    }
}

function updateModeBadges() {
    var c = document.getElementById('activeModesBadges'); c.innerHTML = '';
    SNAKE_MODES.forEach(function(m) {
        if (activeModes[m.id]) { var b=document.createElement('span'); b.className='mode-badge'; b.textContent=m.name; c.appendChild(b); }
    });
}

document.addEventListener('keydown', function(e) {
    var map = { ArrowUp:{x:0,y:-1}, ArrowDown:{x:0,y:1}, ArrowLeft:{x:-1,y:0}, ArrowRight:{x:1,y:0}, w:{x:0,y:-1}, s:{x:0,y:1}, a:{x:-1,y:0}, d:{x:1,y:0}, W:{x:0,y:-1}, S:{x:0,y:1}, A:{x:-1,y:0}, D:{x:1,y:0} };
    var nd = map[e.key];
    if (nd && snakeRunning && !(nd.x===-dir.x&&nd.y===-dir.y)) { nextDir=nd; if(['ArrowUp','ArrowDown','ArrowLeft','ArrowRight'].includes(e.key)) e.preventDefault(); }
    if (e.key===' ' && snakeRunning) { togglePause(); e.preventDefault(); }
});

renderStore();
renderLibrary();
</script>
</body>
</html>
