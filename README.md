# Jekyll-Improved-Paginator-Plugin
Jekyll's built-in paginator sucks! You are forced to use index.html to paginate only posts, for reasons I don't understand, and you have to work-around with what I feel is too much restriction; so this repo contains a plugin that fixes that, or attempts to (would be great to contrib to mainline). You can list a specific collection, or all posts, and pagination works seamlessly supporting some edge use-cases I felt the paginator did not address.

Usage:
 1. download the `_plugins/listing_pages.rb` and place in your `_plugins` folder
 2. In the page(s) you wish to use include the relevant frontmatter (changing as required)
    list_for: posts
    list_limit: 2
 3. Save the file and restart Jekyll.

 > N.b.: If you specify a `list_for` that does not exist, or is invalid, this will error. As the intended use-case for this is to be staged to a site this is fine for production, however do not put this inside a Jekyll generator online, as if you screw up the front-matter your site may experience downtime.

Todo:
======
 * Work on alternative sorting option per-page
 * Work on supporting listing anything Jekyll can access (files, collections, pages, posts)
 * Work on filtering what Jekyll is looking for
 * Work on extending to work with data files to generate listings
 
