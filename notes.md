---
layout: default
title: Notes
permalink: /notes/
---

# Notes

日々の小さな発見、学び、記録を残しています。

仕事、AI、プログラミング、英語、日本文化、箱根の日常、猫、料理など、形式にこだわらず投稿します。

## All Notes

<ul>
{% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <small>{{ post.date | date: "%Y年%-m月%-d日" }}</small>
  </li>
{% endfor %}
</ul>
