---
title: "About"
layout: archive
permalink: /categories/About/
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.about %}
{% for post in posts %}
{% include archive-single.html type=page.entries_layout %}
{% endfor %}
