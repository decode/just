---
layout: default
title: Just Blog
---

<p>
  {% for post in site.posts %} 
    <div class="blog_date">
      <span>{{ post.date | date_to_string }}</span><br><br>
    </div>

    <h3><a href="./{{ post.url }}">{{ post.title }}</a></h3>
    <p>
      {{ post.content }}
    </p>
    <br>
  {% endfor %}
</p>
