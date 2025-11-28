---
hide:
  - navigation
  - toc
---

<!-- Import JetBrains Mono -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">

<style>
    :root {
        --term-bg: #ffffff;
        --term-fg: #1a1a1a;
        --term-input: #008000;
        --term-prompt: #000000;
        --term-font: 'JetBrains Mono', 'Courier New', monospace;
    }
    
    /* Scope font to terminal only */
    .terminal-container {
        font-family: var(--term-font) !important;
        max-width: 700px;
        margin: 5vh auto;
        color: var(--term-fg);
        line-height: 1.6;
        position: relative;
        z-index: 1;
    }

    .terminal-container * {
        font-family: var(--term-font) !important;
    }

    /* Matrix Background */
    #matrix-bg {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: -1;
        opacity: 0.04;
        pointer-events: none;
    }

    /* Terminal Window Chrome */
    .term-window {
        border: 2px solid #000;
        background: rgba(255, 255, 255, 0.98);
        height: 500px;
        display: flex;
        flex-direction: column;
        overflow: hidden;
    }
    
    .term-header {
        background: #000;
        color: #fff;
        padding: 8px 12px;
        font-weight: bold;
        font-size: 0.85em;
        border-bottom: 2px solid #000;
        display: flex;
        justify-content: space-between;
        align-items: center;
        cursor: default;
        text-transform: uppercase;
        letter-spacing: 1px;
        opacity: 0; /* Hidden initially */
        transition: opacity 0.5s;
    }

    .term-body {
        padding: 20px;
        flex: 1;
        overflow-y: auto;
        scroll-behavior: smooth;
    }

    .term-body::-webkit-scrollbar {
        width: 8px;
    }
    .term-body::-webkit-scrollbar-track {
        background: #f1f1f1;
    }
    .term-body::-webkit-scrollbar-thumb {
        background: #888;
    }
    .term-body::-webkit-scrollbar-thumb:hover {
        background: #555;
    }

    /* ASCII & Typography */
    .ascii-art {
        font-weight: bold;
        white-space: pre;
        line-height: 1.1;
        margin-bottom: 20px;
        font-size: 0.70em;
        color: #000;
        display: inline-block;
    }

    .terminal-container a {
        color: var(--term-fg);
        text-decoration: none !important;
        border-bottom: 1px solid #000;
        transition: all 0.1s;
        cursor: pointer;
    }

    .terminal-container a:hover {
        background: #000;
        color: #fff;
        text-decoration: none;
    }

    .prompt {
        color: var(--term-prompt);
        font-weight: bold;
        margin-right: 10px;
        white-space: nowrap;
    }
    
    .user-input-text {
        color: var(--term-input);
        font-weight: bold;
    }
    
    .input-line {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        position: relative;
        min-height: 24px;
    }
    
    #term-input {
        position: absolute;
        opacity: 0;
        height: 100%;
        width: 1px;
        bottom: 0;
        left: 0;
        z-index: -1;
        padding: 0;
        margin: 0;
        border: none;
    }

    #input-display {
        white-space: pre-wrap;
        word-break: break-all;
        color: var(--term-input);
        font-weight: bold;
    }

    .cursor-block {
        display: inline-block;
        width: 10px;
        height: 1.2em;
        background: var(--term-input);
        animation: blink 1s step-end infinite;
        vertical-align: middle;
    }
    
    /* Intro & Effects */
    .intro-text {
        color: #008000;
        font-weight: bold;
        font-size: 1.1em;
        margin-bottom: 10px;
    }
    
    /* Rabbit - Clickable */
    .rabbit-container {
        margin: 30px 0;
        color: #000;
        font-weight: bold;
        white-space: pre;
        font-size: 14px;
        cursor: pointer;
        display: inline-block;
        transition: transform 0.2s;
    }
    
    .rabbit-container:hover {
        transform: scale(1.1);
    }

    /* Pills - Terminal Style */
    .pill-container {
        display: flex;
        justify-content: center;
        gap: 40px;
        margin-top: 30px;
        margin-bottom: 30px;
    }

    .pill {
        font-family: var(--term-font);
        font-size: 16px;
        cursor: pointer;
        transition: all 0.2s;
        user-select: none;
        border-bottom: 2px solid transparent;
        padding: 5px 10px;
        font-weight: bold;
    }
    
    .pill:hover {
        background: #000;
        color: #fff !important;
        border-bottom: 2px solid #000;
    }
    
    .pill-red {
        color: #d32f2f;
        border-bottom: 2px solid #d32f2f;
    }
    
    .pill-blue {
        color: #1976d2;
        border-bottom: 2px solid #1976d2;
    }
    
    .pill-quote {
        text-align: center;
        color: #000;
        margin-bottom: 20px;
        font-size: 1em;
        line-height: 1.6;
    }
    
    .choice-link {
        font-family: var(--term-font);
        font-weight: bold;
        cursor: pointer;
        transition: all 0.2s;
        user-select: none;
        padding: 5px 10px;
        display: inline-block;
        color: #008000;
        border-bottom: 2px solid #008000;
    }
    
    .choice-link:hover {
        background: #008000;
        color: #fff;
    }

    @keyframes blink {
        0%, 100% { opacity: 1; }
        50% { opacity: 0; }
    }

    .tag {
        display: inline-block;
        border: 1px solid #000;
        padding: 0px 6px;
        font-size: 0.8em;
        margin-right: 5px;
        font-weight: bold;
        text-transform: uppercase;
    }

    .cmd-output {
        margin-left: 0;
        margin-bottom: 15px;
        padding-left: 0; 
        animation: fadeIn 0.2s ease-in-out;
    }
    
    .command-history-item {
        margin-bottom: 10px;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(5px); }
        to { opacity: 1; transform: translateY(0); }
    }
    
    .term-list-item {
        margin-bottom: 4px;
        display: flex;
    }
    .term-list-marker {
        margin-right: 10px;
        font-weight: bold;
        min-width: 25px;
    }

    @media (max-width: 600px) {
        .ascii-art { font-size: 0.5em; }
        .pill-container { gap: 30px; }
    }
</style>

<canvas id="matrix-bg"></canvas>

<div class="terminal-container">
    <div class="term-window">
        <div class="term-header" id="term-header">
            <span>system@matrix</span>
            <span>zsh</span>
        </div>
        <div class="term-body" id="terminal-output-area">
            <!-- Content injected by JS -->
        </div>

        <!-- Input Area -->
        <div style="padding: 0 20px 20px 20px; display:none;" id="input-area-wrapper">
            <div class="input-line" id="input-line-container">
                <span class="prompt" id="prompt-span">➜  ~</span>
                <span id="input-display"></span><span class="cursor-block"></span>
                <input type="text" id="term-input" autocomplete="off" spellcheck="false">
            </div>
        </div>
    </div>

    <div style="text-align: center; color: #999; font-size: 0.8em; margin-top: 10px;">
        session_id: <span id="session-id"></span> • host: github.io
    </div>
</div>

<script>
    // --- CONFIGURATION ---
    const PROFILE = {
        name: "Jiaji Deng (邓佳佶)",
        role: "Researcher @ Tongyi Lab, Alibaba",
        edu: "PKU B.S. Math & Finance → USC M.S. Mathematical Finance",
        interests: "Agent Systems, Agentic RL, FinTech",
        email: "dengjiaji@gmail.com",
        intro_quote: '"All boundaries are conventions, waiting to be transcended." -- Cloud Atlas'
    };

    // Blogs updated from mkdocs.yml
    const BLOGS = [
        { title: "Proactive Agents", path: "blog/2025-11-19/" }
    ];

    const PUBLICATIONS = [
        { title: "[PROFILE] Google Scholar", url: "https://scholar.google.com/citations?hl=zh-CN&user=hI2BbTMAAAAJ" },
        { title: "[BOOK] 数智化转型：人工智能的金融实践", url: "https://www.dedao.cn/ebook/detail?id=XOnaYG1qlM7amvGYerDZOy9JVnXL40BoYVzWBkp1NKxoRdb86P2Q5AzgEj9vE5rD" },
        { title: "[BOOK] 专注力的技术", url: "https://book.douban.com/subject/35074482/" }
    ];

    // --- 1. Matrix Background ---
    const canvas = document.getElementById('matrix-bg');
    const ctx = canvas.getContext('2d');

    function resizeCanvas() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    const chars = "01"; 
    const fontSize = 14;
    const columns = canvas.width / fontSize;
    const drops = [];
    for (let i = 0; i < columns; i++) drops[i] = 1;

    function drawMatrix() {
        ctx.fillStyle = 'rgba(255, 255, 255, 0.05)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#000';
        ctx.font = fontSize + 'px monospace';
        for (let i = 0; i < drops.length; i++) {
            const text = chars.charAt(Math.floor(Math.random() * chars.length));
            if (Math.random() > 0.975) ctx.fillText(text, i * fontSize, drops[i] * fontSize);
            if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
            drops[i]++;
        }
    }
    setInterval(drawMatrix, 50);

    // --- 2. Terminal Logic ---
    const input = document.getElementById('term-input');
    const display = document.getElementById('input-display');
    const outputArea = document.getElementById('terminal-output-area');
    const inputContainer = document.getElementById('input-line-container');
    const termHeader = document.getElementById('term-header');
    
    document.getElementById('session-id').innerText = '0x' + Math.floor(Math.random()*16777215).toString(16).toUpperCase();

    // State
    let isIntroMode = true;
    
    const focusInput = (e) => { 
        // Don't interfere with link clicks
        if (e.target.tagName === 'A') return;
        if(!isIntroMode) input.focus({ preventScroll: true }); 
    };
    document.addEventListener('click', focusInput);
    inputContainer.addEventListener('click', focusInput);

    input.addEventListener('input', () => { display.textContent = input.value; });

    // Command Outputs
    const getBlogList = () => {
        let html = `<div><b>[BLOG POSTS]</b></div>`;
        BLOGS.forEach(b => {
            html += `<div class="term-list-item"><span class="term-list-marker">></span><a href="${b.path}">${b.title}</a></div>`;
        });
        return html;
    };

    const getPubs = () => {
        let html = `<div>`;
        PUBLICATIONS.forEach(p => {
            html += `<div class="term-list-item"><span class="term-list-marker">></span><a href="${p.url}"><b>${p.title}</b></a></div>`;
        });
        html += `</div>`;
        return html;
    };

    const outputs = {
        help: () => `
            <table style="width:100%">
                <tr><td style="width:120px">help</td><td>Show this help</td></tr>
                <tr><td>whois</td><td>Display profile</td></tr>
                <tr><td>blog</td><td>List blog posts</td></tr>
                <tr><td>list [type]</td><td>List items (music, books, pubs)</td></tr>
                <tr><td>clear</td><td>Clear screen</td></tr>
            </table>`,
        
        whois: () => `
            Name: ${PROFILE.name}<br>
            Role: ${PROFILE.role}<br>
            Education: ${PROFILE.edu}<br>
            Interests: ${PROFILE.interests}<br>
            Email: ${PROFILE.email}<br>
            `,
            
        evotraders: () => `
            <h6><a href="http://trading.evoagents.cn" target="_blank" rel="noopener noreferrer">[ PROJECT: EvoTraders ]</a></h6>
            <div style="margin-bottom: 10px; color: #444;">"AI agents trading as a team."</div>
            <div>
                <div class="term-list-item"><span class="term-list-marker">[+]</span><div><b>Multi-Agent design</b>: Multi-Agent Collaborative Trading</div></div>
                <div class="term-list-item"><span class="term-list-marker">[+]</span><div><b>Continuous Learning and Evolution</b>: Powered by ReMe</div></div>
                <div class="term-list-item"><span class="term-list-marker">[+]</span><div><b>Real-Time Market Trading</b>: Real-time market data integration, providing backtesting mode and live trading mode</div></div>
            </div>`,
            
        music: () => `
            <div>
                <b>Album: AI self</b> <span style="font-size: 0.9em; color: #666;">(Electronic / Experimental)</span><br>
                > <a href="https://music.163.com/#/album?id=190682220">Listen on NetEase Cloud Music</a>
            </div>`
    };

    const executeCommand = (cmdStr) => {
        const args = cmdStr.trim().split(' ');
        const cmd = args.shift().toLowerCase();
        
        if (cmd === 'help') return outputs.help();
        if (cmd === 'whois' || cmd === 'whoami') return outputs.whois();
        if (cmd === 'clear') { outputArea.innerHTML = ''; return null; }
        if (cmd === 'blog') return getBlogList();
        if (cmd === 'list') {
            const type = args[0] ? args[0].toLowerCase() : '';
            if (type === 'books' || type === 'publications' || type === 'pubs') return getPubs();
            if (type === 'music') return outputs.music();
            return "Usage: list [books|music|publications]";
        }
        if (cmd === 'cat') {
            if (args[0] && args[0].includes('current_project')) return outputs.evotraders();
            return `cat: ${args[0] || ''}: Permission denied or file missing`;
        }
        if (cmd === '') return null;
        return `zsh: command not found: ${cmd}`;
    };

    // Handle Enter
    input.addEventListener('keydown', function(e) {
        if (e.key === 'Enter') {
            const rawInput = this.value;
            if (!rawInput.trim()) return;
            
            // Add history
            const historyEntry = document.createElement('div');
            historyEntry.className = 'command-history-item';
            const safeInput = rawInput.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
            historyEntry.innerHTML = `<div><span class="prompt">➜  ~</span> <span class="user-input-text">${safeInput}</span></div>`;
            
            const outputHtml = executeCommand(rawInput);
            
            if (outputHtml !== null) {
                const outputDiv = document.createElement('div');
                outputDiv.className = 'cmd-output';
                outputDiv.innerHTML = outputHtml;
                historyEntry.appendChild(outputDiv);
                outputArea.appendChild(historyEntry);
            }

            this.value = '';
            display.textContent = '';
            
            // Keep scroll at bottom
            const termBody = document.querySelector('.term-body');
            requestAnimationFrame(() => {
                termBody.scrollTop = termBody.scrollHeight;
            });
        }
    });

    // --- 3. Intro Sequence ---
    
    async function typeText(text, speed = 100, clear = false, className = 'intro-text') {
        if (clear) outputArea.innerHTML = '';
        const line = document.createElement('div');
        line.className = className;
        outputArea.appendChild(line);
        
        for (let i = 0; i < text.length; i++) {
            line.textContent += text[i];
            await new Promise(r => setTimeout(r, speed));
        }
        return line;
    }

    async function askMatrixQuestion() {
        isIntroMode = true;
        input.disabled = true;
        document.getElementById('input-area-wrapper').style.display = 'none';
        termHeader.style.opacity = '0';
        
        await new Promise(r => setTimeout(r, 500));
        await typeText("Do you know THE MATRIX?", 80, true);
        await new Promise(r => setTimeout(r, 500));
        
        const choiceDiv = document.createElement('div');
        choiceDiv.style.marginTop = '20px';
        choiceDiv.innerHTML = `
            <div style="display: flex; gap: 30px; align-items: center;">
                <span class="prompt">➜</span>
                <span class="choice-link" onclick="answerMatrix(true)">YES</span>
                <span style="color: #666;">/</span>
                <span class="choice-link" onclick="answerMatrix(false)">NO</span>
            </div>
        `;
        outputArea.appendChild(choiceDiv);
    }
    
    window.answerMatrix = async (knowsMatrix) => {
        outputArea.innerHTML = '';
        if (knowsMatrix) {
            await runIntro();
        } else {
            enterTerminal();
        }
    };

    async function runIntro() {
        await new Promise(r => setTimeout(r, 300));
        await typeText("Wake up, Neo...", 150, true);
        await new Promise(r => setTimeout(r, 2000));
        
        await typeText("The Matrix has you...", 100, true);
        await new Promise(r => setTimeout(r, 2000));
        
        await typeText("Follow the white rabbit.", 100, true);
        await new Promise(r => setTimeout(r, 1000));
        
        const rabbitDiv = document.createElement('div');
        rabbitDiv.className = 'rabbit-container';
        rabbitDiv.innerHTML = `   \\ /\n  ( . .)\n  (")(")`; 
        rabbitDiv.onclick = () => {
            outputArea.innerHTML = '';
            showKnockKnock();
        };
        outputArea.appendChild(rabbitDiv);
    }
    
    async function showKnockKnock() {
        await typeText("Knock, knock...", 200, true);
        await new Promise(r => setTimeout(r, 1000));
        showPills();
    }
    
    function showPills() {
        outputArea.innerHTML = '';
        const choiceDiv = document.createElement('div');
        choiceDiv.style.marginTop = '40px';
        choiceDiv.innerHTML = `
            <div class="pill-quote">
                "This is your last chance. After this, there is no turning back.<br>
                You take the blue pill—the story ends. You take the red pill—you stay in Wonderland."
            </div>
            <div class="pill-container">
                <span class="pill pill-blue" onclick="choosePill('blue')">blue pill</span>
                <span class="pill pill-red" onclick="choosePill('red')">red pill</span>
            </div>
        `;
        outputArea.appendChild(choiceDiv);
    }
    
    window.choosePill = async (color) => {
        outputArea.innerHTML = '';
        if (color === 'blue') {
            await typeText("There is no one here...", 50);
            await new Promise(r => setTimeout(r, 2000));
            showPills();
        } else {
            await typeText("Welcome to the desert of the real.", 50);
            await new Promise(r => setTimeout(r, 1000));
            enterTerminal();
        }
    };
    
    async function enterTerminal() {
        outputArea.innerHTML = '';
        isIntroMode = true;
        input.disabled = true;
        document.getElementById('input-area-wrapper').style.display = 'none';
        termHeader.style.opacity = '1';
        termHeader.querySelector('span').textContent = 'user@tongyi-lab:~';
        
        // ASCII art as raw text for typing
        const asciiArt = `   ____  ____   ____  ____  ____      ___      ___  ____    ____ 
 |    ||    | /    ||    ||    |    |   \\    /  _]|    \\  /    |
 |__  | |  | |  o  ||__  | |  |     |    \\  /  [_ |  _  ||   __|
 __|  | |  | |     |__|  | |  |     |  D  ||    _]|  |  ||  |  |
/  |  | |  | |  _  /  |  | |  |     |     ||   [_ |  |  ||  |_ |
\\     | |  | |  |  \\     | |  |     |     ||     ||  |  ||     |
 \\____||____||__|__|\\____||____|    |_____||_____||__|__||_____|`;
        
        // Display ASCII art directly
        const artDiv = document.createElement('div');
        artDiv.className = 'ascii-art';
        artDiv.textContent = asciiArt;
        outputArea.appendChild(artDiv);
        
        // Display quote directly
        const quoteDiv = document.createElement('div');
        quoteDiv.className = 'intro-text';
        quoteDiv.textContent = PROFILE.intro_quote;
        outputArea.appendChild(quoteDiv);
        await new Promise(r => setTimeout(r, 500));
        
        const helpDiv = document.createElement('div');
        helpDiv.innerHTML = '<div>Type <span class="tag">help</span> to see available commands.</div>';
        outputArea.appendChild(helpDiv);
        
        await new Promise(r => setTimeout(r, 800));
        
        // Now enable terminal
        isIntroMode = false;
        input.disabled = false;
        document.getElementById('input-area-wrapper').style.display = 'block';
        
        // Run initial whois with typing effect
        await typeCommand('whois jiaji');
        
        input.focus();
        
        // Start Auto-Type Sequences
        runAutoCommands();
    }
    
    async function typeCommand(cmdStr) {
        // Show command being typed
        const historyEntry = document.createElement('div');
        historyEntry.className = 'command-history-item';
        const cmdDisplay = document.createElement('div');
        cmdDisplay.innerHTML = `<span class="prompt">➜  ~</span> <span class="user-input-text"></span>`;
        historyEntry.appendChild(cmdDisplay);
        outputArea.appendChild(historyEntry);
        
        const userInputSpan = cmdDisplay.querySelector('.user-input-text');
        for (let i = 0; i < cmdStr.length; i++) {
            userInputSpan.textContent += cmdStr[i];
            await new Promise(r => setTimeout(r, 40));
        }
        
        await new Promise(r => setTimeout(r, 300));
        
        // Execute and show output
        const outputHtml = executeCommand(cmdStr);
        if (outputHtml !== null) {
            const outputDiv = document.createElement('div');
            outputDiv.className = 'cmd-output';
            outputDiv.innerHTML = outputHtml;
            historyEntry.appendChild(outputDiv);
        }
        
        const termBody = document.querySelector('.term-body');
        termBody.scrollTop = termBody.scrollHeight;
    }
    
    // --- 4. Auto-Type Commands Sequence ---
    const autoCmdQueue = [
        { text: "cat current_project.md | grep 'EvoTraders' -A 5", delay: 1000 },
        { text: "list publications", delay: 1500 },
        { text: "list music", delay: 1500 }
    ];

    async function runAutoCommands() {
        // Wait a bit after initial load
        await new Promise(r => setTimeout(r, 1000));

        for (const item of autoCmdQueue) {
            // Wait before starting typing this command
            await new Promise(r => setTimeout(r, item.delay));
            
            // Simulate typing
            const cmd = item.text;
            for (let i = 0; i <= cmd.length; i++) {
                // Check if user interrupted by typing? (Optional: skip if user types)
                // For now, just overwrite display. But to be safe, if input.value is not empty, we pause or skip.
                if (input.value.length > 0) return; // Stop if user interacts

                display.textContent = cmd.substring(0, i);
                // Force scroll
                const termBody = document.querySelector('.term-body');
                termBody.scrollTop = termBody.scrollHeight;
                
                await new Promise(r => setTimeout(r, Math.random() * 30 + 30));
            }
            
            await new Promise(r => setTimeout(r, 300)); // Pause at end of line
            
            // Execute
            const historyEntry = document.createElement('div');
            historyEntry.className = 'command-history-item';
            historyEntry.innerHTML = `<div><span class="prompt">➜  ~</span> <span class="user-input-text">${cmd}</span></div>`;
            
            const outputHtml = executeCommand(cmd);
            if (outputHtml !== null) {
                const outputDiv = document.createElement('div');
                outputDiv.className = 'cmd-output';
                outputDiv.innerHTML = outputHtml;
                historyEntry.appendChild(outputDiv);
                outputArea.appendChild(historyEntry);
            }
            
            display.textContent = '';
            
            const termBody = document.querySelector('.term-body');
            termBody.scrollTop = termBody.scrollHeight;
        }
    }

    // Start
    window.addEventListener('load', askMatrixQuestion);

</script>
