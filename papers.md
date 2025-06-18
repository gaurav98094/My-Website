---
layout: default
title: "📚 Papershelf"
permalink: /papers/
---

# Papershelf

<div class="tag-filter">
  <div class="tag-filter-header">Filter by topic:</div>
  <div class="tag-buttons">
    <button class="tag-button active" data-tag="all">All</button>
    {% assign paper_posts = site.categories.papers %}
    {% assign paper_tags = paper_posts | map: "tags" | uniq | sort %}
    {% for tag in paper_tags %}
      <button class="tag-button" data-tag="{{ tag }}">{{ tag }}</button>
    {% endfor %}
  </div>
</div>

<ul class="paper-list">
  {% assign paper_posts = site.categories.papers | sort: 'date' | reverse %}
  {% for post in paper_posts %}
    <li class="paper-item" data-tags="{{ post.tags | join: ' ' }}">
      <a href="{{ post.url | relative_url }}" class="list-title">{{ post.title }}</a>
      <span class="list-date">{{ post.date | date: "%b %d, %Y" }}</span>
    </li>
  {% endfor %}
  {% if paper_posts.size == 0 %}
    <li><em>No papers found.</em></li>
  {% endif %}
</ul>

<style>
/* H2 heading styling */
h2 {
  color: #7c3aed !important;
  font-weight: 600;
  border-bottom: 2px solid #e5e7eb;
  padding-bottom: 0.5rem;
  margin-top: 2rem;
  margin-bottom: 1.5rem;
}

.tag-filter {
  margin: 2rem 0;
  padding: 1rem;
  background: #f6f8fd;
  border-radius: 0.8rem;
  box-shadow: 0 2px 8px rgba(99,102,241,0.04);
}

.tag-filter-header {
  font-weight: 600;
  color: #6366f1;
  margin-bottom: 0.8rem;
  font-size: 1.1rem;
}

.tag-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag-button {
  padding: 0.4rem 1rem;
  border: 1.5px solid #e5e7eb;
  border-radius: 0.6rem;
  background: white;
  color: #374151;
  font-size: 0.95rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.tag-button:hover {
  background: #f4f6fb;
  border-color: #6366f1;
  color: #6366f1;
}

.tag-button.active {
  background: #6366f1;
  color: white;
  border-color: #6366f1;
}

.paper-list {
  margin-top: 2rem;
}

.paper-item {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.paper-item.hidden {
  display: none;
  opacity: 0;
}

@media (max-width: 600px) {
  .tag-buttons {
    gap: 0.3rem;
  }
  
  .tag-button {
    padding: 0.3rem 0.8rem;
    font-size: 0.9rem;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const tagButtons = document.querySelectorAll('.tag-button');
  const paperItems = document.querySelectorAll('.paper-item');

  tagButtons.forEach(button => {
    button.addEventListener('click', () => {
      // Update active button
      tagButtons.forEach(btn => btn.classList.remove('active'));
      button.classList.add('active');

      const selectedTag = button.getAttribute('data-tag');

      // Filter papers
      paperItems.forEach(item => {
        if (selectedTag === 'all') {
          item.classList.remove('hidden');
        } else {
          const itemTags = item.getAttribute('data-tags').split(' ');
          if (itemTags.includes(selectedTag)) {
            item.classList.remove('hidden');
          } else {
            item.classList.add('hidden');
          }
        }
      });
    });
  });
});
</script>
