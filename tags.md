---
layout: default
author_profile: true
title: Tags
permalink: /tags/
---

<div id="main" role="main">
  {% include sidebar.html %}

  <article class="page" itemscope itemtype="http://schema.org/CreativeWork">
    <div class="page__inner-wrap">
      <!-- Get the tag name for every tag on the site and set them
      to the `site_tags` variable. -->
      {% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}

      <!-- `tag_words` is a sorted array of the tag names. -->
      {% assign tag_words = site_tags | split:',' | sort %}

      <!-- List of all tags -->
      <footer>
        <p class="page__taxonomy">
          <strong><i class="fa fa-fw fa-tags" aria-hidden="true"></i>Tags:</strong>
          <span itemprop="keywords">
            
              {% for item in (0..site.tags.size) %}{% unless forloop.last %}
                {% capture this_word %}{{ tag_words[item] }}{% endcapture %}
                
                  <a href="#{{ this_word | cgi_escape }}" class="page__taxonomy-item">{{ this_word }}
                    <span>({{ site.tags[this_word].size }})</span>
                  </a>
                
              {% endunless %}{% endfor %}
           
          </span>
        </p>
      </footer>
      


      <!-- Posts by Tag -->
      <div>
        {% for item in (0..site.tags.size) %}{% unless forloop.last %}
          {% capture this_word %}{{ tag_words[item] }}{% endcapture %}
          <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
          {% for post in site.tags[this_word] %}{% if post.title != null %}
            <div>
              <span style="float: left;">
                <a href="{{ post.url }}">{{ post.title }}</a>
              </span>
              <span style="float: right;">
                {{ post.date | date_to_string }}
              </span>
            </div>
            <div style="clear: both;"></div>
          {% endif %}{% endfor %}

        {% endunless %}{% endfor %}

      </div>
    </div>
  </article>
</div>