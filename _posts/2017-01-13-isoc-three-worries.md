---
layout: post
title: Three worries about web search engines
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-slide.jpg
tags: [isoc]
---

> This post contains the text of the lightning talk presented at the 
> New Year Event of the Dutch Internet Society (ISOC) on 12 January 2017. 
> Of course, the [slides for the Internet Society meeting][1] were 
> appropriately made in HTML.

Web search is _the_ single most important application of the web. Without search, the web would be virtually useless. I love Google (and Yahoo, and Bing), but there are some things that worry me about search engines. Let's discuss three of those worries: 


## 1. The Search Engine Manipulation Effect

Search engines influence people. In 2014, [Robert Epstein and Ronald Robertson][2] of the American Institute for Behavioral Research and Technology in the US conducted the following experiment: They asked people what candidate they would support in the Australian election, Tony Abbott or Julia Gillard? Then they let them search information about the candidates. However, the researchers did not tell the people that they manipulated the search results. People used a search engine for which  higher-ranked search results linked to Web pages that describe one candidate as the better than the other. Their paper shows the results of two search engines: one that is biased to Gillard and one that is biased to Abbot. In all cases, people changed their minds towards the biased search engine's results much and much more often than you would expect if people change their minds at random. The study shows that people have a great trust in search engines. If results are willingly manipulated, search engines could easily swing an election. The researchers call this the _Search Engine Manipulation Effect_. 

## 2. Privacy

The second thing that worries me: Search engines receive information from us that is really, really private. We search things about our health, about our sexual preferences, about our financial situation. Most search engines log our queries, and they hold on to that information, indefinitely. They also log our clicks. And they use this information to target us with advertisements.

Sadly, the most vulnerable people in our society, people with bad health or with bad credit scores, are in practice targeted the most. It is worth reading Cathy O'Neil's analogy between optimizing advertisement returns and the "itinerant quack" in an old western ([O'Neil 2016][3]):

> Vulnerability is worth gold. It always has been. Picture an itinerant
> quack in an old western movie. He pulls into town with his wagon full
> of jangling jars and bottles. When he sits down with an elderly
> prospective customer, he seeks out her weaknesses. She covers her
> mouth when she smiles, indicating that she's sensitive about her bad
> teeth. She anxiously twirls her old wedding ring, which from the
> looks of her swollen knuckle will be stuck there till the end of her
> days. Arthritis. So when he pitches his products to her, he focuses
> on the ugliness of her teeth and her aching hands. He can promise to
> restore the beauty of her smile and wash away the pain from her
> joints. With this knowledge, he knows he's halfway to a sale before
> even clearing his throat to speak.


## 3. Crawling, crawling, crawling...

The third thing that worries me: Search engines need a lot of resources. They constantly crawl the web, downloading pages to check if things changed. My [personal blog][4] at the university is downloaded more by web robots that crawl the site, than by people that read my blog posts... You might think: Write better blog posts, Djoerd, and you are right. But, even so, constantly downloading my blog to detect changes is crazy. My blog has its own search field, which instantly shows updates when something changes. If only, somehow, we can redirect queries from search engines, that show an interest in the things I blog about, directly to my blog's search field?

## Federated Search

Searsia's approach to search can ease some of these worries. Searsia is a _federated_ search engine. A Searsia search engine is a federation of search engines, like the European Union (EU) is a federation of countries. Within the EU, each countries has its own government and its own laws. Within Searsia, each search engine indexes whatever it likes and returns whatever it likes. 

Sites like Wikipedia, Amazon, Stack Overflow and YouTube provide their own search interface. Obviously, they do not need to crawl their site, because they own the data. They instantly know when something changed. Searsia comes with a configuration mechanism that makes it easy to add search engines to the federation.
When a Searsia engine receives a query, it forwards the query to a selection of the search engines in the federation. It will try to select those search engines that most likely satisfy the user's need, for instance forwarding a query to YouTube, if it believes the user would like a video. This way, Searsia displays live results from YouTube, instead of results that were crawled a while ago.

Each Searsia engine is a search engine too, pretty much like any other search engine, so we might make a federation of those search engines again.

## Conclusion

Let's go back to our three worries: Manipulation, Privacy, and Costs of crawling. What do you gain by installing Searsia? First, Searsia delegates queries to multiple search engines that it does not control. Even if one or two of those manipulate or censor their results, there will be other engines in the federation that show more objective results. Second, all queries go via Searsia, so engines in the federation can no longer track individual users. Of course, now Searsia will get all your queries, but no worries, anyone can run a Searsia server. Third, Searsia does not crawl the web, ever. It will learn over time from each engine in the federation what its contents are. This makes it cheap to set up a Searsia engine, and easy to maintain. You can run Searsia on a cheap server in your own network.

## Acknowledgments

We are grateful to the Vietsch Foundation for supporting our work. We also thank NLNet and the University of Twente.

## Epilogue

At the ISOC meeting, someone in the audience asked me the following: 

> Does Searsia show the advertisements of a search engine? 
> If not then search engines will likely object to being part of 
> a Searsia federation.

Searsia will generally be configured to access the official APIs of search engines from Google, Twitter, etc., and it will show whatever the engine's official API returns. For our current demonstration deployment, [U. Twente Search][5], we have not seen any of the APIs returning advertisements. However, Searsia's configuration options are quite general; they include options for scraping web results, and for selecting (and ignoring) returned elements, including advertisements.

So, yes, Searsia can be configured such that it ignores advertisements from engines.
The Searsia client explicitly shows what engine in the federation produced the results. This way, Searsia transparently creates traffic for search engines and for the sites they search. Searsia announces itself by a custom [User-Agent string][6]. If sites object to being part of Searsia, they can be removed from the federation.


[1]: http://searsia.org/deck.js/isoc2017.html "Searsia: Search federated. Presented at the ISOC New Year 2017."
[2]: http://dx.doi.org/10.1073/pnas.1419828112 "Robert Epstein and Ronald Robertson. The search engine manipulation effect (SEME) and its possible impact on the outcomes of elections. Proceedings of the National Academy of Sciences of the USA 112(33), 2014."
[3]: https://weaponsofmathdestructionbook.com "Cathy O'Neil. Weapons of Math Destruction: How big data increases inequality and threatens democracy. _Crown, New York_, 2016."
[4]: http://www.cs.utwente.nl/~hiemstra/ "Djoerd Hiemstra's home page: A bit of teaching, some research, shake well..."
[5]: https://search.utwente.nl "University of Twente Search"
[6]: https://en.wikipedia.org/wiki/User_agent#Use_in_HTTP "Wikipedia: User Agent, Use in HTTP"
