---
layout: default
title: 📝 Blogs
permalink: /blogs/
---


# Blogs

<p>I document and share insights on topics that interest me. Here are all the blogs I've written so far.</p>

<ul>
  {% if site.categories.blog %}
    {% assign blog_posts = site.categories.blog | sort: 'date' | reverse %}
    {% for post in blog_posts %}
      <li>
        <a href="{{ post.url | relative_url }}" class="list-title">{{ post.title }}</a>
        <span class="list-date">{{ post.date | date: "%b %d, %Y" }}</span>
      </li>
    {% endfor %}
    {% if blog_posts.size == 0 %}
      <li><em>No blog posts found.</em></li>
    {% endif %}
  {% else %}
    <li><em>No blog posts found.</em></li>
  {% endif %}
</ul>