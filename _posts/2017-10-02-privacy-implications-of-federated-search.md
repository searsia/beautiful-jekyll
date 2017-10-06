---
layout: post
title: Privacy implications of federated search
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-water.jpg
share-img: http://searsia.org/blog/img/searsia-water.jpg
tags: [advertisements, privacy]
---

# Privacy implicatons of federated search

What does "federated" mean in federated search? 
Like the European Union is a _federation_ of independent countries, so is a
Searsia engine a _federation_ of independent search engines. When Searsia
receives a query, it does not perform a lot of searching itself: Searsia
forwards the query to a limited number of search engines in the federation 
that will do the actual searching. This has some interesting implications 
for the user's privacy.

An important implication is the following: Searsia does not forward any
identifying information to the engines in the federation. Like many web
applications, Searsia consists of a web [client][12] that runs in the user's
web browser and a [server][13] that runs on another system. Searsia forwards
its queries via the server. The Searsia server will not forward any
identifying information, such as [cookies][1] or the [user agent string][2]
to engines in the federation. Also, by forwarding the query, the engines
in the federation do not receive the user's [IP address][3]. So, engines
in the federation cannot track the queries of individual users, and
engines will be unable to return personalized results or targeted
advertisements.

However, there are several ways that private information can still
_leak_ to search engines in the federation. We address three types of
privacy leakage in this post: Leakage via images, via advertisements, 
and via clicks.

## Leakage via images

Search engines in the federation might return thumbnail images in their
search results. These images are not provided directly, but by means of
the URL of the image. When the Searsia client retrieves the image to
display it in the search results, it will send the privacy sensitive
information mentioned above (cookies, user-agent string, IP number)
to a third party site. The third party site can be the search engine
in the federation that provided the image URL, or any other other site 
for that matter.

Directly downloading images has another downsite: These images might
only be available over an insecure connection (HTTP instead of HTTPS), 
thereby creating a [mixed-content][4] page, where part of the page
is not secure. Although web browsers like Firefox will still display 
images in mixed-content pages, they also display a warning icon in the
address bar.

## Leakage via clicks

Whenever the user visits a web site, for instance by clicking on a search
result, the user will obviously share some identifying information with
that site. In some cases, this information might include the user's search
terms:
[Search leakage][9] is the _"transmission of a user's search terms to 
the site in the search results that the user chooses to visit"._
Leakage of the user's search terms may occur because of the 
[HTTP referrer][10] header. Browsers that run the Searsia client will 
send this referrer header — possibly including the query — to the site 
that the user wants to visit.

Leakage of the user's search terms might be the biggest threat to 
privacy in this list, because users share intimate details with search
engines. Users might search information about their health, about their 
sexual preferences, or about their financial situation. It is therefore
important to annonymize queries properly. 

## Leakage via advertisements

At Searsia we are investigating how to add [advertisements][5] to our
search results without leaking information. Most on-line advertisement
networks will instruct publishers that want to display advertisements 
to include Javascript in their page or they instruct publishers to load 
an external Javascript file (or both). Obviously in such cases, not 
only downloading the Javascript file leaks privacy information, but 
it additionally runs third-party code in the user's browser to 
further monitor the user's behaviour. For instance, advertising networks
use [web beacons][6] to check if the advertisement is viewable or 
[mouse Tracking][7] to check if they are hovered or clicked.

As an example of the requirements of advertisement networks, Yahoo's 
[Native ads for the web][8] shows the kind of code that has to be
included in a web site to allow Yahoo displaying advertisements. 
It also shows the use of a _viewability beacon_: A call to 
Yahoo to indicate that the advertisement is visible on the site.

## How Searsia prevents privacy leakage

Searsia version 1.0 prevents privacy leakage as follows: 

1. Leakage via images will be prevented by adding an option that lets the 
Searsia server also forward the images. This way, it serves as a proxy for 
images and additionally provides secure web connections if the 
Searsia server is served over HTTPS. 

2. Leakage via clicks is prevented by the a [Referrer Policy][11] meta 
header in Searsia's client. The client will use the default policy '`no-referrer`', 
so it will not share any referrer information. 
This can be changed to for instance `'origin'` to send only the first part
of the URL without the query string.

3. Leakage via advertisements, finally, cannot be prevented easily, unless
the advertisement networks allow the Searsia server to anonymize all 
the user interactions with the advertisements. This is ongoing work, and we
will spend a future blog posts on advertisements without privacy leakage.

 
[1]: https://en.wikipedia.org/wiki/HTTP_cookie "HTTP Cookie on Wikipedia"
[2]: https://en.wikipedia.org/wiki/User_agent#Use_in_HTTP "HTTP User-Agent on Wikipedia"
[3]: https://en.wikipedia.org/wiki/IP_address "IP address on Wikipedia"
[4]: https://support.mozilla.org/en-US/kb/mixed-content-blocking-firefox "Mixed content on Mozilla support"
[5]: /blog/2017-05-26-some-thoughts-on-search-advertising/ "Search advertising on Searsia"
[6]: https://en.wikipedia.org/wiki/Web_beacon "Web beacon on Wikipedia"
[7]: https://en.wikipedia.org/wiki/Mouse_tracking "Mouse tracking on Wikipedia"
[8]: https://developer.yahoo.com/flurry/docs/publisher/code/native-web-tags/ "Flurry native ad tags and testing" 
[9]: https://en.wiktionary.org/wiki/search_leakage "Search Leakage on Wikipedia"
[10]: https://en.wikipedia.org/wiki/HTTP_referer "HTTP referrer on Wikipedia"
[11]: https://www.w3.org/TR/referrer-policy/ "Referrer policy W3C standard"
[12]: https://github.com/searsia/searsiaclient "Searsia client"
[13]: https://github.com/searsia/searsiaserver "Searsia server"

