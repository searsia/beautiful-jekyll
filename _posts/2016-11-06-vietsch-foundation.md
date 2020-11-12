---
layout: post
title: Vietsch Foundation funds Searsia
bigimg: /img/searsia-window.jpg
tags: [sponsors]
---

We are happy and proud to announce that the [Vietsch Foundation][1] will 
support the further development of Searsia. The Vietsch Foundation was 
founded by [Willem Karel Vietsch][2] (1952-2014) through his last will and 
testament: 

> Karel was very involved in the Internet community. He spent a large
> part of his life working in the area of research and education
> networking, which he help developing with his energy, creativity and
> thorough methodical approach. Sadly, his early death, put a stop to
> Karel's mission to support people and new developments, therefore he
> created the Vietsch Foundation, with the official objective of
> promoting "research into and development of advanced technology for
> scientific research and higher education", in the widest sense. 

Searsia is funded from the "Research and Higher Education Technology
Fund", a new thematic fund that is managed by the [NLnet Foundation][3].
The Vietsch Foundation will fund the Searsia work packages: 
*Recommendations* and *Advertisements*.

## Recommendations without tracking of users 

Searsia manages large collections of independent sources. Many advanced
features of search engines might be seen as sources too, such as query
autocompletion, related queries, and spelling correction, that is, these
features are provided by modules that receive the query, and return a
recommendation. Query autocompletion provides users with suggested
queries in a drop down box as they type their query.  Related queries
are given on the search page to direct users to alternative formulations
of their query, or to otherwise related information. Spelling correction
suggests corrected queries if the user types an incorrectly spelled
query, or an otherwise unusual query. Corrections are either used
directly or presented to the user as alternatives ("Did you mean: ...").

There are two main approaches to recommendations, often used in for
instance movie recommender systems: 
*1) collaborative filtering* provides recommendations based on actions 
from similar users (as in Amazon: "Customers who bought this item also 
bought..."); and 
*2) content-based filtering* provides recommendations based on the 
similarity between items. 
Autocompletions and related queries in search engines are almost
always based on queries from other users, i.e., they are essentially
collaborative filtering approaches. Besides the fact that it might be
undesirable to log the actions of the users, there are also other
drawbacks: First, there is a cold-start problem: How to implement
recommendations for a new system (when there are no user actions yet),
or for a system that does not have a lot of users? Second, user queries
might be stupid, racist, or otherwise objectionable: How to prevent
recommending those? (it is not hard to find examples on-line of search
engine autocomplete fails, as well as law suits about objectionable
recommendations).

We will implement and demonstrate open source solutions for recommended
queries that use content-based filtering, for instance based on a web
crawl, or directly based on the Searsia sample index (The Searsia server
indexes search results for each resource to learn what information each
resource provides). Our recommendations work without user tracking.


## Advertisements without tracking of users

Advertisements are the main source of income for many web sites and
search engines. To make Searsia an interesting solution for developers
of web search applications, we want to provide them the means to easily
and transparantly add advertisements as an independent source to
Searsia. The advertisements must be recognisable as advertisements, they
should not track the users of the search service, and it should be easy
to switch them off. Advertisements in search engines are much more
effective than advertisements on ordinary web sites, because users tell
the search engine exactly what they are currently looking for: The
user’s query is the ideal signal for an advertisement network. We
believe user tracking is not desirable and not needed for good
advertisements in search applications. Searsia technology should (also)
work without user tracking.

Searsia uses a broker (the Searsia server) that acts as an intermediary
between the sources and the user. We will implement advertisement such
that the user’s queries will not go directly to the advertisement
network. Instead, they are forwarded by the broker. So, the
advertisement network will not receive information that might identify
the user, such as IP numbers, cookies, and the browser’s user agent
string, which makes it virtually impossible to identify or track the user.

We will find at least one, and likely more advertisement partners that
share our vision, and that are willing to provide advertisements for
anonymous queries from Searsia search engines.

## More information

For more information, check out the information at the Vietsch Foundation
and NLnet.

* [Searsia at Vietsch Foundation][4]
* [Searsia at NLnet][5]

[1]: http://www.vietsch-foundation.org "Vietsch Foundation"
[2]: https://nl.wikipedia.org/wiki/Karel_Vietsch "Karel Vietsch"
[3]: https://nlnet.nl "NLNet Foundation"
[4]: http://www.vietsch-foundation.org/2017/01/30/searsia-project/ "Searsia at Vietsch Foundation"
[5]: https://nlnet.nl/project/searsia/ "Searsia at NLnet"
