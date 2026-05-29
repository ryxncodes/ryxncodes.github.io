---
title: Projects
description: Practical IT, systems administration, and cybersecurity projects covering Windows support, PowerShell automation, Active Directory labs, governance tools, and portfolio work.
icon: fas fa-diagram-project
order: 1
---

<style>
  .projects-intro {
    margin-bottom: 1.5rem;
  }

  .project-status-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: .75rem;
    margin: 1.25rem 0 1.75rem;
  }

  .project-status-card {
    border: 1px solid var(--main-border-color);
    border-radius: 8px;
    padding: .85rem 1rem;
    background: var(--card-bg);
  }

  .project-status-card strong {
    display: block;
    font-size: 1.45rem;
    line-height: 1;
    color: var(--heading-color);
  }

  .project-status-card span {
    display: block;
    margin-top: .35rem;
    font-size: .85rem;
    color: var(--text-muted-color);
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .project-card {
    border: 1px solid var(--main-border-color);
    border-radius: 8px;
    padding: 1.1rem;
    background: var(--card-bg);
  }

  .project-card h2 {
    margin: 0 0 .55rem;
    font-size: 1.15rem;
  }

  .project-meta {
    display: flex;
    flex-wrap: wrap;
    gap: .45rem;
    margin-bottom: .8rem;
  }

  .project-pill {
    display: inline-flex;
    align-items: center;
    gap: .35rem;
    border: 1px solid var(--main-border-color);
    border-radius: 999px;
    padding: .22rem .55rem;
    font-size: .78rem;
    line-height: 1.2;
    color: var(--text-muted-color);
  }

  .project-pill::before {
    content: "";
    width: .45rem;
    height: .45rem;
    border-radius: 999px;
    background: var(--text-muted-color);
  }

  .project-pill.finished::before {
    background: #2da44e;
  }

  .project-pill.progress::before {
    background: #0969da;
  }

  .project-pill.lab::before {
    background: #bf8700;
  }

  .project-pill.archived::before {
    background: #6e7781;
  }

  .project-pill.featured {
    border-color: rgba(45, 164, 78, .45);
    color: var(--heading-color);
  }

  .project-pill.featured::before {
    background: #2da44e;
  }

  .project-card p {
    margin-bottom: .75rem;
  }

  .project-detail {
    margin: .75rem 0;
    padding: 0;
    list-style: none;
  }

  .project-detail li {
    margin: .45rem 0;
  }

  .project-detail strong {
    color: var(--heading-color);
  }

  .project-tracker {
    margin: .9rem 0 1rem;
  }

  .project-tracker-label {
    display: flex;
    justify-content: space-between;
    gap: .75rem;
    margin-bottom: .35rem;
    font-size: .82rem;
    color: var(--text-muted-color);
  }

  .project-meter {
    height: .5rem;
    overflow: hidden;
    border-radius: 999px;
    background: var(--main-border-color);
  }

  .project-meter span {
    display: block;
    height: 100%;
    border-radius: inherit;
    background: linear-gradient(90deg, #2da44e, #0969da);
  }

  .project-actions {
    margin-top: .85rem;
  }

  .project-actions a {
    display: inline-flex;
    align-items: center;
    gap: .4rem;
    font-weight: 600;
  }

  @media (max-width: 575px) {
    .projects-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<p class="projects-intro">
  A running snapshot of what I have built, what I am actively improving, and what I am using as a lab to keep sharpening my IT, scripting, and security skills.
</p>

<div class="project-status-grid" aria-label="Project status summary">
  <div class="project-status-card">
    <strong>2</strong>
    <span>finished</span>
  </div>
  <div class="project-status-card">
    <strong>2</strong>
    <span>in progress</span>
  </div>
  <div class="project-status-card">
    <strong>2</strong>
    <span>lab</span>
  </div>
  <div class="project-status-card">
    <strong>0</strong>
    <span>archived</span>
  </div>
</div>

<div class="projects-grid">
  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill progress">in progress</span>
      <span class="project-pill featured">featured</span>
      <span class="project-pill">TypeScript</span>
      <span class="project-pill">Next.js</span>
      <span class="project-pill">Prisma</span>
    </div>
    <h2>AI Governance Toolkit</h2>
    <p>A workspace app for tracking AI vendors, policies, reviews, evidence, and risk decisions.</p>
    <ul class="project-detail">
      <li><strong>Problem:</strong> Teams need a repeatable way to document AI usage, vendor reviews, and governance decisions without losing the evidence behind them.</li>
      <li><strong>Tech:</strong> TypeScript, Next.js, Prisma, PostgreSQL-style data modeling, authentication, and automated verification scripts.</li>
    </ul>
    <div class="project-tracker" aria-label="AI Governance Toolkit progress">
      <div class="project-tracker-label">
        <span>Core workflow</span>
        <span>70%</span>
      </div>
      <div class="project-meter"><span style="width: 70%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="https://github.com/ryxncodes/ai-governance-toolkit" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>

  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill finished">finished</span>
      <span class="project-pill featured">featured</span>
      <span class="project-pill">PowerShell</span>
      <span class="project-pill">Windows 11</span>
      <span class="project-pill">Endpoint support</span>
    </div>
    <h2>Windows 11 Migration Script</h2>
    <p>A PowerShell readiness checker built during a large Windows 11 migration effort.</p>
    <ul class="project-detail">
      <li><strong>Problem:</strong> Manual checks for TPM, Secure Boot, RAM, disk layout, and drive type were slowing down endpoint migration work.</li>
      <li><strong>Tech:</strong> PowerShell, CIM queries, background jobs, hardware checks, and workstation troubleshooting logic.</li>
    </ul>
    <div class="project-tracker" aria-label="Windows 11 Migration Script progress">
      <div class="project-tracker-label">
        <span>Ready for reuse</span>
        <span>100%</span>
      </div>
      <div class="project-meter"><span style="width: 100%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="https://github.com/ryxncodes/Windows-11-Migration-Script" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>

  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill lab">lab</span>
      <span class="project-pill featured">featured</span>
      <span class="project-pill">PowerShell</span>
      <span class="project-pill">Active Directory</span>
      <span class="project-pill">Windows Server</span>
    </div>
    <h2>Windows 11 Active Directory Administration Lab</h2>
    <p>A hands-on lab for practicing Windows administration, domain workflows, and repeatable support tasks.</p>
    <ul class="project-detail">
      <li><strong>Problem:</strong> Admin skills stick better when they are practiced in a controlled environment that mirrors real help desk and sysadmin work.</li>
      <li><strong>Tech:</strong> Windows 11, Windows Server concepts, Active Directory, PowerShell, user and device administration.</li>
    </ul>
    <div class="project-tracker" aria-label="Active Directory lab progress">
      <div class="project-tracker-label">
        <span>Lab coverage</span>
        <span>55%</span>
      </div>
      <div class="project-meter"><span style="width: 55%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="https://github.com/ryxncodes/Windows-11-Active-Directory-Administration-Lab" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>

  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill finished">finished</span>
      <span class="project-pill">Python</span>
      <span class="project-pill">Automation</span>
      <span class="project-pill">Data extraction</span>
    </div>
    <h2>Roblox Outfit Scraper</h2>
    <p>A Python scraper for collecting Roblox outfit data in a repeatable way.</p>
    <ul class="project-detail">
      <li><strong>Problem:</strong> Repetitive browser lookups are slow when the same public outfit data needs to be gathered consistently.</li>
      <li><strong>Tech:</strong> Python, web requests, parsing, structured output, and small automation workflows.</li>
    </ul>
    <div class="project-tracker" aria-label="Roblox Outfit Scraper progress">
      <div class="project-tracker-label">
        <span>Usable script</span>
        <span>90%</span>
      </div>
      <div class="project-meter"><span style="width: 90%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="https://github.com/ryxncodes/Roblox-Outfit-Scraper" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>

  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill progress">in progress</span>
      <span class="project-pill">Jekyll</span>
      <span class="project-pill">GitHub Pages</span>
      <span class="project-pill">Writing</span>
    </div>
    <h2>Portfolio and Writeups Site</h2>
    <p>This site: a place to collect CTF notes, project writeups, certification reflections, and practical IT learning.</p>
    <ul class="project-detail">
      <li><strong>Problem:</strong> Work samples are easier to trust when the reasoning, tradeoffs, and lessons learned are visible in one place.</li>
      <li><strong>Tech:</strong> Jekyll, Chirpy, Markdown, GitHub Pages, self-hosted static assets, and simple content workflows.</li>
    </ul>
    <div class="project-tracker" aria-label="Portfolio site progress">
      <div class="project-tracker-label">
        <span>Portfolio polish</span>
        <span>75%</span>
      </div>
      <div class="project-meter"><span style="width: 75%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="https://github.com/ryxncodes/ryxncodes.github.io" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>

  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill lab">lab</span>
      <span class="project-pill">Swift</span>
      <span class="project-pill">macOS</span>
      <span class="project-pill">UI utility</span>
    </div>
    <h2>OpenFolderIcons</h2>
    <p>A small macOS utility experiment around folder icon workflows.</p>
    <ul class="project-detail">
      <li><strong>Problem:</strong> Personal desktop workflows get smoother when repetitive visual customization steps are easier to repeat.</li>
      <li><strong>Tech:</strong> Swift, macOS app concepts, local file workflows, and lightweight utility design.</li>
    </ul>
    <div class="project-tracker" aria-label="OpenFolderIcons progress">
      <div class="project-tracker-label">
        <span>Experiment maturity</span>
        <span>40%</span>
      </div>
      <div class="project-meter"><span style="width: 40%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="https://github.com/ryxncodes/OpenFolderIcons" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>
</div>
