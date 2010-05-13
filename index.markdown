---
layout: default
title: Just Blog
---
{% for post in site.posts %} 
  <div class="container">
    <div class="blog_date">
      <span>{{ post.date | date_to_string }}</span>
    </div>
    <div class="blog_title">
      <h3><a href="./{{ post.url }}">{{ post.title }}</a></h3>
    </div>
    <div class="blog_content">
      {{ post.content | truncatewords:30 }}
    </div>
  </div>
{% endfor %}
