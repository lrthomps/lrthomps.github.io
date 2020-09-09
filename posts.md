---
layout: page
---

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: '%b %Y' }}):
      
      <p>{{ post.summary }}</p>
    </li>
  {% endfor %}
</ul>

<a href="{{ "feed.xml" | relative_url }}" title="posts">
            <img src="{{ 'assets/images/rss-orange.png' | relative_url }}" height=25px></a>
