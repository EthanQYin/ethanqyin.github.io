---
layout: page
permalink: /coffee-chat/
title: coffee chat
description: 15 minutes on Zoom · Mondays and Fridays around noon, Chicago time
nav: true
nav_order: 3
booking:
  embed: https://scheduler.zoom.us/ethan-yin-h7h6ns/chat-with-ethan # Zoom Scheduler 预约页的链接。清空就退回"发邮件约时间"的版本
  url: # 不想内嵌、只放一个预约按钮时填这个（任何预约工具的链接都行）
_styles: |
  .coffee-chat-booking {
    margin: 2rem 0;
  }
  .coffee-chat-booking iframe {
    display: block;
    width: 100%;
    height: 45rem;
    border: 0;
  }
  @media (max-width: 576px) {
    .coffee-chat-booking iframe {
      height: 56rem;
    }
  }
  .coffee-chat-booking .booking-note {
    margin-top: 0.75rem;
    color: var(--global-text-color-light);
    font-size: 0.875rem;
  }
  .coffee-chat-booking a.booking-button {
    display: inline-block;
    padding: 0.5rem 1.5rem;
    border: 1px solid var(--global-theme-color);
    border-radius: 0.25rem;
    color: var(--global-theme-color);
    font-weight: 400;
  }
  .coffee-chat-booking a.booking-button:hover {
    background-color: var(--global-theme-color);
    color: var(--global-hover-text-color);
    text-decoration: none;
  }
---

Always welcome to talk about research, PhD life, running, orienteering, etc.{% unless page.booking.embed or page.booking.url %} Just email me at [qichuan@uchicago.edu](mailto:qichuan@uchicago.edu?subject=Coffee%20chat) to find a time.{% endunless %}

{% if page.booking.embed %}
{% assign embed_src = page.booking.embed %}
{% if embed_src contains 'zoom.us' %}
{% unless embed_src contains 'embed=true' %}
{% if embed_src contains '?' %}
{% assign embed_src = embed_src | append: '&embed=true' %}
{% else %}
{% assign embed_src = embed_src | append: '?embed=true' %}
{% endif %}
{% endunless %}
{% endif %}

<div class="coffee-chat-booking">
  <iframe src="{{ embed_src }}" title="Book a coffee chat" loading="lazy"></iframe>
  <p class="booking-note">
    Calendar not loading? <a href="{{ page.booking.embed }}">Open the booking page</a>.
  </p>
</div>

{% elsif page.booking.url %}

<div class="coffee-chat-booking">
  <a class="booking-button" href="{{ page.booking.url }}">Book a 15-minute slot</a>
</div>

{% endif %}
