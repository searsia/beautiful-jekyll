---
layout: post
title: Web search; No tracking
bigimg: /img/searsia-poem.jpg
share-img: http://searsia.org/blog/img/searsia-poem.jpg
tags: [advertisements, autocompletions, privacy, release]
---

> This post is based on the Searsia lightning talk for the 2018 
> [New Year meeting of the Dutch Internet Society](https://newyear.isoc.nl/2018/),
> for which [the slides](http://searsia.org/deck.js/isoc2018.html) 
> were appropriately made in HTML.
>
> (top picture by [@bitsoffreedom@twitter.com](https://twitter.com/bitsoffreedom/status/951533529330012166))

The following poem, which according to the poet, [@lifning@cybre.space](https://cybre.space/@lifning/98835409973873638), 
has been "floating around the fediverse", perfectly describes what's wrong with the world wide web today: 

        
        roses are red
        violets are blue
        in surveillance capitalism
        a poem reads you

        and shows you ads
        for flower shops
        and tracks your clicks
        and never stops

        it cares not about
        if privacy's harmed
        the money is green
        when people are farmed

        twitter is cyan
        facebook is blue
        your friends are the product
        and so are you
        

## Surveillance capitalism

In [surveillance capitalism](https://en.wikipedia.org/wiki/Surveillance_capitalism), companies compete by 
collecting as much data as possible through surveillance. They sell that data, or they use the data to 
predict who is most likely to buy a product or service.

Why do companies use surveillance? They will (have to) explain this in their terms-of-service: 
You know, the lengthy disclaimer that you accepted without reading. Typically, the 
terms-of-service of companies like Google and Facebook claim that collecting user data is necessary for
at least two reasons: _1) to improve the service_ and _2) to show targeted advertisements_.

## 1. To improve the service

An example of a search service that is improved with user data is Google's query autocompletion service. 
Google stores the queries of all its users to predict what you search for. Autocompletions are an effective 
feature. They help users to formulate better queries, and they save users keystrokes: Very helpful if 
you are searching on your mobile phone. The image below shows autocompletions for the prefix "surveillance".

| ![Query autocompletions for 'surveillance'](http://searsia.org/deck.js/images/isoc2018service.png) |

## 2. To show targeted advertisements

The main reason for collecting user data is, of course, to show targeted advertisements.
Why are targeted advertisements so profitable? This vintage news paper advertisement for a pain killer is only 
effective to people that are in pain. In the old days, the only way to target such an advertisement, was
to choose a news paper that is read more by people in pain, and target pages in the news paper that are read
most by the same people, for instance the _health pages_. 
Today, Facebook and Google will be able to find the individuals among their users 
that are likely in pain, and show the advertisement only to them.
This makes targeted advertisements much more profitable

| ![Vintage pain killer advertisement (1908)](http://searsia.org/deck.js/images/isoc2018ad.jpg) |

Companies like Facebook and Google would like you to think that they _must_ collect data to improve services 
and show targeted advertisements. We work at Searsia to debunk this.


## Query autocompletions without tracking users

Let's have a closer look at query autocompletions. Using user data to predict query autocompletions 
causes several problems. For instance, Google actively 
[promoted nazi propaganda](https://www.theguardian.com/commentisfree/2016/dec/11/google-frames-shapes-and-distorts-how-we-see-world) 
for innocent queries like "did the h", and even worse, the first results for those queries would be pages from 
neo-nazi sites like Stormfront that deny that the holocaust happened.

| ![Google autocompletions suggesting 'did the holocaust happen'](http://searsia.org/deck.js/images/ia2017-autocompletion1.png) |

Many small organizations and individuals were damaged by autocompletions. There have been lawsuits in
[France](https://searchengineland.com/google-loses-french-lawsuit-over-google-suggest-32994),
[Italy](http://www.zdnet.com/article/google-loses-autocomplete-defamation-case-in-italy/),
[Germany](https://techcrunch.com/2012/09/07/germanys-former-first-lady-sues-google-for-defamation-over-autocomplete-suggestions/), and
[Japan](http://www.bbc.com/news/technology-17510651), 
where individuals could for instance not get a job because Google suggested offensive completions 
for their name. Google [started to actively filter](https://blog.google/products/search/google-search-autocomplete/) 
completions for person names after these lawsuits, but its autocompletions continue to suggested terms which could be viewed as 
[racist, sexist or homophobic](http://eprints.lancs.ac.uk/63268/).

At Searsia, we do not track user queries for autocompletions. Instead, we use the anchor texts of web pages, 
that is, the text of hyperlinks. We compared its performance with autocompletions based on user queries for a 
general web search task. Our approach that uses hyperlinks is 
[as effective as](/blog/2017-03-18-query-suggestions-without-tracking-users/)
 the approach that uses user data. 
The results below show that for short queries, we need 1 more keystroke to predict the full user query. 
For long queries, our approach outperforms the approach based on user data.

| ![Experiment: Autocompletions from web content vs. Autocompletions from user data](http://searsia.org/deck.js/images/ia2017-results2.png) |


## Targeted advertisements without tracking

Now, you might think: Sure, you can improve services without tracking people, but it is impossible to target 
advertisements without tracking people. Not quite. Remember Searsia is a search engine. Users tell a search 
engine what they are looking for. If you are looking for a car, Searsia can show you advertisements for cars. 
The advertisements are based on the search terms, not on the person.

Targeted advertisements by Searsia are based on the query, not on the person, so there is not need to track
individual users. Images and banners are provided via a local proxy, so the merchant or advertisement network
will not know the users' IP address unless they click on the advertisement. Advertisements do not use third 
party Javascript, third party cookies, or web beacons to prevent further 
[privacy leakage via advertisements](/blog/2017-10-02-privacy-implications-of-federated-search/).

| ![Advertisements for the query 'Amazon'](/blog/img/amazon-ads.png) |

The requirements for Javascript and cookies above do not allow Searsia to display ads from for instance 
Google's [DoubleClick](https://en.wikipedia.org/wiki/DoubleClick). However, they are perfect for displaying
advertisements from affiliate programs and networks. Searsia connects big affiliate programs APIS of for
instance [Amazon](https://affiliate-program.amazon.com/). It provides local search from datafeeds of 
affiliate networks like [ShareASale](https://www.shareasale.com). 
The image above shows example advertisements provided by [Dr. SheetMusic](httsp://drsheetmusic.com) for the
query [amazon](https://drsheetmusic.com/sheet-music/amazon), which provides advertisements for charities if 
there are no targeted affiliate results.


## Federated search

Searsia provides free open source software for federated search. Federated systems are the answer to global 
corporations like Twitter, Facebook and Google that profit from tracking their users. 
In a federated system, no-one owns the complete service, so no-one is able to profit from tracking all
user interactions. The poem that started this post was taken from [Mastodon](https://joinmastodon.org), a 
federated alternative for Twitter and Facebook. 
Just as Mastodon is a federated alternative for Twitter, Searsia's technology might one day be an 
alternative for Google. If that happens, we know that there is no reason to track users, not even for 
providing autocompletions or targeted advertisements.

## Acknowledgments

Many thanks to the [Vietsch Foundation](http://vietsch-foundation.org) and 
[NLnet Foundation](https://nlnet.nl) for funding our work on query 
recommendations and search advertising without tracking users.

