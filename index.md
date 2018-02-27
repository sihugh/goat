---
layout: default
---
<div class="home">
  {% if page.title %}
    <h1 class="page-heading">{{ page.title }}</h1>
  {% endif %}

  {% if site.posts.size > 0 %}
    <h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>
    <ul class="post-list">
      {% for post in site.posts %}
      <li>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.date | date: "%Y-%m-%d" }} - {{ post.title | downcase | escape }}
          </a>
        </h3>
        {% if site.show_excerpts %}
          {{ post.excerpt }}
        {% endif %}
      </li>
      {% endfor %}
    </ul>

    <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
  {% endif %}

</div>
