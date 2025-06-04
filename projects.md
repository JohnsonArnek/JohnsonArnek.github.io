---
layout: page # Or 'default', or 'project_listing' if you create a custom one for this later
title: "My Projects"
permalink: /projects/ # This ensures the page is accessible at yoursite.com/projects/
# You can add other front matter like a description for SEO if your theme supports it
# description: "A curated list of projects I've worked on, showcasing my skills and interests."
---

<h1>{{ page.title }}</h1>

<p>Here's a selection of projects I've developed or contributed to. Click on any project to learn more about it.</p>

<div class="project-list">
  {% if site.projects.size > 0 %}
    {% for project in site.projects %}
      <article class="project-item">
        <h2><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h2>
        
        {% if project.short_description %}
          <p class="project-excerpt">{{ project.short_description }}</p>
        {% elsif project.description %} {# Fallback to 'description' if 'short_description' isn't available #}
          <p class="project-excerpt">{{ project.description | strip_html | truncatewords: 30 }}</p>
        {% endif %}

        {% if project.status %}
          <p><strong>Status:</strong> {{ project.status }}</p>
        {% endif %}

        {% if project.technologies and project.technologies.size > 0 %}
          <p class="project-technologies">
            <strong>Built with:</strong> {{ project.technologies | join: ", " }}
          </p>
        {% endif %}
        
        <p><a href="{{ project.url | relative_url }}" class="read-more-link">View Details →</a></p>
      </article>
      {% unless forloop.last %}<hr class="project-separator">{% endunless %}
    {% endfor %}
  {% else %}
    <p>No projects to display at the moment. Check back soon!</p>
  {% endif %}
</div>

<!-- Basic styling (you'll want to move this to your SASS/CSS file in Step 5) -->
<style>
  .project-list .project-item {
    margin-bottom: 2em;
    padding-bottom: 1em;
  }
  .project-list .project-item h2 {
    margin-bottom: 0.5em;
  }
  .project-list .project-excerpt {
    color: #555;
  }
  .project-list .project-technologies {
    font-size: 0.9em;
    color: #777;
  }
  .project-list .read-more-link {
    font-weight: bold;
  }
  .project-list .project-separator {
    border: 0;
    border-top: 1px solid #eee;
    margin: 2em 0;
  }
</style>
