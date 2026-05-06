---
hide:
  - navigation
  - toc
---

<style>
  .home {
    max-width: 760px;
    margin: 0 auto;
    padding: 48px 20px 72px;
    color: #1f2933;
  }

  .home a {
    color: #1d4ed8;
    text-decoration-thickness: 1px;
    text-underline-offset: 3px;
  }

  .home a:hover {
    color: #0f172a;
  }

  .home-hero {
    display: grid;
    grid-template-columns: 96px 1fr;
    gap: 24px;
    align-items: center;
    margin-bottom: 40px;
  }

  .home-avatar {
    width: 96px;
    height: 96px;
    border-radius: 18px;
    object-fit: cover;
    border: 1px solid #d8dee9;
  }

  .home-kicker {
    margin: 0 0 6px;
    color: #64748b;
    font-size: 0.95rem;
  }

  .home h1 {
    margin: 0;
    color: #111827;
    font-size: 2.25rem;
    line-height: 1.12;
    letter-spacing: 0;
  }

  .home-intro {
    margin: 14px 0 0;
    max-width: 650px;
    color: #374151;
    font-size: 1.03rem;
    line-height: 1.75;
  }

  .home-section {
    padding: 28px 0;
    border-top: 1px solid #e5e7eb;
  }

  .home-section h2 {
    margin: 0 0 14px;
    color: #111827;
    font-size: 1.16rem;
    line-height: 1.3;
    letter-spacing: 0;
  }

  .home-list {
    margin: 0;
    padding-left: 1.1rem;
    color: #374151;
    line-height: 1.75;
  }

  .home-list li + li {
    margin-top: 8px;
  }

  .home-meta {
    color: #64748b;
  }

  .home-links {
    display: flex;
    flex-wrap: wrap;
    gap: 10px 18px;
    margin-top: 18px;
    font-size: 0.98rem;
  }

  @media (max-width: 640px) {
    .home {
      padding: 32px 4px 56px;
    }

    .home-hero {
      grid-template-columns: 72px 1fr;
      gap: 16px;
      margin-bottom: 28px;
    }

    .home-avatar {
      width: 72px;
      height: 72px;
      border-radius: 14px;
    }

    .home h1 {
      font-size: 1.9rem;
    }
  }
</style>

<main class="home">
  <header class="home-hero">
    <img class="home-avatar" src="figure/icon.jpg" alt="Jiaji Deng profile image">
    <div>
      <p class="home-kicker">Researcher at Tongyi Lab, Alibaba</p>
      <h1>Jiaji Deng</h1>
      <p class="home-intro">
        I work on agent systems, agentic reinforcement learning, and financial AI.
        My current interests center on systems that can reason, act, learn, and
        keep useful state across real time.
      </p>
      <nav class="home-links" aria-label="Profile links">
        <a href="mailto:dengjiaji@gmail.com">Email</a>
        <a href="https://github.com/Dengjiaji">GitHub</a>
        <a href="https://scholar.google.com/citations?hl=zh-CN&amp;user=hI2BbTMAAAAJ">Google Scholar</a>
      </nav>
    </div>
  </header>

  <section class="home-section" aria-labelledby="research-interests">
    <h2 id="research-interests">Research Interests</h2>
    <ul class="home-list">
      <li>Agent systems and proactive agents</li>
      <li>Agentic reinforcement learning</li>
      <li>Financial technology and market-facing AI systems</li>
    </ul>
  </section>

  <section class="home-section" aria-labelledby="selected-work">
    <h2 id="selected-work">Selected Work</h2>
    <ul class="home-list">
      <li><a href="https://scholar.google.com/citations?hl=zh-CN&amp;user=hI2BbTMAAAAJ">Google Scholar profile</a></li>
      <li><a href="http://trading.evoagents.cn">EvoTraders</a> <span class="home-meta">AI agents trading as a team</span></li>
      <li><a href="https://www.dedao.cn/ebook/detail?id=XOnaYG1qlM7amvGYerDZOy9JVnXL40BoYVzWBkp1NKxoRdb86P2Q5AzgEj9vE5rD">数智化转型：人工智能的金融实践</a></li>
      <li><a href="https://book.douban.com/subject/35074482/">专注力的技术</a></li>
    </ul>
  </section>

  <section class="home-section" aria-labelledby="writing">
    <h2 id="writing">Writing</h2>
    <ul class="home-list">
      <li><a href="blog/2025-11-19/">Proactive Agents</a> <span class="home-meta">Notes on triggers, scheduling, and long-running agent systems</span></li>
    </ul>
  </section>

  <section class="home-section" aria-labelledby="contact">
    <h2 id="contact">Contact</h2>
    <ul class="home-list">
      <li>Email: <a href="mailto:dengjiaji@gmail.com">dengjiaji@gmail.com</a></li>
      <li>GitHub: <a href="https://github.com/Dengjiaji">github.com/Dengjiaji</a></li>
      <li>Google Scholar: <a href="https://scholar.google.com/citations?hl=zh-CN&amp;user=hI2BbTMAAAAJ">Jiaji Deng</a></li>
    </ul>
  </section>
</main>
