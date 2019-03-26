---
layout: page
title: Notes
permalink: /notes/
---


I've started writing as I think it'll help deepen my understanding of the topics I'm interested in. Feedback welcome.

{% for post in site.posts %}
- `{{ post.date | date: "%Y-%m-%d" }}` - [{{ post.title }}]({{ post.url }}) {% endfor %}
