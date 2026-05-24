---
layout: page
title: "Jason 'vanRijn' Kasper"
---

Software engineer by day, dad-of-three by night, accidental blogger since 2000.

By day I write software at Apple. The rest of the time, life happens — my darling bride, three kids, faith, movies, video games, code, fountain pens and Japanese paper, the occasional adventurous home improvement project. This site is the [running record](/posts/) of all of it, going back to 2000 — when I have something to say (and sometimes when I don't).

{% assign post = site.posts.first %}
{% if post %}
<section style="margin-top: 2.5rem;">
  <h2 style="margin-bottom: 1rem;">Latest from the blog</h2>
  <article>
    <h3 style="margin: 0 0 0.25rem;"><a href="{{ post.url | relative_url }}" rel="bookmark">{{ post.title }}</a></h3>
    <p style="margin: 0 0 0.75rem; color: #888; font-size: 0.9em;">
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
    </p>
    {% if post.excerpt %}
      <div>{{ post.excerpt }}</div>
      <p><a href="{{ post.url | relative_url }}">Read more →</a></p>
    {% endif %}
  </article>
</section>
{% endif %}

<section style="margin-top: 2.5rem;">
  <h2 style="margin-bottom: 1rem;">Find me elsewhere</h2>
  <ul style="list-style: none; padding: 0; margin: 0; display: flex; flex-wrap: wrap; gap: 1.25rem;">
    {% for link in site.data.social %}
      <li><a href="{{ link.url }}"{% if link.rel %} rel="{{ link.rel }}"{% endif %}>{{ link.title }}</a></li>
    {% endfor %}
  </ul>
</section>
