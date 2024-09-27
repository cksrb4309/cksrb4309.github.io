---
title: "😘 자기소개"
layout: category
permalink: /introduction/profile/
taxonomy: profile
author_profile: true
sidebar_main: true
sidebar:
    nav: "docs"
---



{% assign posts = site.category.github-blog %}

{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}