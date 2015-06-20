# Jekyll-Improved-Paginator-Plugin
Jekyll's built-in paginator sucks! You are forced to use index.html to paginate only posts, for reasons I don't understand, and you have to work-around with what I feel is too much restriction; so this repo contains a plugin that fixes that, or attempts to (would be great to contrib to mainline). You can list a specific collection, or all posts, and pagination works seamlessly supporting some edge use-cases I felt the paginator did not address.

# Usage:
 1. download the `_plugins/listing_pages.rb` and place in your `_plugins` folder
 2. In the page(s) you wish to use include the relevant frontmatter (changing as required)
    list_for: posts
    list_limit: 2
 3. Include the relevant liquid to list your objects
    
    ```liquid
    <div class="post">
    {% if page.pages >= 1 %}
    <ul class="post-list">
      Page {{ page.curpage }} of {{ page.pages }}, 
      {{ page.list_for }} {{ page.min_rec }} to {{ page.max_rec }}
      {% for item in page.list %}
        <li>
          <h2>
            <a class="post-link" href="{{ item.url | prepend: site.baseurl }}">{{ item.title }}</a>
          </h2>
          <span class="post-meta">{{ item.date | date: "%b %-d, %Y" }}</span>
          {{ item.excerpt }}
          <a href="{{ item.url | prepend: site.baseurl }}"><small>More...</small></a>
        </li>
      {% endfor %}
    </ul>
    {% endif %}
    {% if page.pages > 1 %}
      {% capture nextpg %}{{ page.curpage | to_i | plus: 1 }}{% endcapture %}
      {% capture prevpg %}{{ page.curpage | to_i | minus: 1 }}{% endcapture %}
      <div class="pagination">
      {% if page.curpage > 1 %}
        <a rel="prev" href="{{ page.page_baseurl | prepend: site.baseurl | append: prevpg | replace: '//', '/' }}">&laquo; Prev</a>
      {% endif %}
      {% for pg in (1..page.pages) %}
        {% if page.curpage == pg %}
        <span>{{ pg }}</span>
        {% else %}
        <a rel="prev" href="{{ page.page_baseurl | prepend: site.baseurl | append: pg | replace: '//', '/' }}">{{ pg }}</a>
        {% endif %}
      {% endfor %}
      {% if page.curpage < page.pages %}
        <a rel="prev" href="{{ page.page_baseurl | prepend: site.baseurl | append: nextpg | replace: '//', '/' }}">Next &raquo;</a>
      {% endif %}
      </div>
    {% endif %}
  </div>
    ```
    
 4. Save the file and restart Jekyll.

 > N.b.: If you specify a `list_for` that does not exist, or is invalid, this will error. As the intended use-case for this is to be staged to a site this is fine for production, however do not put this inside a Jekyll generator online, as if you screw up the front-matter your site may experience downtime.

# Todo:
 * Work on alternative sorting option per-page
 * Work on supporting listing anything Jekyll can access (files, collections, pages, posts)
 * Work on filtering what Jekyll is looking for
 * Work on extending to work with data files to generate listings
 
