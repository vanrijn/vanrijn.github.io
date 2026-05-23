---
layout: page
title: Home
alt_title: "Jason 'vanRijn' Kasper"
sub_title: Software engineer by day, dad-of-three by night, accidental blogger since 2000.
---

By day I write software at Apple. The rest of the time, life happens — my darling bride, three kids, faith, movies, video games, code, fountain pens and Japanese paper, the occasional adventurous home improvement project. This site is the [running record](/posts/) of all of it, going back to 2000 — when I have something to say (and sometimes when I don't).

<ul style="list-style: none; padding: 0; margin: 2.5rem 0 0; display: flex; flex-wrap: wrap; gap: 1.5rem;">
  {% for link in site.data.social %}
    <li><a href="{{ link.url }}"{% if link.rel %} rel="{{ link.rel }}"{% endif %}><span class="icon icon--{{ link.icon }}">{% include {{ link.icon | prepend: 'icon-' | append: '.svg' }} %}</span> {{ link.title }}</a></li>
  {% endfor %}
</ul>
