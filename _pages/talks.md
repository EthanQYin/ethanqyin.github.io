---
# 这个页面不用手改：所有条目都来自 _data/talks.yml，加一次报告只需要在那个文件里加一条。
layout: page
permalink: /talks/
title: talks
nav: true
nav_order: 2
show_posters: true # 改成 false 就不显示 _data/talks.yml 里 type: poster 的条目
_styles: |
  .talks .talk-tag {
    display: inline-block;
    margin-left: 0.15rem;
    padding: 0.1rem 0.5rem;
    border: 1px solid var(--global-divider-color);
    border-radius: 999px;
    color: var(--global-text-color-light);
    font-size: 0.68rem;
    font-weight: 400;
    letter-spacing: 0.04em;
    line-height: 1.4;
    text-transform: uppercase;
    vertical-align: 0.12em;
    white-space: nowrap;
  }
  .talks .talk-tag.upcoming {
    border-color: var(--global-theme-color);
    color: var(--global-theme-color);
  }
---

{% assign talks = site.data.talks | sort: 'date' | reverse %}
{% if page.show_posters == false %}
{% assign talks = talks | where_exp: 'talk', "talk.type != 'poster'" %}
{% endif %}
{% assign talks_by_year = talks | group_by_exp: 'talk', "talk.date | date: '%Y'" %}
{% assign link_kinds = 'paper,slides,poster,video' | split: ',' %}

<div class="publications talks">
{% for year in talks_by_year %}
  <h2 class="bibliography">{{ year.name }}</h2>
  <ol class="bibliography">
  {% for talk in year.items %}
    {% assign has_title = false %}
    {% if talk.title and talk.title != '' %}{% assign has_title = true %}{% endif %}
    <li data-date="{{ talk.date | date: '%Y-%m-%d' }}">
      <div class="title">
        {% if has_title %}{{ talk.title }}{% else %}{{ talk.event }}{% endif %}
        {% if talk.type and talk.type != 'talk' %}<span class="talk-tag">{{ talk.type }}</span>{% endif %}
      </div>
      <div class="periodical">
        {% if has_title %}<em>{{ talk.event }}</em> &middot;{% endif %}
        {{ talk.location }} &middot; {{ talk.date | date: '%b %Y' }}
      </div>
      {% if talk.paper or talk.slides or talk.poster or talk.video %}
      <div class="links">
        {% for kind in link_kinds %}
          {% assign href = talk[kind] %}
          {% if href %}
            {% unless href contains '://' %}
              {% assign href = href | prepend: '/assets/pdf/' | relative_url %}
            {% endunless %}
            <a href="{{ href }}" class="btn btn-sm z-depth-0" role="button">{{ kind | capitalize }}</a>
          {% endif %}
        {% endfor %}
      </div>
      {% endif %}
    </li>
  {% endfor %}
  </ol>
{% endfor %}
</div>

<script>
  (function () {
    var now = new Date();
    var today = new Date(now.getTime() - now.getTimezoneOffset() * 60000).toISOString().slice(0, 10);
    document.querySelectorAll(".talks li[data-date]").forEach(function (li) {
      if (li.getAttribute("data-date") < today) return;
      var tag = document.createElement("span");
      tag.className = "talk-tag upcoming";
      tag.textContent = "upcoming";
      li.querySelector(".title").appendChild(tag);
    });
  })();
</script>
