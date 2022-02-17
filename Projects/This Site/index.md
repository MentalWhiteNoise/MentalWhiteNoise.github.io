---
layout: project
title: This Site&#58; Organizing My Project Notes
categories: [project, github, jekyll, github_pages]
project: this_site
---

The purpose of this site, as stated at my home page, is to share some ot the projects I've done, as well as capture notes for myself. I'd also like to be able to build this site as I learn new things, as opposed to only looking back.

* [{{page.title}}](#project-title)
  * TOC
  {:toc}
* [Related Articles](#articles)

## History

I have tried several different tools in order to document notes, web sites, steps, etc relating to different projects as I learn things. Nothing seems to work well. From links in favorites, folders on my system filled with txt notes, MS Word documents, Google Docs, MS OneNote, Evernote. I have backup drives and thumb drives and data on the cloud. No solution seems to give me the correct balance of quick and easy, allowing both quick notes as well as detailed, formalized tutorials. Every time I decide to work with or expand something I have learned I end up searching for my notes and files in all of these places, to see what I did previously. Well, here is me trying another tool.

## GitHub and Jekyll

So... how is this site made and why do I think it will work this time? Well, I don't necessarily think it will work this time; I'm a pessimist. But if it doesn't work, I still got to learn something new!

Work introduced me to various source control solutions (I am a DB guy, not a coder), including one [GitHub]. GitHub is awesome. It is complicated and difficult to learn all of the terminology and concepts behind it, but once you do, it opens up an entirely different world for people who either want to learn to code or have found free software that they love but "if only it did this *one* thing just a little differently..." So, what's a source control solution have to do with this site? Well, if you are at all familiar with [Mardown], a sort of shortcut for writing blogs and such (great cheat-sheet [here][Markdown Cheatsheet] for getting started), GitHub integrates with [Jekyll] to allow you to quickly and easily build a website from markdown (.md) files. Github even hosts it for you without cost! And, if you are a tinkerer like me, you don't have to settle for simple with your web site.

## Getting started

Okay, so I am just learning this. First, it starts with creating a GitHub account. It's free to sign up, as long as you publish your source code publicly. Here is a great article on creating an account: <http://www.wikihow.com/Create-an-Account-on-GitHub>. Next, I created a repository for my site, but the steps that GitHub provide (here: <https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/>) have you do it in a slightly different order. 

After following these instructions, I not only had my site working from this hosted URL, but I also got it running locally. This allows me to test changes much more quickly, and see the results.

## Structured Content

I did not want to go with the date-based posts that is more the default structure for GitHub Pages. I don't care when I update or publish a project, I care what the project is about, what technologies it uses, etc. So, the first thing I did was think about how I wanted to organize, store, and most importantly navigate this information, keeping in mind the strengths and weeknesses of the Markdown language and Jekyll.

- **Every page will have a link back to my home page**
  This may seem so obvious it isn't worth stating, but I am stating it none the less. I want a header on every page that the reader can quickly go to my home page. I don't think this site will be very deep, so it should only take a couple of clicks from the home page to get to any piece of information.
  
- **Links to me; info about me**
  Less critical, it would be nice to have links where the reader can contact me, find out more about me, get to my source code, etc. This information can be in the header or footer.
  
- **Every page will have a footer**
  Even if I decide to put most of the informatoin on the header, every page will also have a footer. I think this is a great way to balance posts and let the user know they've reach the end.
  
- **Every project will have a project page**
  I am project focused. Not all projects are entirely independant, but I should have at the very list a landing page for each project that explains what the project is and provides a little history.
  
- **Not every project can fit in a single post**
  In fact, I believe that most projects will require additional articles and posts. This will allow the reader to stay at a high level in understanding the project, or take a deep dive on any technical issue or note. However, when a project is very straight forward, the entire documentation about and around the project may be in a single post.
  
- **The home page should provide a list of project**
  Until I have so many projects that the home page just looks cluttered, I should have a list of all projects on the home page. This list should be a short description and a link to the project landing page.
  
- **All pages of a similar type should have a similar look and feel**
   Whether the home page, a project page, a project article, or a project notes page, each page should look similar, so "finding" content about different projects should be easy once the reader is used to this site. Each page type should also look a little different, so that a reader can quickly tell if they are on a project page or a technical article about an aspect of a project.
   
 - **A project page should list any supplimentary material**
   When a project has supplimentary material like articles or loose notes, it should list all materials at the end. The project page can also link to the material at specific points within where it makes sense, but even when this occurs, having a list of all related pages in a specific location will make navigation easier. 
   Note that this should be the same location as the list of projects on the home page.
      
## Pick a theme
I didn't really like any of the themes, but this seemed like a good starting point. So I picked [Slate] as a starting point.

I had to download the theme in order to test it. I extracted to a separate location and then copied over certain directories:
* _layouts
* _ssas 
* assets

I can now verify, for a properly created index.md file, it will display properly.

## Coding the layout of the site

First, I cleaned up the default.html file in the _layouts folder, getting rid of "if" sections that weren't used.

Next, I decided to start updating this template to allow the "every page" functionality I wanted (based on the structured content above).

### Every page will have a link back to my home page

  For now, since I am not worried about the exact format, I just wrapped the section in the header with the title.
{% raw %}
```md
<a href="{{ site.baseurl /}}"><h1 id="project_title">{{ site.title | default: site.github.repository_name }}</h1></a>
```
{% endraw %}
   
### Links to me; info about me
  
This template already has a nice banner area in the header where I can add links. I am not entirely sure what information I'll want, but I will start by modifying that.
{% raw %}
Replaced 
```md
<a id="forkme_banner" href="{{ site.github.repository_url }}">View on GitHub</a>
```
{% endraw %}

{% raw %}
With 
```md
<div id="menu_banner" >
  <ul>
    {% for pg in site.pages %}
      {% for cat in pg.categories %}
        {% if pg.title and cat == "menu" %}
    <li>
      <a href="{{ pg.url | prepend: site.baseurl }}">{{ pg.title }}</a>
    </li>
        {% endif %}
      {% endfor %}
    {% endfor %}
  </ul>
</div>
``` 
{% endraw %}
  
This will let me add pages to the site with a category of "menu" in the list of categories, and those pages will automatically get added to this header menu area.

Next, I needed to add the menu_banner css, similar to the forkme_banner, but withou the github icon, and with slightly adjusted coloration. I start by replacing my style.css from the assets/css folder, as instructed in the [theme readme].

{% raw %}
```md
---
---

@import "{{ site.theme }}";
```
{% endraw %}
  
Then I look at the _site/assets/css/style.css file to determine the formatting of the "forkme_banner" element, copy and then modify it. I also explored the generated html and made some additional small changes. And I discovered that superscript and subscript are not supported markdown tags. Inline styles don't work within searchable tags (like title), so I als created a couple of class styles to support this. Here is what my css ended up as (note that the blank line at the end of this file appears to be critical):

{% raw %}
```css
---
---

@import "{{ site.theme }}";

#menu_banner {
  display: block;
  position: absolute;
  top: 0;
  right: 10px;
  z-index: 10;
  padding: 10px 50px 10px 10px;
  color: #fff;
  background: #005077;
  font-weight: 700;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  border-bottom-left-radius: 2px;
  border-bottom-right-radius: 2px; }

#header_wrap a {
  color: #fff;
}

.sup {
  vertical-align: super;
}
.sub {
  vertical-align: sub;
}

``` 
{% endraw %}

### Every page will have a footer

Now that I have a place to store the links for personal info in the header, I want to address the footer. This theme does not have the footer I want... so instead of what's there, I am going to add a left and a right section, and provide quick contact info. I think I'll have my email on the left, and my github account on the right. Other than linking the GitHub repository for this site [here][This Site GitHub], I'll include a link to this site in an about page, so each page in the site is not too cluttered. 

I am going to replace this section:

{% raw %}
```md
<footer class="inner">
  {% if site.github.is_project_page %}
  <p class="copyright">{{ site.title | default: site.github.repository_name }} maintained by <a href="{{ site.github.owner_url }}">{{ site.github.owner_name }}</a></p>
  {% endif %}
  <p>Published with <a href="https://pages.github.com">GitHub Pages</a></p>
</footer>
```
{% endraw %}

With a few additional divs:
  
{% raw %}
```md  
<footer class="inner">
  <div id="footer-left">
    <span><a href="mailto:{{ site.email }}">{{ site.email }}</a></span>
  </div>
  <div id="footer-right">
    <span><a href="//github.com/{{ site.github_username }}"><img alt="The GitHub Logo" src="/assets/images/blacktocat.png" width="24" height="24">{{ site.github_username }}</a></span>
  </div>
</footer>
```
{% endraw %}

Of course, after adding these divs, it's back to the style.css to make this works the way I want. This took a little bit of trial and error.

{% raw %}
```css
/* URLs that are too long mess with mobile. This is a quick fix */
.project-content {
  overflow: hidden;
}

/* Lock the footer to keep a minimum width on mobile devices, and keep the footer looking good. */
#footer_wrap .inner {
  min-width: 375px;
}

#footer_wrap .inner div {  
  display: table;
  width: -webkit-calc(50%);
  width: calc(50%);
  float: left;
  height: 50px;
}

#footer_wrap span {
  display: table-cell;
  vertical-align: middle; 
}

#footer_wrap a {
  text-decoration: none;
}

#footer_wrap a:hover { 
  text-decoration: underline;
  font-weight: normal;
}

#footer_wrap img {
  vertical-align: middle;
  border: none;
  box-shadow: none;
}

#footer-left {
  text-align: left;
  vertical-align: middle;
}

#footer-right {
  text-align: right;
  vertical-align: middle;
}
```
{% endraw %}
   
### Every project will have a project page

The first thing I do to create the concept of a project page is to create a new layout for projects. I do this by creating a file, "project.html" in the "_layouts" folder. This layout will be based on the default layout, but will have some changes.

{% raw %}
```md
---
layout: default
---
<div class="project">

  <header class="project-header">
    <h1 id="project-title" class="project-title">{{ page.title }}</h1>
  </header>

  <article class="project-content">
    {{ content }}
  </article>
  
  {% include articlelist.html %}

</div>

```
{% endraw %}

The main differences of the project template is that I wrap the project related components, automatically pull in the title of the project (based on the title of the page), and include a list of articles in the footer. I will talk about this piece in the section on the requirement *A project page should list any supplimentary material*.

Implementing this new layout is as simple as creating a Markdown file (.md) with the correct header information.

{% raw %}
```md
------
layout: project
title: This Site
categories: [project, github, jekyll]
project: this_site
---
```
{% endraw %}

The layout is specified as "project", so it will use the correct layout. This layout expects a title, as it uses it in the "{% raw %}`{{ page.title }}`{% endraw %}" section. The list of categories contain keywords that I will use to quickly get a list of pages of a specific type (like projects) or about a specific topic (like GitHub). I also label the project, again for the requirement *A project page should list any supplimentary material*. The rest of the document is for the most part freeform, so it's up to me to use specific sections and structure in the contents of all project pages.

While not necessary, I have also created a folder called "Projects", and within that I create a different folder for each project. I also create the project page as the "index.md" file within each folder. This provides for a friendly url and a single location for all images and supporting articles and notes about a project.

* **Not every project can fit in a single post**

In addition to the project layout, I added a "page" layout to use for additional articles and posts. It is basically the same as the project layout, but a little simpler.

{% raw %}
```md
---
layout: default
---
<div class="post">

  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
  </header>

  <article class="post-content">
    {{ content }}
  </article>

</div>
```
{% endraw %}

Using it is straight forward. Most of the work is again in setting the correct header information.
{% raw %}
```md
---
layout: page
title: Special Characters in GitHub Pages
categories: [article, github, github_pages]
project: this_site
---
```
{% endraw %}

The layout should be "page". Again, the layout uses the title, so it should be provided. The category should include "article" or "note", and then again any topic identifiers that I may end up using later. The last and most important requirement is that the project matches the parent project.  
  
### The home page should provide a list of project

I create another layout for the home page, "home.html", again in the _layout folder. This isn't needed, but it helps me to keep the complex functionality centralized within the layouts, instead of the content pages. Also, I may want to change the structure of the home page at some point and diverge from the default. This gives me one place to make that change.
  
{% raw %}
```md
---
layout: default
---
{{ content }}

{% include projectlist.html %}
```
{% endraw %}

The functionality here that actually builds the list of projects is pulled from projectlist.html. This makes it easy for me, should I decide later, to include a list of projects somewhere else as well. It also centralizes my "lists" into a single location. I create an "_includes" folder and create this html file there. 

{% raw %}
```md
<h1 class="page-heading">Projects</h1>

<ul class="project-list">
  {% for post in site.pages %}
    {% for cat in post.categories %}
      {% if post.title and cat == "project" %}
    <li>
      <h2>
        <a class="project-link" href="{{ post.url | replace: 'index.html', '' | prepend: site.baseurl }}">{{ post.title }}</a>
      </h2>
    </li>
      {% endif %}
    {% endfor %}    
  {% endfor %}
</ul>
```
{% endraw %}

Currently there is no sorting, but this block of code will look through every page within the site, and if the page has a category called "project", it will add a block of HTML for that page as a list item, with a url to that page.
  
### All pages of a similar type should have a similar look and feel
   
This is satisfied through all of the layout templates that I have created, along with keeping the structure of my writing simple and straight forward.
   
### A project page should list any supplimentary material
  
Within the project layout was a section of code " {% raw %}`{% include articlelist.html %}`{% endraw %}". Similar to the what's in the home layout, this section copies the content of the articlelist.html page from the _includes directory. This page is a little more complex than projectlist.html...

{% raw %}
```md
{% assign c = 0 %}
{% for pg in site.pages %}
  {% if pg.project == page.project %}
    {% if pg.categories contains 'article' %}
      {% assign c = c | plus:1 %}
    {% endif %}
  {% endif %}
{% endfor %}

{% if c > 0 %}
  <h1 id="articles" class="page-heading">Articles</h1>
  <ul class="project-list">
  {% for pg in site.pages %}
    {% if pg.project == page.project %}
      {% for pcat2 in pg.categories %}
        {% if pcat2 == "article" %}
    <li>
      <h3>
        <a class="project-link" href="{{ pg.url | replace: 'index.html', '' | prepend: site.baseurl }}">{{ pg.title }}</a>
      </h3>
    </li>    
        {% endif %}
      {% endfor %}
    {% endif %}
  {% endfor %}
  </ul>
{% endif %}
```
{% endraw %}

Most of the logic is similar... but there are some obvious differences. First, this will look through each page within the site, and only if the "project" is the same as that defined in the page using the project template, and if the page within the site includes the category "article", then it will count that page. This basically counts the total number of articles within a project. Next, only if the article count is more than zero, it will again loop through with the same criteria, this time building a set of list items. Note that the articles section has an id. This allows linking to this section from within the document.

## What next

Well, I will try and update this project, or add supplementary articles, as I make changes to the structure of this site. You are reading this within the current published version, and the current repository (code that is driving the site) can be found [here][This Site GitHub].

I am also including some helpful links and miscellaneous notes for myself. 

## Usefull links

* Markdown Cheatsheet (<https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>)
* Jekyll & Liquid Cheatsheet (<https://gist.github.com/smutnyleszek/9803727>)
* Reference Github Pages Site (<https://github.com/MilanAryal/milanaryal.github.io/tree/master/assets/css>) (<https://milanaryal.com/writings/>)
* Setting up GotHub Pages site locally with Jekyll (<https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#next-steps-configuring-jekyll>)
* My site at GitHub (<https://github.com/MentalWhiteNoise/MentalWhiteNoise.github.io>)
  Once published (<https://mentalwhitenoise.github.io/>)
* Theme for my site (<https://github.com/pages-themes/slate>)
* My other site (needs work) (<http://n1nfmind.com/>)

## Quick start for local debug

cd C:\Git\MentalWhiteNoise\MentalWhiteNoise.github.io
bundle exec jekyll serve
<http://localhost:4000/>


[GitHub]:   https://github.com/
[Jekyll]:   http://jekyllrb.com/
[Markdown]: https://en.wikipedia.org/wiki/Markdown
[Markdown Cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[SourceTree]: https://www.sourcetreeapp.com/
[Slate]: https://pages-themes.github.io/slate/
[theme readme]: https://github.com/pages-themes/slate
[This Site GitHub]: https://github.com/MentalWhiteNoise/MentalWhiteNoise.github.io