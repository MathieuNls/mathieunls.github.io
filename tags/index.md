---
layout: page
---
<style>
// for tag cloud and archives
.tag-cloud {
  list-style: none;
  padding: 0;
  text-align: justify;
  font-size: 16px;
  li {
    display: inline-block;
    margin: 0 12px 12px 0;
  }
}
#archives {
  padding: 5px;
}
.archive-group {
  margin: 5px;
  border-top: 1px solid #ddd;
}
.archive-item {
  margin-left: 5px;
}
.post-tags {
  text-align: right;
}
</style>

<ul class="tag-cloud">
{% for tag in site.tags %}
  <li style="font-size: {{ tag | last | size | times: 100 | divided_by: site.tags.size | plus: 70  }}%">
    <a href="#{{ tag | first | slugize }}">
      {{ tag | first }}
    </a>
  </li>
{% endfor %}
</ul>

<div id="archives">
{% for tag in site.tags %}
  <div class="archive-group">
    {% capture tag_name %}{{ tag | first }}{% endcapture %}
    <h3 id="#{{ tag_name | slugize }}">{{ tag_name }}</h3>
    <a name="{{ tag_name | slugize }}"></a>
    {% for post in site.tags[tag_name] %}
    <article class="archive-item">
      <h4><a href="{{ root_url }}{{ post.url }}">{{post.title}}</a></h4>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>
