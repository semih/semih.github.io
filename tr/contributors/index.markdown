---
layout: page
title: "katkıda bulun"
date: 2014-05-10 -0800
comments: false
categories: [personal blog]
sharing: false
lang: tr
---

Fark ettiğin problemlerin çözümüne katkı sağlayarak blog sitemi geliştirebilirsin. Bu şekilde bir talebin olursa, bana "pull request" göndermen yeterli!


Bloğumdaki her bir post için düzenle linki mevcut. Bu linke giderek postu tarayıcıdan kolayca düzenleyebilir, bana otomatik olarak pull request gönderebilirsin.

Veya [repository'mi ziyaret et]({{site.github_repo_url}}) ve bana pull request gönder.

<ul>
{% for contributor in site.github.contributors %}
  <li>
    <img src="{{ contributor.avatar_url }}" width="32" height="32" /> <a href="{{ contributor.html_url }}">{{ contributor.login }}</a>
  </li>
{% endfor %}
</ul>
