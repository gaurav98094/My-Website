---
layout: default
title: "Gaurav K"
description: "A personal research hub of papers, projects, and ideas"
title-heading: false
---

<style>
.hero {
  max-width: 800px;
  margin: 4rem auto;
  padding: 2.2rem 1.2rem 2.7rem 1.2rem;
  text-align: center;
  font-family: inherit;
  background: #fff;
  box-shadow: 0 4px 32px rgba(99,102,241,0.07);
  border-radius: 1.2rem;
}

.hero-img {
  width: 230px;
  height: 250px;
  max-width: 100%;
  object-fit: cover;
  border-radius: 50%;
  border: 4px solid #b3bcf6;
  margin-bottom: 1.3rem;
  box-shadow: 0 10px 36px rgba(99,102,241,0.15);
  background: #fff;
}

.hero h1 {
  font-size: 2.2rem;
  font-weight: 700;
  margin-bottom: 0.2rem;
  color: #23272f;
  letter-spacing: -0.5px;
  text-align: center;
}

.hero .subtitle {
  font-size: 0.93rem;
  color: #ef4444; /* red-500 */
  font-weight: 500;
  margin-bottom: 1.3rem;
  letter-spacing: 0.04em;
  text-align: center;
  max-width: 95vw;
  word-break: break-word;
  margin-left: auto;
  margin-right: auto;
  font-family: 'Fira Mono', 'JetBrains Mono', 'Menlo', monospace;
}

.hero-summary {
  font-size: 1.08rem;
  color: #444;
  margin: 0 auto 2.1rem auto;
  max-width: 600px;
  line-height: 1.7;
  text-align: left;
  background: #f6f8fd;
  border-radius: 0.7rem;
  padding: 1.2rem 1.5rem;
  box-shadow: 0 2px 8px rgba(99,102,241,0.04);
}

.social-links {
  margin: 1.7rem 0 0.7rem 0;
  display: flex;
  justify-content: center;
  gap: 1.2rem;
}

.social-links a {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: #f3f4f6;
  color: #6366f1;
  font-size: 1.5rem;
  transition: background 0.2s, color 0.2s;
  box-shadow: 0 2px 8px rgba(99,102,241,0.08);
  text-decoration: none;
}

.social-links a:hover {
  background: #6366f1;
  color: #fff;
}

.nav-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1.2rem;
  margin-top: 2rem;
}

.nav-grid a {
  display: block;
  padding: 1.2rem;
  border-radius: 1rem;
  background-color: #f3f4f6;
  color: #1f2937;
  text-decoration: none;
  font-weight: 500;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.04);
  transition: all 0.2s ease-in-out;
}

.nav-grid a:hover {
  background-color: #6366f1;
  color: white;
  transform: translateY(-3px);
  box-shadow: 0 8px 24px rgba(99, 102, 241, 0.18);
}

@media (max-width: 600px) {
  .container {
    width: 100vw;
    max-width: 100vw;
    min-width: 0;
    margin: 0;
    padding-left: 0.2rem;
    padding-right: 0.2rem;
    box-sizing: border-box;
  }
  .hero {
    width: 100%;
    max-width: 100vw;
    margin: 1.2rem 0 1.2rem 0;
    border-radius: 0;
    padding-left: 0.2rem;
    padding-right: 0.2rem;
    box-sizing: border-box;
  }
  .hero-img {
    width: 150px;
    height: 150px;
    max-width: 80vw;
    max-height: 40vw;
  }
  .hero-summary {
    font-size: 1.01rem;
    padding: 0.8rem 0.7rem;
    max-width: 100%;
    margin-left: 0.4rem;
    margin-right: 0.4rem;
  }
  .social-links {
    gap: 0.7rem;
  }
  .nav-grid {
    grid-template-columns: 1fr;
    gap: 0.7rem;
  }
  .nav-grid a {
    font-size: 1.01rem;
    padding: 0.9rem;
  }
  .recent-section {
    width: 100vw;
    max-width: 100vw;
    margin: 0;
    border-radius: 0;
    padding-left: 0;
    padding-right: 0;
  }
  .recent-list {
    gap: 0.7rem;
  }
  .recent-card {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.3rem;
    padding: 0.9rem 0.7rem 0.9rem 0.7rem;
  }
  .recent-title {
    font-size: 1.01rem;
  }
  .recent-date {
    margin-left: 0;
    font-size: 0.97rem;
  }
  .hero .subtitle {
    font-size: 0.88rem;
    max-width: 95vw;
    word-break: break-word;
    white-space: normal;
    margin-left: auto;
    margin-right: auto;
  }
}

.recent-section {
  margin: 2.5rem auto 0 auto;
  max-width: 700px;
  background: #fff;
  border-radius: 1rem;
  box-shadow: 0 2px 16px rgba(99,102,241,0.06);
  padding: 2rem 1.5rem 1.5rem 1.5rem;
}
.recent-section h2 {
  font-size: 1.32rem;
  font-weight: 700;
  color: #23272f;
  margin-bottom: 1.1rem;
  letter-spacing: -0.5px;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.recent-icon {
  font-size: 1.25em;
  vertical-align: middle;
}
.recent-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
}
.recent-card {
  background: linear-gradient(120deg, #f6f8fd 80%, #e0e7ff 100%);
  border-radius: 0.7rem;
  box-shadow: 0 2px 8px rgba(99,102,241,0.04);
  padding: 1.1rem 1.3rem 1.1rem 1.3rem;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  transition: box-shadow 0.18s, background 0.18s;
  border: 1px solid #e0e7ff;
}
.recent-card:hover {
  box-shadow: 0 4px 18px rgba(99,102,241,0.13);
  background: #f3f4f6;
}
.recent-title {
  color: #23272f;
  font-weight: 600;
  font-size: 1.08rem;
  text-decoration: none;
  transition: color 0.18s;
}
.recent-title:hover {
  color: #6366f1;
}
.recent-date {
  color: #8b949e;
  font-size: 0.99rem;
  margin-left: 1.2rem;
  white-space: nowrap;
  font-family: 'Inter', 'Segoe UI', 'Roboto', 'Helvetica Neue', Arial, sans-serif;
  font-weight: 500;
}
</style>

<div class="hero" style="text-align: center;">
  <img src="{{ '/img/me2.png' | relative_url }}" alt="Profile" class="hero-img" />
  <h1>Hey, I am Gaurav</h1>
  <div class="subtitle">curious, data-driven, and always learning</div>

  <div class="social-links" style="justify-content: center;">
    <a href="https://www.linkedin.com/in/gaurav98094/" target="_blank" title="LinkedIn" aria-label="LinkedIn">
      <svg width="22" height="22" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.761 0 5-2.239 5-5v-14c0-2.761-2.239-5-5-5zm-11 19h-3v-10h3v10zm-1.5-11.268c-.966 0-1.75-.784-1.75-1.75s.784-1.75 1.75-1.75 1.75.784 1.75 1.75-.784 1.75-1.75 1.75zm15.5 11.268h-3v-5.604c0-1.337-.025-3.063-1.868-3.063-1.868 0-2.154 1.459-2.154 2.968v5.699h-3v-10h2.881v1.367h.041c.401-.761 1.381-1.563 2.844-1.563 3.042 0 3.604 2.003 3.604 4.605v5.591z"/></svg>
    </a>
    <a href="https://github.com/gaurav98094" target="_blank" title="GitHub" aria-label="GitHub">
      <svg width="22" height="22" fill="currentColor" viewBox="0 0 24 24"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.387.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.416-4.042-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.084-.729.084-.729 1.205.084 1.84 1.236 1.84 1.236 1.07 1.834 2.809 1.304 3.495.997.108-.775.418-1.305.762-1.605-2.665-.305-5.466-1.334-5.466-5.931 0-1.31.469-2.381 1.236-3.221-.124-.303-.535-1.523.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.553 3.297-1.23 3.297-1.23.653 1.653.242 2.873.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.803 5.624-5.475 5.921.43.372.823 1.102.823 2.222 0 1.606-.014 2.898-.014 3.293 0 .322.216.694.825.576 4.765-1.588 8.199-6.084 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
    </a>
    <a href="mailto:gaurav98095@email.com" title="Email" aria-label="Email">
      <svg width="22" height="22" fill="currentColor" viewBox="0 0 24 24"><path d="M12 12.713l-11.985-7.713v15.001h23.97v-15.001l-11.985 7.713zm11.985-9.713h-23.97l11.985 7.713 11.985-7.713z"/></svg>
    </a>
    <a href="https://www.youtube.com/@gauravkds" target="_blank" title="YouTube" aria-label="YouTube" class="youtube">
      <svg width="22" height="22" fill="currentColor" viewBox="0 0 24 24"><path d="M23.498 6.186a2.994 2.994 0 0 0-2.112-2.116C19.425 3.5 12 3.5 12 3.5s-7.425 0-9.386.57A2.994 2.994 0 0 0 .502 6.186C0 8.15 0 12 0 12s0 3.85.502 5.814a2.994 2.994 0 0 0 2.112 2.116C4.575 20.5 12 20.5 12 20.5s7.425 0 9.386-.57a2.994 2.994 0 0 0 2.112-2.116C24 15.85 24 12 24 12s0-3.85-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
    </a>
  </div>

  <div class="hero-summary" style="text-align: center;">
    <b>Data Scientist ⚡ GenAI Engineer</b><br><br>
    I build ML systems that work — at scale, in prod, and on real business problems.<br><br>
    From MLOps to GenAI, cloud AI to messy data — I've shipped it.<br><br>
    Also teaching Data Science & AI on <b>YouTube</b>, breaking down tough tech for everyone.<br><br>
    <b>Let's build something impactful.</b>
  </div>

</div>

