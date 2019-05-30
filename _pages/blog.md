---
layout: page
permalink: blog.html
title: Blog
aside:
  toc: true
---

<div class="layout--archive js-all">
  {%- include tags.html -%}
  <div class="js-result layout--archive__result d-none">
    {%- include article-list.html articles=site.posts type='brief' show_info=true reverse=true group_by='year' -%}
  </div>
</div>

<script>
  {%- include scripts/archieve.js -%}
</script>
