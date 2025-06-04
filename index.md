---
layout: home
title: Welcome to the Idea Graveyard
---

<div class="home-intro">
  <h1>Welcome to the Idea Graveyard! 💀</h1>
  <p class="lead">I'm VB, a professional Jack of all trades, master of none. This is my digital resting place for <a href="{{ "/blog/" | relative_url }}">musings and writings</a> and a showcase for <a href="{{ "/projects/" | relative_url }}">side projects</a> and explorations across a spectrum of interests – from art and AI to coding, economics, and beyond.</p>
</div>

<hr class="home-section-divider">

<section class="home-section">
  <h2><a href="{{ "/blog/" | relative_url }}">Latest from the Crypt (Writings)</a></h2>
  {% if site.posts.size > 0 %}
    <ul class="post-list-condensed">
      {% for post in site.posts limit:3 %}
        <li class="post-item">
          <span class="post-meta">{{ post.date | date: "%B %-d, %Y" }}</span>
          <h3><a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
          {% if post.excerpt %}
            <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 35 }} <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a></p>
          {% endif %}
        </li>
      {% endfor %}
    </ul>
    <p class="view-all-link"><a href="{{ "/blog/" | relative_url }}">Unearth all writings …</a></p>
  {% else %}
    <p>The crypt is quiet for now... No writings unearthed yet. Stay tuned!</p>
  {% endif %}
</section>

<hr class="home-section-divider">

<section class="home-section">
  <h2><a href="{{ "/projects/" | relative_url }}">Featured Experiments (Projects)</a></h2>
  {% if site.projects.size > 0 %}
    <div class="featured-projects-grid">
      {% assign featured_projects = site.projects | where_exp: "project", "project.featured == true" | limit:3 %}
      {% if featured_projects.size == 0 %}
        {% assign featured_projects = site.projects | limit:3 %}
      {% endif %}

      {% for project in featured_projects %}
        <div class="project-card">
          {% if project.image %}
            <a href="{{ project.url | relative_url }}">
              <img src="{{ project.image | relative_url }}" alt="{{ project.image_alt | default: project.title }}" class="project-card-image">
            </a>
          {% endif %}
          <div class="project-card-content">
            <h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>
            <p class="project-card-description">
              {{ project.short_description | default: project.description | strip_html | truncatewords: 20 }}
            </p>
            <a href="{{ project.url | relative_url }}" class="button project-card-button">Examine Specimen</a>
          </div>
        </div>
      {% endfor %}
    </div>
    
    {% assign total_projects = site.projects.size %}
    {% assign num_featured_shown = featured_projects.size %}

    {% if total_projects > 3 or (num_featured_shown > 0 and num_featured_shown < total_projects) %}
      <p class="view-all-link"><a href="{{ "/projects/" | relative_url }}">Explore all experiments …</a></p>
    {% endif %}
    
  {% else %}
    <p>The lab is currently empty... No experiments to showcase yet. Check back for new creations!</p>
  {% endif %}
</section>

<!-- 
  REMEMBER TO MOVE THESE STYLES TO YOUR SASS FILES LATER!
-->
<style>
  .home-intro { text-align: center; margin-bottom: 2.5em; }
  .home-intro h1 { margin-bottom: 0.3em; }
  .home-intro .lead { font-size: 1.25em; color: #555; margin-bottom: 1em;}
  .home-section-divider { margin: 2.5em 0; border: 0; border-top: 1px solid #eee; }
  .home-section h2 { margin-bottom: 1em; text-align: center; }
  .home-section h2 a { text-decoration: none; color: inherit; }
  .home-section h2 a:hover { text-decoration: underline; }
  .post-list-condensed { list-style: none; padding-left: 0; }
  .post-list-condensed .post-item { margin-bottom: 1.8em; }
  .post-list-condensed .post-meta { display: block; font-size: 0.85em; color: #777; margin-bottom: 0.3em; }
  .post-list-condensed .post-item h3 { margin-top: 0; margin-bottom: 0.4em; font-size: 1.4em; }
  .post-list-condensed .post-item h3 a { text-decoration: none; }
  .post-list-condensed .post-excerpt { font-size: 0.95em; color: #555; margin-bottom: 0.5em; }
  .post-list-condensed .post-excerpt .read-more { font-weight: bold; text-decoration: none; }
  .featured-projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5em; margin-bottom: 1.5em; }
  .project-card { border: 1px solid #e0e0e0; border-radius: 8px; overflow: hidden; display: flex; flex-direction: column; background-color: #fff; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
  .project-card-image { width: 100%; height: 180px; object-fit: cover; }
  .project-card-content { padding: 1em; flex-grow: 1; display: flex; flex-direction: column; }
  .project-card-content h3 { margin-top: 0; font-size: 1.25em; margin-bottom: 0.5em; }
  .project-card-content h3 a { text-decoration: none; }
  .project-card-description { font-size: 0.9em; color: #666; flex-grow: 1; margin-bottom: 1em; }
  .project-card-button { display: inline-block; padding: 8px 15px; background-color: #007bff; color: white; text-decoration: none; border-radius: 4px; text-align: center; margin-top: auto; }
  .project-card-button:hover { background-color: #0056b3; }
  .view-all-link { text-align: center; margin-top: 1.5em; font-size: 1.1em; }
</style>
