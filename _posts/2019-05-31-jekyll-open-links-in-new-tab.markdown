---
layout: post
title:  "Jekyll Opening Links in New Tag"
date:   2019-05-31 19:51:00 +0100
last_modified_at: 2019-06-24 22:51:00 +0100
categories: jekyll
permalink: /jekyll-open-links-in-new-tab/
tags: [jekyll]
description: One of the first things I noticed after setting up this blog is that links to external sites open in the same window. 
---

One of the first things I noticed after setting up this blog is that links to external sites open in the same window. 
I'm by no means an expert in UX but I know I want to try my best keep people on this site. 
I also find it handy when researching as you can easily refer back to the page you were reading.

I am hosting this on GitHub and letting it build the site which means I am limited to the plugins I can use. 
I found [this](https://keith-mifsud.me/projects/jekyll-target-blank) plugin which does what I want but sadly it is not supported by GitHub. 

Time for some hacking. This is by no means a nice solution but the code below does the trick. 
It hooks onto all click events, checks if what has been clicked is inside an anchor tag then checks if the link on the anchor is external. 
If the link is external it is opened in a new window otherwise the link works as normal. 
Originally I had the code assume that the anchor was the target for the click event however the links at the bottom of this page are icons with spans next to them.
Checking that the target is inside an anchor using the `closest(tag)` method allows links on images/spans/icons.

External link checking is done by using the Jekyll `url` and `baseUrl` variable, if it begins with the `url + baseUrl` then it is internal otherwise it is external. 
This was tripped up when running locally as the URL is set to `localhost` however I was using `127.0.0.1` to access the site. 
This caused internal links to open in new tabs. This was fixed by adding another a check for `127.0.0.1` for internal links.

This blog is using the minima theme so to add this I copied the `head.html` file in the `_includes` folder and added a script tag with the below content.
The file can be found [here](https://github.com/jekyll/minima/blob/master/_includes/head.html).

{% raw %}
```javascript
const baseUrl = '{{ site.url + site.baseurl }}'.toLowerCase();
document.addEventListener('click', function (event) {
    let anchor = event.target.closest("A");
    if(anchor){
        const href = anchor.href.toLowerCase();
        if(!href.startsWith(baseUrl) && !href.startsWith('http://127.0.0.1')){
            window.open(href,'_blank');
            event.preventDefault()
        }
    }

}, false);
```
{% endraw %}