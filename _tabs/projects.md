---
title: Projects
description: Practical IT, systems administration, and cybersecurity projects covering Windows support, PowerShell automation, and Active Directory administration.
icon: fas fa-diagram-project
order: 1
---

<style>
  .projects-intro {
    margin-bottom: 1.5rem;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }

  .project-card {
    display: flex;
    flex-direction: column;
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
    margin: auto 0 1rem;
    padding-top: .9rem;
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
    display: flex;
    flex-wrap: wrap;
    gap: .85rem;
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

<div class="projects-grid">
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
      <a href="/posts/Windows_11_PowerShell_Script/"><i class="fas fa-book-open"></i> Write-up</a>
      <a href="https://github.com/ryxncodes/Windows-11-Migration-Script" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i> GitHub</a>
    </div>
  </article>

  <article class="project-card">
    <div class="project-meta">
      <span class="project-pill finished">finished</span>
      <span class="project-pill featured">featured</span>
      <span class="project-pill">PowerShell</span>
      <span class="project-pill">Active Directory</span>
      <span class="project-pill">Windows Server</span>
    </div>
    <h2>Windows 11 Active Directory Administration Lab</h2>
    <p>A built and validated Windows domain backed by a seven-script PowerShell administration toolkit.</p>
    <ul class="project-detail">
      <li><strong>Automation:</strong> Health checks, user provisioning, stale-account review, guarded cleanup, group reporting, and GPO backups.</li>
      <li><strong>Validation:</strong> Tested in the live domain with a final health result of 31 passes, 0 warnings, and 0 failures.</li>
    </ul>
    <div class="project-tracker" aria-label="Active Directory lab progress">
      <div class="project-tracker-label">
        <span>Lab complete</span>
        <span>100%</span>
      </div>
      <div class="project-meter"><span style="width: 100%;"></span></div>
    </div>
    <div class="project-actions">
      <a href="/posts/building-active-directory-lab/"><i class="fas fa-book-open"></i> Write-up</a>
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

</div>
