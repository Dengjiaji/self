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
    
    /* Scope font to terminal only, protecting site nav */
    .terminal-container {
        font-family: var(--term-font) !important;
        max-width: 840px;
        margin: 0 auto;
        color: var(--term-fg);
        line-height: 1.6;
        position: relative;
        z-index: 1;
        min-height: 80vh;
        padding-bottom: 100px;
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
        opacity: 0.06;
        pointer-events: none;
    }

    /* Terminal Window Chrome */
    .term-window {
        border: 2px solid #000;
        background: rgba(255, 255, 255, 0.98);
        box-shadow: 15px 15px 0px rgba(0,0,0,0.1);
        margin-bottom: 40px;
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
    }

    .term-body {
        padding: 25px;
        overflow-y: auto;
    }

    /* ASCII & Typography */
    .ascii-art {
        font-weight: bold;
        white-space: pre;
        line-height: 1.1;
        margin-bottom: 20px;
        overflow-x: auto;
        font-size: 0.75em;
        color: #000;
    }

    .terminal-container h3 {
        font-size: 1.1em;
        margin: 0 0 10px 0;
        font-weight: bold;
        text-transform: uppercase;
        color: #000;
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
    
    /* Input Line Construction */
    .input-line {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        position: relative; /* Context for absolute input */
    }
    
    /* Fix: Input positioned invisibly over the area to prevent scroll jumps */
    #term-input {
        position: absolute;
        opacity: 0;
        height: 100%; /* Cover the line height */
        width: 1px; /* Minimal width */
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
        margin-bottom: 25px;
        padding-left: 0; 
        animation: fadeIn 0.2s ease-in-out;
    }
    
    .command-history-item {
        margin-bottom: 15px;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(5px); }
        to { opacity: 1; transform: translateY(0); }
    }
    
    .grid-2 {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 20px;
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
        .grid-2 { grid-template-columns: 1fr; }
        .ascii-art { font-size: 0.5em; }
    }
</style>

<!-- Canvas for Matrix Effect -->
<canvas id="matrix-bg"></canvas>

<div class="terminal-container">

    <!-- Main Terminal Window -->
    <div class="term-window">
        <div class="term-header">
            <span>user@tongyi-lab:~</span>
            <span>zsh</span>
        </div>
        <div class="term-body" id="terminal-output-area">
            
            <!-- Initial Welcome Message -->
            <div class="command-history-item">
<div class="ascii-art">
  ____  ____   ____  ____  ____      ___      ___  ____    ____ 
 |    ||    | /    ||    ||    |    |   \    /  _]|    \  /    |
 |__  | |  | |  o  ||__  | |  |     |    \  /  [_ |  _  ||   __|
 __|  | |  | |     |__|  | |  |     |  D  ||    _]|  |  ||  |  |
/  |  | |  | |  _  /  |  | |  |     |     ||   [_ |  |  ||  |_ |
\  `  | |  | |  |  \  `  | |  |     |     ||     ||  |  ||     |
 \____j|____||__|__|\____||____|    |_____||_____||__|__||___,_|
                                                                        
                                                
</div>
                <div style="margin-bottom: 20px; color: #666;">
                "All boundaries are conventions, waiting to be transcended." <br>
                -- Cloud Atlas
                </div>
                <div>Type <span class="tag">help</span> to see available commands.</div>
            </div>

            <!-- Static First Command -->
            <div class="command-history-item">
                <div><span class="prompt">➜  ~</span> <span class="user-input-text">whois jiaji</span></div>
                <div class="cmd-output">
                    Name: Jiaji Deng (邓佳佶)<br>
                    Role: Researcher @ Tongyi Lab<br>
                    Education: PKU B.S. Math & Finance → USC M.S. Mathematical Finance<br>
                    Interests: Agent Systems, Agentic RL, FinTech<br>
                    Email: dengjiaji@foxmail.com
                </div>
            </div>

            <!-- Dynamic content will be typed here by JS -->

        </div>

        <!-- Interactive Input Line -->
        <div style="padding: 0 25px 25px 25px;">
            <div class="input-line" id="input-line-container">
                <span class="prompt">➜  ~</span>
                <span id="input-display"></span><span class="cursor-block"></span>
                <input type="text" id="term-input" autocomplete="off" spellcheck="false">
            </div>
        </div>
    </div>

    <div style="text-align: center; color: #999; font-size: 0.8em; margin-top: 20px;">
        session_id: <span id="session-id"></span> • host: github.io
    </div>

</div>

<script>
    // --- 1. Matrix Background Effect ---
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


    // --- 2. Terminal System ---
    const input = document.getElementById('term-input');
    const display = document.getElementById('input-display');
    const outputArea = document.getElementById('terminal-output-area');
    const inputContainer = document.getElementById('input-line-container');
    const cursorBlock = document.querySelector('.cursor-block');
    
    document.getElementById('session-id').innerText = '0x' + Math.floor(Math.random()*16777215).toString(16).toUpperCase();

    // Input handling
    const focusInput = () => {
        // Prevent scroll jump by saving position? 
        // Actually fixing CSS 'top: -9999px' to 'position: absolute' in container solves most jumps.
        input.focus({ preventScroll: true }); 
    };
    document.addEventListener('click', focusInput);
    inputContainer.addEventListener('click', focusInput);

    input.addEventListener('input', () => {
        display.textContent = input.value;
    });

    // Output Templates
    const outputs = {
        help: () => `
            <table style="width:100%">
                <tr><td style="width:120px">help</td><td>Show this help message</td></tr>
                <tr><td>whois [user]</td><td>Display user profile</td></tr>
                <tr><td>list [type]</td><td>List items (music, books, publications)</td></tr>
                <tr><td>cat [file]</td><td>View file content</td></tr>
                <tr><td>clear</td><td>Clear terminal screen</td></tr>
                <tr><td>blog</td><td>Navigate to blog index</td></tr>
            </table>`,
        
        whois: () => `
            Name: Jiaji Deng (邓佳佶)<br>
            Role: Researcher @ Tongyi Lab, Alibaba<br>
            Education: PKU B.S. Math & Finance → USC M.S. Mathematical Finance<br>
            Interests: Agent Systems, Agentic RL, FinTech<br>
            Email: dengjiaji@foxmail.com<br>
            `,

            
        evotraders: () => `
            <h6>[ PROJECT: EvoTraders ]</h6>
            <div style="margin-bottom: 10px; color: #444;">"AI agents trading as a team, not solo players."</div>
            <div>
                <div class="term-list-item"><span class="term-list-marker">[+]</span><div><b>Multi-Agent Collaboration</b>: Data + Strategy + Risk Agents</div></div>
                <div class="term-list-item"><span class="term-list-marker">[+]</span><div><b>Memory Evolution</b>: Powered by ReMe for continuous learning</div></div>
                <div class="term-list-item"><span class="term-list-marker">[+]</span><div><b>Real-Time Execution</b>: Live market interaction via AgentScope</div></div>
            </div>`,
            
        publications: () => `
            <div>
                <div class="term-list-item">
                    <span class="term-list-marker">></span>
                    <a href="https://scholar.google.com/citations?hl=zh-CN&user=hI2BbTMAAAAJ"><b>[PROFILE] Google Scholar</b></a>
                </div>
                <div class="term-list-item">
                    <span class="term-list-marker">></span>
                    <a href="https://www.dedao.cn/ebook/detail?id=XOnaYG1qlM7amvGYerDZOy9JVnXL40BoYVzWBkp1NKxoRdb86P2Q5AzgEj9vE5rD"><b>[BOOK] 数智化转型：人工智能的金融实践</b></a>
                </div>
                <div class="term-list-item">
                    <span class="term-list-marker">></span>
                    <a href="https://book.douban.com/subject/35074482/"><b>[BOOK] 专注力的技术</b></a>
                </div>
            </div>`,
            
        music: () => `
            <div>
                <b>Album: AI self</b> <span style="font-size: 0.9em; color: #666;">(Electronic / Experimental)</span><br>
                > <a href="https://music.163.com/#/album?id=190682220">Listen on NetEase Cloud Music</a>
            </div>`
    };

    // Execution Logic
    const executeCommand = (cmdStr) => {
        const args = cmdStr.trim().split(' ');
        const cmd = args.shift().toLowerCase();
        
        if (cmd === 'help') return outputs.help();
        if (cmd === 'whois') return outputs.whois();
        if (cmd === 'whoami') return outputs.whois(); // alias
        if (cmd === 'clear') { outputArea.innerHTML = ''; return null; }
        if (cmd === 'hello') return `Hello! Nice to meet you.<br>Try: <span class="tag">list music</span>`;
        if (cmd === 'blog') {
            setTimeout(() => window.location.href = "blog/", 800);
            return "Redirecting...";
        }
        
        if (cmd === 'list') {
            const type = args[0] ? args[0].toLowerCase() : '';
            if (type === 'books' || type === 'publications') return outputs.publications();
            if (type === 'music') return outputs.music();
            return "Usage: list [books|music|publications]";
        }
        
        if (cmd === 'cat') {
            const file = args[0];
            if (file && file.includes('current_project')) return outputs.evotraders();
            if (file === 'about.md') return outputs.whois();
            return `cat: ${file || ''}: No such file`;
        }
        
        return `zsh: command not found: ${cmd}`;
    };

    // Handle User Enter
    input.addEventListener('keydown', function(e) {
        if (e.key === 'Enter') {
            const rawInput = this.value;
            if (!rawInput.trim()) return;
            
            // Add to history
            const historyEntry = document.createElement('div');
            historyEntry.className = 'command-history-item';
            const safeInput = rawInput.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
            historyEntry.innerHTML = `<div><span class="prompt">➜  ~</span> <span class="user-input-text">${safeInput}</span></div>`;
            
            // Execute
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
            
            // Scroll to bottom (using requestAnimationFrame to ensure DOM updated)
            requestAnimationFrame(() => {
                 window.scrollTo(0, document.body.scrollHeight);
            });
        }
    });


    // --- 3. Typewriter Sequence for Intro ---
    // This simulates the user typing commands upon page load
    
    const typeWriterQueue = [
        { text: "cat current_project.md | grep 'EvoTraders' -A 5", delay: 800 },
        { text: "list publications", delay: 1500 },
        { text: "list music", delay: 1500 }
    ];

    async function runTypewriter() {
        // Disable user input during animation
        input.disabled = true;
        cursorBlock.style.display = 'none'; // Use our fake cursor for animation if we wanted, 
                                            // but simpler to just update the display span
        
        for (const item of typeWriterQueue) {
            await new Promise(r => setTimeout(r, item.delay));
            
            // Type text char by char
            for (let i = 0; i <= item.text.length; i++) {
                display.textContent = item.text.substring(0, i);
                // Scroll to bottom as we type
                window.scrollTo(0, document.body.scrollHeight); 
                await new Promise(r => setTimeout(r, Math.random() * 30 + 30));
            }
            
            await new Promise(r => setTimeout(r, 300)); // Pause before enter
            
            // Simulate Enter
            const historyEntry = document.createElement('div');
            historyEntry.className = 'command-history-item';
            historyEntry.innerHTML = `<div><span class="prompt">➜  ~</span> <span class="user-input-text">${item.text}</span></div>`;
            
            const outputHtml = executeCommand(item.text);
            if (outputHtml !== null) {
                const outputDiv = document.createElement('div');
                outputDiv.className = 'cmd-output';
                outputDiv.innerHTML = outputHtml;
                historyEntry.appendChild(outputDiv);
                outputArea.appendChild(historyEntry);
            }
            
            display.textContent = '';
            window.scrollTo(0, document.body.scrollHeight);
        }
        
        // Re-enable user input
        input.disabled = false;
        input.focus({ preventScroll: true });
        cursorBlock.style.display = 'inline-block';
    }

    // Start sequence
    window.addEventListener('load', runTypewriter);

</script>
