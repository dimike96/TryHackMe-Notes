# THM - Google Dorking

[TryHackMe | Google Dorking](https://tryhackme.com/room/googledorking)

> Michael Jack | 06/2022

--- 

## Task 1 - Ye Ol' Search Engine

> Google is arguably the most famous example of “Search Engines”, I mean who remembers Ask Jeeves? ~~*shudders*~~
> 
> Now it might be rather patronizing explaining how these “Search Engines” work, but there’s a lot more going on behind the scenes then what we see. More importantly, we can leverage this to our advantage to find all sorts of things that a word list wouldn’t. Researching as a whole - especially in the context of Cybersecurity encapsulates almost everything you do as a pentester.

"Search Engines" such as Google are huge indexers – specifically, indexers of content spread across the World Wide Web.

---

## Task 2 - Let's Learn About Crawlers

### What are Crawlers?

> These crawlers discover content through 
> various means. One being by pure discovery, where a URL is visited by 
> the crawler and information regarding the content type of the website is
>  returned to the search engine. In fact, there are lots of information 
> modern crawlers scrape – but we will discuss how this is used later. 
> Another method crawlers use to discover content is by following any and 
> all URLs found from previously crawled websites. Much like a virus in 
> the sense that it will want to traverse/spread to everything it can.

Crawlers go through webpages and attempt to get to every website to retrieve information such as keywords to aid in searches.

> Q: Name the key term of what a "crawler" is used to do.

```
Index
```

> Q: What is the name of the technique that "Search Engines" use to retrieve this information from websites?

```
Crawling
```

> Q: What is an example of the type of contents that could be gathered from a website?

```
Keywords
```

---

## Task 3 - Enter: Search Engine Optimization

> Search Engine Optimisation or SEO is a prevalent and lucrative topic in modern-day search engines.

There's a variety of factors that influence how search results are ranked, using something akin to a points scoring system. Here are a few of the influences:

> • How responsive your website is to the different browser types I.e. 
> Google Chrome, Firefox and Internet Explorer - this includes Mobile 
> phones!
> 
> • How easy it is to crawl your website (or if crawling is 
> even allowed ...but we'll come to this later) through the use of 
> "Sitemaps"
> 
> • What kind of keywords your website has (i.e. In our 
> examples if the user was to search for a query like “Colours” no domain 
> will be returned - as the search engine has not (yet) crawled a domain 
> that has any keywords to do with “Colours”

There are tools available online that help you analyze and see how a particular page might be ranked. Like [Measure page quality](https://web.dev/measure/) from Google.

There's also times where we would want to effectively do the opposite and prevent pages from being indexed and easily accessible from anyone. How can we do that?

---

## Task 4 - Beepboop - Robots.txt

> Aside from the search engines who provide these "Crawlers", website/web-server owners 
> themselves ultimately stipulate what content "Crawlers" can scrape. 
> Search engines will want to retrieve **everything** from a website - but there are a few cases where we wouldn't want **all** of the contents of our website to be indexed! Can you think of any...? How about a secret administrator login page? We don't want **everyone** to be able to find that directory - especially through a google search.

`Robots.txt` is the first thing indexed by crawlers when visiting a website. Similar to "Sitemaps" which will be covered later.

The file resides at the root directory specified by the webserve itself, and defines the permission the crawler has to the website. It can stipulate what type of crawler is allowed, and what files or directories are to be excluded from indexing by the crawler.

Example:

```
User-agent: *
Allow: /

Sitemap: https://mywebsite.com/sitemap.xml
```

For the above example, any crawler (any user-agent) can access the site, the entire directory is available to be indexed, and the sitemap is located at the specified url.

To exclude folders we can add lines like these:

```
Disallow: /secret-directory/
Disallow: /not-secret/super-secret/
```

This would remove "secret-directory" and it's contents/subdirectories from indexing, allow indexing of "not-secret" but not it's sebdirectory "super-secret".

We can use regex like (```/*.ext$```) where "ext" is some file extension, to disallow indexing of all files of some extension. We could use any such regex statement to dissallow subsets of files, or specify files to disallow directly.

We can use specific user agents to specify crawlers from Google (```Googlebot```), Microsoft MSN (```msnbot```), etc.

> Q: Where would "robots.txt" be located on the domain "ablog.com"?

```url
ablog.com/robots.txt
```

> Q: If a website was to have a sitemap, where would that be located?

```url
/sitemap.xml
```

> Q: How would we only allow "Bingbot" to index the website?

```
User-agent: Bingbot
```

> Q: How would we prevent a crawler from indexing the directory "/dont-index-me/"?

```
Disallow: /dont-index-me/
```

> Q: What is the extension of a Unix/Linux system configuration file that we might want to hide from "Crawlers"?

```
.conf
```

---

## Task 5 - Sitemaps

> “Sitemaps” are indicative resources that are helpful for crawlers, as 
> they specify the necessary routes to find content on the domain.

Sitemaps are valuable to crawlers and make them more favorable as it makes them easier to traverse and index.

> Q: What is the typical file structure of a sitemap?

```
xml
```

> What real life example can sitemaps be compared to?

```
map
```

> Name the keyword for the path taken for content on a website.

```
route
```

---

## Task 6 - What is Google Dorking?

Using advanced search methods such as logical operators and quotes, and keywords to refine a search to get desired results.

> Q: What would be the format used to query the site "bbc.co.uk" about flood defences?

```
site: bbc.co.uk flood defences
```

> Q: What term, would you use to search by file type?

```
filetype:
```

> Q: What term can we use to look for login pages?

```
intitle:Login
```

---
