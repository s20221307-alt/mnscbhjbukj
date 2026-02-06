root {
            --zzz-green: #c6f432;
            --zzz-black: #050505;
            --zzz-grey: #1a1a1a;
            --zzz-white: #f0f0f0;
            --zzz-ora<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>絕區零調頻模擬 (AI Fairy Ver.)</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Rajdhani:wght@500;700;900&family=Noto+Sans+TC:wght@500;700;900&display=swap');
nge: #ff4d00;
            --zzz-red: #ff003c;
            --rank-s: #ffc700;
            --rank-a: #d640ff;
            --rank-b: #00d9ff;
        }

        body {
            background-color: var(--zzz-black);
            background-image: 
                linear-gradient(45deg, #111 25%, transparent 25%, transparent 75%, #111 75%, #111),
                linear-gradient(45deg, #111 25%, transparent 25%, transparent 75%, #111 75%, #111);
            background-size: 20px 20px;
            background-position: 0 0, 10px 10px;
            color: var(--zzz-white);
            font-family: 'Rajdhani', 'Noto Sans TC', sans-serif;
            margin: 0;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
            text-transform: uppercase;
        }

        /* --- CRT Overlay Effect --- */
        body::after {
            content: " ";
            display: block;
            position: fixed;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            z-index: 999;
            background-size: 100% 2px, 3px 100%;
            pointer-events: none;
        }

        /* --- Header --- */
        .header {
            width: 100%;
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--zzz-black);
            border-bottom: 2px solid var(--zzz-green);
            box-sizing: border-box;
            z-index: 10;
        }

        .header-title {
            font-weight: 900;
            font-size: 2rem;
            color: var(--zzz-green);
            letter-spacing: -1px;
            font-style: italic;
            text-shadow: 2px 2px 0px #fff;
        }

        .resource-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .tape-counter {
            background: var(--zzz-grey);
            border: 1px solid #333;
            padding: 5px 20px;
            border-radius: 4px;
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: bold;
            transform: skewX(-10deg);
        }

        .icon-tape {
            width: 24px;
            height: 24px;
            background: conic-gradient(from 45deg, #333, #666, #333);
            border-radius: 50%;
            border: 2px solid var(--zzz-white);
            position: relative;
        }
        .icon-tape::after {
            content: '';
            position: absolute;
            top: 50%; left: 50%; width: 6px; height: 6px;
            background: var(--zzz-green);
            transform: translate(-50%, -50%);
            border-radius: 50%;
        }

        /* --- TV/Banner Container --- */
        .tv-wrapper {
            position: relative;
            margin-top: 30px;
            width: 90%;
            max-width: 1000px;
            height: 480px;
            background: #000;
            border-radius: 20px;
            padding: 10px;
            box-shadow: 0 0 0 5px #222, 0 0 20px rgba(198, 244, 50, 0.2);
        }

        .screen-content {
            width: 100%;
            height: 100%;
            background: #111;
            border-radius: 10px;
            position: relative;
            overflow: hidden;
            border: 2px solid #333;
        }

        /* Banner Graphics */
        .banner-bg {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-size: cover;
            background-position: center;
            z-index: 1;
            transition: background 0.5s ease;
        }
        
        .halftone-overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: radial-gradient(circle, #000 1px, transparent 1.5px);
            background-size: 8px 8px;
            opacity: 0.3;
            z-index: 2;
        }

        /* Decoration Lines */
        .deco-line {
            position: absolute;
            height: 200%;
            width: 2px;
            background: rgba(255,255,255,0.1);
            transform: rotate(45deg);
            z-index: 2;
        }

        .banner-info {
            position: absolute;
            left: 50px;
            bottom: 60px;
            z-index: 5;
            max-width: 600px;
        }

        .channel-tag {
            background: var(--zzz-green);
            color: var(--zzz-black);
            padding: 4px 12px;
            font-weight: 900;
            font-size: 1rem;
            display: inline-block;
            transform: skewX(-10deg);
            margin-bottom: 15px;
        }

        .char-name {
            font-size: 5rem;
            font-weight: 900;
            line-height: 0.9;
            color: var(--zzz-white);
            margin: 0;
            text-shadow: 4px 4px 0px var(--zzz-black);
            font-style: italic;
            letter-spacing: -2px;
        }

        .char-meta {
            margin-top: 15px;
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--zzz-orange);
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .channel-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: var(--zzz-green);
            color: var(--zzz-black);
            width: 60px;
            height: 60px;
            border: none;
            font-weight: 900;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 20;
            clip-path: polygon(20% 0%, 100% 0, 100% 80%, 80% 100%, 0 100%, 0% 20%);
            transition: transform 0.1s;
        }
        .channel-btn:active { transform: translateY(-50%) scale(0.9); }
        .btn-prev { left: -30px; }
        .btn-next { right: -30px; }

        /* --- Control Panel --- */
        .controls {
            display: flex;
            gap: 20px;
            margin-top: 30px;
            position: relative;
            flex-wrap: wrap;
            justify-content: center;
        }

        .signal-btn {
            background: var(--zzz-black);
            color: var(--zzz-white);
            border: 2px solid var(--zzz-white);
            padding: 15px 40px;
            font-family: 'Rajdhani', sans-serif;
            font-weight: 900;
            font-size: 1.5rem;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all 0.2s;
            text-transform: uppercase;
        }

        .signal-btn:hover {
            background: var(--zzz-green);
            color: var(--zzz-black);
            border-color: var(--zzz-green);
            box-shadow: 0 0 15px var(--zzz-green);
        }

        .btn-10 {
            background: var(--zzz-white);
            color: var(--zzz-black);
            border-color: var(--zzz-white);
        }
        .btn-10:hover {
            background: var(--zzz-orange);
            border-color: var(--zzz-orange);
            color: var(--zzz-white);
            box-shadow: 0 0 15px var(--zzz-orange);
        }

        .btn-auto {
            background: var(--zzz-red);
            color: #fff;
            border-color: var(--zzz-red);
        }
        .btn-auto:hover {
            background: #fff;
            color: var(--zzz-red);
            border-color: #fff;
            box-shadow: 0 0 15px var(--zzz-red);
        }
        
        .btn-fairy {
            background: #111;
            color: #00d9ff; /* Fairy Blue */
            border-color: #00d9ff;
        }
        .btn-fairy:hover {
            background: #00d9ff;
            color: #000;
            box-shadow: 0 0 15px #00d9ff;
        }

        /* --- Stats Box --- */
        .stats-box {
            margin-top: 20px;
            background: rgba(0,0,0,0.8);
            border: 1px solid #333;
            padding: 10px 20px;
            font-size: 0.8rem;
            color: #888;
            font-family: monospace;
            border-left: 4px solid var(--zzz-green);
        }

        /* --- Animation (TV Tune-in) --- */
        .tune-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #000;
            z-index: 100;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .signal-wave {
            width: 100%;
            height: 10px;
            background: var(--zzz-green);
            box-shadow: 0 0 20px var(--zzz-green);
            animation: collapse 0.4s ease-in forwards;
        }

        .noise {
            width: 100%; height: 100%;
            background: repeating-linear-gradient(0deg, transparent, transparent 1px, #111 1px, #111 2px);
            opacity: 0.1;
            position: absolute;
            animation: noiseMove 0.2s infinite;
        }

        @keyframes collapse {
            0% { height: 10px; width: 100%; }
            50% { height: 2px; width: 100%; }
            100% { height: 0px; width: 0%; opacity: 0;}
        }

        /* --- Results Grid --- */
        .results-container {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(5, 5, 5, 0.95);
            z-index: 90;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(5px);
        }

        .results-header {
            color: var(--zzz-green);
            font-size: 2rem;
            font-weight: 900;
            margin-bottom: 20px;
            font-style: italic;
        }

        .cards-grid {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
            max-width: 1200px;
        }

        .agent-card {
            width: 140px;
            height: 300px;
            background: #111;
            border: 1px solid #333;
            position: relative;
            display: flex;
            flex-direction: column;
            overflow: hidden;
            animation: slideUp 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275) backwards;
            transition: transform 0.2s;
        }
        
        .agent-card:hover {
            transform: scale(1.05) translateY(-10px);
            z-index: 10;
            box-shadow: 0 10px 30px rgba(0,0,0,0.8);
        }

        /* Rarity Styles (No Images, just abstract) */
        .rank-s { border: 3px solid var(--rank-s); box-shadow: 0 0 20px var(--rank-s); }
        .rank-a { border: 2px solid var(--rank-a); box-shadow: 0 0 10px rgba(214, 64, 255, 0.3); }
        .rank-b { border: 1px solid var(--rank-b); }

        .card-bg {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            z-index: 1;
            opacity: 0.8;
        }
        
        .rank-s .card-bg { background: linear-gradient(135deg, rgba(255, 199, 0, 0.8) 0%, transparent 60%); }
        .rank-a .card-bg { background: linear-gradient(135deg, rgba(214, 64, 255, 0.8) 0%, transparent 60%); }
        .rank-b .card-bg { background: linear-gradient(135deg, rgba(0, 217, 255, 0.5) 0%, transparent 60%); }

        .card-info {
            position: absolute;
            bottom: 0; left: 0; width: 100%;
            height: 100%;
            z-index: 3;
            padding: 15px;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            box-sizing: border-box;
        }

        .agent-rank {
            font-weight: 900;
            font-size: 3.5rem;
            position: absolute;
            top: 0;
            right: 0px;
            line-height: 0.8;
            opacity: 0.4;
            color: #fff;
            z-index: 0;
            font-style: italic;
        }

        .agent-name {
            font-weight: 900;
            font-size: 1.2rem;
            line-height: 1.1;
            text-transform: uppercase;
            text-shadow: 0 2px 4px #000;
            position: relative;
            z-index: 10;
            margin-bottom: 5px;
        }

        .agent-type {
            font-size: 0.75rem;
            font-weight: 700;
            background: #000;
            color: #fff;
            display: inline-block;
            padding: 3px 8px;
            width: fit-content;
            position: relative;
            z-index: 10;
        }

        .rank-s .agent-type { background: var(--rank-s); color: #000; }
        .rank-a .agent-type { background: var(--rank-a); color: #fff; }
        .rank-b .agent-type { background: var(--rank-b); color: #000; }

        .close-btn {
            margin-top: 40px;
            background: var(--zzz-green);
            color: #000;
            border: none;
            padding: 10px 60px;
            font-weight: 900;
            font-size: 1.2rem;
            cursor: pointer;
            clip-path: polygon(10% 0, 100% 0, 100% 70%, 90% 100%, 0 100%, 0 30%);
        }
        .close-btn:hover { background: #fff; }
        
        /* --- AI Terminal Modal --- */
        .ai-modal {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.9);
            z-index: 200;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(10px);
        }

        .ai-terminal {
            width: 80%;
            max-width: 600px;
            background: #0d0d0d;
            border: 2px solid #00d9ff;
            padding: 20px;
            box-shadow: 0 0 30px rgba(0, 217, 255, 0.3);
            color: #00d9ff;
            font-family: 'Consolas', monospace;
            position: relative;
            overflow: hidden;
        }
        
        .ai-terminal::before {
            content: "FAIRY_SYSTEM_ACCESS_V2.0";
            position: absolute;
            top: 5px; left: 10px;
            font-size: 0.7rem;
            opacity: 0.5;
        }
        
        .ai-content {
            margin-top: 20px;
            min-height: 100px;
            white-space: pre-wrap;
            line-height: 1.5;
            font-size: 1rem;
        }
        
        .ai-loading {
            animation: blink 1s infinite;
        }
        
        @keyframes blink { 0% { opacity: 0; } 50% { opacity: 1; } 100% { opacity: 0; } }
        
        .ai-close-btn {
            margin-top: 20px;
            background: transparent;
            border: 1px solid #00d9ff;
            color: #00d9ff;
            padding: 5px 20px;
            cursor: pointer;
            font-family: 'Rajdhani', sans-serif;
            font-weight: bold;
            text-transform: uppercase;
        }
        .ai-close-btn:hover { background: #00d9ff; color: #000; }
        
        .analyze-btn {
            margin-top: 10px;
            background: var(--rank-s);
            color: #000;
            border: none;
            padding: 5px 15px;
            font-weight: bold;
            cursor: pointer;
            font-size: 0.8rem;
            display: none; /* Dynamic */
        }

        @keyframes slideUp {
            from { transform: translateY(100px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

    </style>
</head>
<body>

    <div class="header">
        <div class="header-title">ZENLESS ZONE ZERO</div>
        <div class="resource-container">
            <div class="tape-counter">
                <div class="icon-tape"></div>
                <span id="tape-count">∞</span>
            </div>
        </div>
    </div>

    <div class="tv-wrapper">
        <button class="channel-btn btn-prev" onclick="switchChannel(-1)">‹</button>
        <div class="screen-content">
            <div class="banner-bg" id="banner-bg"></div>
            <div class="halftone-overlay"></div>
            <div class="deco-line" style="left:20%"></div>
            <div class="deco-line" style="left:25%; width:5px;"></div>
            
            <div class="banner-info">
                <div class="channel-tag">獨家頻段</div>
                <h1 class="char-name" id="char-name">艾倫·喬</h1>
                <div class="char-meta">
                    <span id="char-rank" style="color:var(--rank-s)">S級</span>
                    <span style="font-size:0.8rem; color:#fff;">//</span>
                    <span id="char-attr">冰屬性 · 強攻</span>
                </div>
            </div>
        </div>
        <button class="channel-btn btn-next" onclick="switchChannel(1)">›</button>
    </div>

    <div class="controls">
        <button class="signal-btn" onclick="search(1)">
            單次調頻
        </button>
        <button class="signal-btn btn-10" onclick="search(10)">
            十連調頻
        </button>
        <button class="signal-btn btn-auto" onclick="autoSearch()">
            自動調頻 (直至 S 級)
        </button>
        <button class="signal-btn btn-fairy" onclick="askFairy()">
            Fairy 運勢運算
        </button>
    </div>

    <div class="stats-box">
        [SYSTEM LOG] PITY_S: <span id="pity-s" style="color:var(--zzz-green)">0</span>/90 | PITY_A: <span id="pity-a" style="color:var(--zzz-white)">0</span>/10 | UP_GUARANTEE: <span id="guarantee">FALSE</span>
        <button onclick="resetSystem()" style="float:right; background:transparent; border:none; color:#555; cursor:pointer;">[RESET]</button>
    </div>

    <!-- Animation Overlay -->
    <div class="tune-overlay" id="anim-layer">
        <div class="noise"></div>
        <div class="signal-wave"></div>
        <h1 style="color:var(--zzz-green); font-size:3rem; font-style:italic; font-weight:900; z-index:2;">SIGNAL SEARCHING...</h1>
    </div>

    <!-- Results -->
    <div class="results-container" id="results-layer">
        <div class="results-header" id="res-header"></div>
        <div class="cards-grid" id="grid"></div>
        <div style="display:flex; gap:20px; align-items:center;">
             <button class="close-btn" onclick="closeResults()">確認接收</button>
             <button class="analyze-btn" id="analyze-btn" onclick="analyzeSignal()">S 級信號解析</button>
        </div>
    </div>

    <!-- AI Terminal -->
    <div class="ai-modal" id="ai-modal">
        <div class="ai-terminal">
            <div class="ai-content" id="ai-output"><span class="ai-loading">_CALCULATING...</span></div>
            <button class="ai-close-btn" onclick="closeAI()">CLOSE TERMINAL</button>
        </div>
    </div>

    <script>
        const apiKey = ""; // Runtime provided

        // --- Data ---
        // Clean data without images
        const DB = {
            banners: [
                {
                    name: "簡 (Jane)",
                    rank: "S級",
                    attr: "物理 · 異常",
                    bg: "linear-gradient(135deg, #111 0%, #800 100%)"
                },
                {
                    name: "凱撒 (Caesar)",
                    rank: "S級",
                    attr: "物理 · 防護",
                    bg: "linear-gradient(135deg, #111 0%, #aa8800 100%)"
                },
                {
                    name: "艾倫·喬 (Ellen)",
                    rank: "S級",
                    attr: "冰屬性 · 強攻",
                    bg: "linear-gradient(135deg, #111 0%, #300 100%)"
                },
                {
                    name: "朱鳶 (Zhu Yuan)",
                    rank: "S級",
                    attr: "以太屬性 · 強攻",
                    bg: "linear-gradient(135deg, #000 0%, #1a237e 100%)"
                },
                {
                    name: "青衣 (Qingyi)",
                    rank: "S級",
                    attr: "電屬性 · 擊破",
                    bg: "linear-gradient(135deg, #000 0%, #004d40 100%)"
                }
            ],
            s_rank: [
                { name: "萊卡恩 (Lycaon)", attr: "冰 · 擊破" },
                { name: "珂蕾妲 (Koleda)", attr: "火 · 擊破" },
                { name: "麗娜 (Rina)", attr: "電 · 支援" },
                { name: "葛莉絲 (Grace)", attr: "電 · 異常" },
                { name: "貓又 (Nekomata)", attr: "物理 · 強攻" },
                { name: "11號 (Soldier 11)", attr: "火 · 強攻" }
            ],
            a_rank: [
                { name: "賽斯 (Seth)", attr: "電 · 防護" },
                { name: "安比 (Anby)", attr: "電 · 擊破" },
                { name: "比利 (Billy)", attr: "物理 · 強攻" },
                { name: "妮可 (Nicole)", attr: "以太 · 支援" },
                { name: "可琳 (Corin)", attr: "物理 · 強攻" },
                { name: "本 (Ben)", attr: "火 · 防護" },
                { name: "蒼角 (Soukaku)", attr: "冰 · 支援" },
                { name: "安東 (Anton)", attr: "電 · 強攻" },
                { name: "露西 (Lucy)", attr: "火 · 支援" },
                { name: "派派 (Piper)", attr: "物理 · 異常" }
            ],
            b_rank: [
                { name: " [音擎] 湍流矢", attr: "B級音擎" },
                { name: " [音擎] 磁暴", attr: "B級音擎" },
                { name: " [音擎] 復仇者", attr: "B級音擎" },
                { name: " [音擎] 街頭鑽頭", attr: "B級音擎" },
                { name: " [音擎] 殘響", attr: "B級音擎" }
            ]
        };

        // --- State ---
        let currentBanner = 0;
        let pityS = 0;
        let pityA = 0;
        let guaranteeS = false;
        let lastSRankChar = null; // Store for analysis

        // --- UI ---
        const uiName = document.getElementById('char-name');
        const uiRank = document.getElementById('char-rank');
        const uiAttr = document.getElementById('char-attr');
        const uiBg = document.getElementById('banner-bg');
        
        const animLayer = document.getElementById('anim-layer');
        const resLayer = document.getElementById('results-layer');
        const resHeader = document.getElementById('res-header');
        const grid = document.getElementById('grid');
        const analyzeBtn = document.getElementById('analyze-btn');
        
        const aiModal = document.getElementById('ai-modal');
        const aiOutput = document.getElementById('ai-output');

        // --- Init ---
        updateBanner();

        // --- Functions ---
        function switchChannel(dir) {
            currentBanner += dir;
            if (currentBanner < 0) currentBanner = DB.banners.length - 1;
            if (currentBanner >= DB.banners.length) currentBanner = 0;
            updateBanner();
        }

        function updateBanner() {
            const b = DB.banners[currentBanner];
            uiName.innerText = b.name;
            uiRank.innerText = b.rank;
            uiAttr.innerText = b.attr;
            uiBg.style.background = b.bg;
        }

        function getProbS(p) { return p < 74 ? 0.006 : 0.006 + (p - 73) * 0.06; }
        
        function pull() {
            pityS++;
            pityA++;
            const rand = Math.random();
            const probS = getProbS(pityS);

            // S Rank
            if (rand < probS || pityS >= 90) {
                pityS = 0;
                // 50/50 Logic
                const bannerChar = DB.banners[currentBanner];
                const win = guaranteeS || Math.random() < 0.5;
                
                if (win) {
                    guaranteeS = false;
                    return { ...bannerChar, rarity: 's' };
                } else {
                    guaranteeS = true;
                    const spook = DB.s_rank[Math.floor(Math.random() * DB.s_rank.length)];
                    return { ...spook, rarity: 's' };
                }
            }

            // A Rank
            if (pityA >= 10 || rand < 0.05 + probS) { 
                pityA = 0;
                const char = DB.a_rank[Math.floor(Math.random() * DB.a_rank.length)];
                return { ...char, rarity: 'a' };
            }

            // B Rank
            const item = DB.b_rank[Math.floor(Math.random() * DB.b_rank.length)];
            return { ...item, rarity: 'b' };
        }

        function search(n) {
            if (animLayer.style.display === 'flex') return;
            const results = [];
            for(let i=0; i<n; i++) results.push(pull());
            
            updateStats();
            playAnim(results);
        }

        function autoSearch() {
            if (animLayer.style.display === 'flex') return;
            
            let results = [];
            let totalPulls = 0;
            let foundS = false;
            let maxSafety = 200; // Limit to prevent infinite loop
            
            while(!foundS && totalPulls < maxSafety) {
                // Do a 10-pull
                let batch = [];
                for(let i=0; i<10; i++) {
                    let res = pull();
                    batch.push(res);
                    totalPulls++;
                    if(res.rarity === 's') {
                        foundS = true;
                    }
                }
                // Update results to be the final winning batch
                results = batch;
            }
            
            updateStats();
            playAnim(results, `自動調頻完畢: 花費 ${totalPulls} 抽`);
        }

        function playAnim(results, customMsg) {
            animLayer.style.display = 'flex';
            setTimeout(() => {
                animLayer.style.display = 'none';
                showResults(results, customMsg);
            }, 1000); 
        }

        function showResults(results, customMsg) {
            grid.innerHTML = '';
            resHeader.innerText = customMsg || "";
            
            // Sort by rarity
            const order = { 's': 3, 'a': 2, 'b': 1 };
            results.sort((a,b) => order[b.rarity] - order[a.rarity]);
            
            // Check for S rank to enable analysis button
            const sRank = results.find(r => r.rarity === 's');
            if (sRank) {
                lastSRankChar = sRank.name;
                analyzeBtn.style.display = 'block';
            } else {
                lastSRankChar = null;
                analyzeBtn.style.display = 'none';
            }

            results.forEach((item, idx) => {
                const div = document.createElement('div');
                div.className = `agent-card rank-${item.rarity}`;
                div.style.animationDelay = `${idx * 0.05}s`;
                
                // Abstract card content (no image)
                div.innerHTML = `
                    <div class="card-bg"></div>
                    <div class="card-info">
                        <div class="agent-rank">${item.rarity.toUpperCase()}</div>
                        <div class="agent-name">${item.name.split(' ')[0]}</div>
                        <div class="agent-type">${item.attr.split('·')[0]}</div>
                    </div>
                `;
                grid.appendChild(div);
            });
            resLayer.style.display = 'flex';
        }

        function closeResults() {
            resLayer.style.display = 'none';
        }

        function updateStats() {
            document.getElementById('pity-s').innerText = pityS;
            document.getElementById('pity-a').innerText = pityA;
            document.getElementById('guarantee').innerText = guaranteeS ? "TRUE" : "FALSE";
        }

        function resetSystem() {
            pityS = 0; pityA = 0; guaranteeS = false;
            updateStats();
        }

        // --- AI Features ---

        async function generateContent(prompt) {
            try {
                const response = await fetch(
                    `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`,
                    {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify({
                            contents: [{
                                parts: [{ text: prompt }]
                            }]
                        })
                    }
                );
                
                if (!response.ok) {
                    throw new Error(`API error: ${response.status}`);
                }

                const data = await response.json();
                return data.candidates[0].content.parts[0].text;
            } catch (error) {
                console.error("Gemini API Error:", error);
                return "系統連線異常... Fairy 無法連接至數據庫。";
            }
        }

        async function askFairy() {
            aiModal.style.display = 'flex';
            aiOutput.innerHTML = '<span class="ai-loading">_FAIRY_ANALYZING_LUCK_INDEX...</span>';
            
            const prompt = `你現在是遊戲《絕區零》中的人工智能 'Fairy'。請用冷靜、理性、稍微帶點機器的口吻，為 '繩匠' (玩家) 分析今日的調頻 (抽卡) 運勢。目前的 S 級保底計數為 ${pityS}/90。請用繁體中文回答，字數 100 字以內。`;
            
            const text = await generateContent(prompt);
            aiOutput.innerText = text;
        }

        async function analyzeSignal() {
            if (!lastSRankChar) return;
            
            aiModal.style.display = 'flex';
            aiOutput.innerHTML = `<span class="ai-loading">_DECRYPTING_SIGNAL_[${lastSRankChar}]...</span>`;
            
            const prompt = `你現在是遊戲《絕區零》中的資料庫。請簡短介紹角色 '${lastSRankChar}' 的戰鬥風格或背景故事，風格要像加密的檔案解密。請用繁體中文回答，字數 100 字以內。`;
            
            const text = await generateContent(prompt);
            aiOutput.innerText = text;
        }

        function closeAI() {
            aiModal.style.display = 'none';
        }

    </script>
</body>
</html>
