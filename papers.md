---
layout: default
title: "📚 Papershelf"
permalink: /papers/
---

# Papershelf

<p>I read a few papers every week around various topics that interest me. Here are the most recent ones I've summarized.</p>

<ul>
  {% if site.categories.papers %}
    {% assign paper_posts = site.categories.papers | sort: 'date' | reverse %}
    {% for post in paper_posts %}
      <li>
        <a href="{{ post.url | relative_url }}" class="list-title">{{ post.title }}</a>
        <span class="list-date">{{ post.date | date: "%b %d, %Y" }}</span>
      </li>
    {% endfor %}
    {% if paper_posts.size == 0 %}
      <li><em>No papers found.</em></li>
    {% endif %}
  {% else %}
    <li><em>No posts found.</em></li>
  {% endif %}
</ul>
