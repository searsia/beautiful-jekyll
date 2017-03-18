---
layout: post
title: Query suggestions without tracking users
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-laptop.jpg
tags: [autocompletions]
---

Today, we launch [searsiasuggest][1], a simple but effective open source solution for query suggestions. It implements 3 kinds of query suggestions: 1) autocompletions, 2) spelling correction, and 3) related queries. The software works pretty much like many similar solutions: It inputs a list of queries with their popularity, it indexes those queries, and it ranks the queries given the user input. The query suggestions are demonstrated on [UT Search][2], an enterprise search engine for the University of Twente. Let's have a look at the three kinds of query suggestions implemented by [searsiasuggest][1]:

## Query autocompletions

Query autocompletions return popular queries by treating the user input as a prefix. For instance, when the user
inputs "computer s", the system returns popular completions of that prefix, such as "computer science", "computer systems" and "computer supported cooperative work".

| ![Query autocompletions for 'computer s'][3] |

## Spell-corrected queries

Spelling correction will suggest alternative spellings for user queries. If for instance the user ignores the suggestions from autocompletions and enters "computer sience" instead (without the "c" in "science") then the spelling correction kicks in, returning "computer science" as its suggested query.  UT search displays the following:

| ![Spelling correction for 'computer sience'][4] |

## Related queries

Suppose the user now selects the corrected query "computer science", then the search engine might show related queries, such as "Electrical Engineering Mathematics and Computer Science" and "science and technology" as follows. No rocket science either, you have probably seen this before in web search. UT search shows:

| ![Related queries for 'computer science'][5] |


## How to obtain popular query suggestions?

To use [searsiasuggest][1], you need a list of popular query suggestions. How to obtain those suggestions? In practice, search engines often use queries from previous users, i.e. query logs, to return query suggestions. Query logs are very effective in predicting query autocompletions and related queries. If you have a query log for your search engine, then you can effectively use them in [searsiasuggest][1]. 

However, there are many downsides to using query logs. We talked about some of these in last month's blog post [Query autocompletions considered harmful][6]: Query suggestions that use query logs may return offensive and damaging results, and they suffer from a destructive feedback loop, where bad suggestions are mutually reinforced by the search engine and its users. Other downsides might be of a more principled nature: Maybe your organisation's privacy policies do not allow you to log user input and user interactions; or maybe [We don't track you][7] is your organization's motto and main strategy to distinguish your product from its competitors.

## Popular queries without logging any queries?

Inspired by research of [Sumit Bhatia, Debapriyo Majumdar, and Prasenjit Mitra][8], [Reiner Kraft and Jason Zien][9], and [Van Dang and Bruce Croft][10], we decided to obtain our query suggestions from the anchor text of web pages, i.e., the text that you click on in hyperlinks. We collected more than 1 million web pages for the domain `utwente.nl` and extracted about 200,000 unique query suggestions from the anchor text of those web pages. UT Search receives currently about 1000 queries per day on average (including repeats), so collecting that many unique queries from user logs will likely take several years. We described the prodedure in: [Collecting Data for Query Suggestions: a poor person's approach][11].

## The quality of query suggestions from anchors

Are query suggestions from anchor text any good compared to query suggestions from query logs? To check this, we used the query log of [Greg Pass, Abdur Chowdhury, and Cayley Torgeson][12], which contains 20 million queries submitted by about 650,000 users to the AOL search engine between March and May in 2006. Following the recent query autocompletion experiments by [Fei Cai, Shangsong Liang, and Maarten de Rijke][13], we used queries submitted before 8 May 2006 as train queries and queries submitted afterwards as test queries. We removed queries containing URL substrings (`http:`, `https:`, `www.`, `.com`, `.net`, `.org`, and `.edu`) from both training and test queries. We did not further filter the data ([Fei Cai et al.][13] only kept queries appearing in both partitions). Because we are not interested in personalisation, we put 99% of the users in the training data, and the remaining 1% of the users in the test data. This leaves more than 3.3 million unique training queries for [searsiasuggest][1] and 952 queries for testing the system. For every test query, we used 10 different prefixes as input to [searsiasuggest][1]: 1 to 5 characters, and 1 to 5 words. If the query has less than 5 characters or less than 5 words, we take the full query as input. For each prefix we measured the mean reciprocal rank of the position for which [searsiasuggest][1] returns the full test query. The mean reciprocal rank is calculated as one divided by the position of the correct results, so it will be 1 if the correct result is returned first, 0.5 if it is returned second, etc. We also measured the average number of results returned for each prefix. The results are presented in Table 1.

*Table 1, Quality of query autocompletions using query logs*

Prefix |  MRR  | Returned
:----- |:-----:| --------: 
1 char | 0.026 |  10.00
2 char | 0.072 |  10.00
3 char | 0.135 |   9.99
4 char | 0.181 |   9.71
5 char | 0.227 |   9.28
1 word | 0.271 |   8.15
2 word | 0.354 |   4.40
3 word | 0.365 |   3.30
4 word | 0.365 |   3.06
5 word | 0.366 |   3.04

Table 1 shows that after typing 3 characters the MRR is 0.135, so the correct suggestion is on average available in the top 7 results (1/8 = 0.125). After typing 1 word, the MRR is 0.271, i.e., on average the correct suggestion is available in the top 4 results.

For anchor text completions we ideally would need a large web crawl from 2006 (the year of the query log). In absence of such a crawl, we used data from [ClueWeb09][14], a web crawl of more than 1 billion pages crawled in January and February 2009 by researchers at Carnegie Mellon University. [Anchor texts][15] for the English pages in this collection (about 0.5 billion pages) are readily available, so we do not actually need to process the ClueWeb09 web pages themselves. Anchor texts with the separators  (`.`, `?`,`!`, `|`, `-` or `;`) followed by a space were split in multiple strings. Text in braces `()`, `{}`, `[]` was removed from the strings. We processed the anchor texts by retaining only suggestions that occur at least 15 times. This resulted in 46 million unique suggestions. Performance of the ClueWeb09 anchor text suggestions is presented in Table 2.

*Table 2, Quality of query autocompletions using anchor texts*

Prefix |  MRR  | Returned
:----- |:-----:| --------: 
1 char | 0.006 |  10.00
2 char | 0.025 |  10.00
3 char | 0.066 |  10.00
4 char | 0.123 |   9.92
5 char | 0.180 |   9.71
1 word | 0.251 |   8.62
2 word | 0.415 |   5.42
3 word | 0.440 |   3.95
4 word | 0.443 |   3.67
5 word | 0.443 |   3.64

The results show that for queries of 2 words or more (the average query length in the test data is 2.6), anchor text autocompletions perform better than query log autocompletions, up till an MRR of 0.443 (0.366 for query logs). Query log autocompletions perform better for shorter queries: Anchor text autocompletions need about one character more than query log autocompletions for the first 5 characters.

## Conclusion

Query autocompletions based on anchor text from web pages perform remarkably well. For queries of more than 1 word, they outperform autocompletions that are based on over two months of query log data. Simply extracting all anchor texts is really only a first attempt to get well-performing autocompletions from web content. Ideas to improve suggestions are: Using linguistic knowledge to get suggestions from all web page text (for instance using the [Stanford CoreNLP tools][16]), using web knowledge like [PageRank scores][17] and [Spam scores][18] to improve the quality of suggestions, and reranking of suggestions by their "query-ness" using machine learning. But for now, please enjoy the query suggestions from [searsiasuggest][1].

## Acknowledgments

We are grateful to the [Vietsch Foundation][19] for funding our work on query suggestions.



[1]: https://github.com/searsia/searsiasuggest "Searsia Suggest"
[2]: https://search.utwente.nl "UT Search"
[3]: /blog/img/ut-autocompletions.jpg "Autcompletions for 'computer s'"
[4]: /blog/img/ut-spelling.jpg "Spelling correction for 'computer sience'"
[5]: /blog/img/ut-related.jpg "Related queries for 'computer science'"
[6]: /blog/2017-02-09-autocomplete/ "Query autocompletions considered harmful"
[7]: https://duckduckgo.com/about "About DuckDuckGo"
[8]: http://sumitbhatia.net/papers/sigir11.pdf "SIGIR 2011"
[9]: http://www.wsdm-conference.org/2010/proceedings/docs/p41.pdf "WSDM 2010"
[10]: http://wwwconference.org/proceedings/www2004/docs/1p666.pdf "WWW 2004"
[11]: https://github.com/searsia/searsiasuggest/tree/master/src/main/perl "Collecting Data for Query Suggestions"
[12]: http://people.cs.georgetown.edu/~abdur/publications/pos-infoscale.pdf
[13]: https://staff.fnwi.uva.nl/m.derijke/wp-content/papercite-data/pdf/cai-prefix-adaptive-2016.pdf 
[14]: http://lemurproject.org/clueweb09/ "ClueWeb09"
[15]: http://academictorrents.com/details/bb36fce78df3609627ec3495ca4fa37c28fcee18 "Anchor text derived from ClueWeb09"
[16]: http://stanfordnlp.github.io/CoreNLP/ "Stanford CoreNLP – a suite of core NLP tools"
[17]: http://www.lemurproject.org/clueweb09/pageRank.php "ClueWeb09 PageRank scores"
[18]: http://durum0.uwaterloo.ca/clueweb09spam/ "Waterloo Spam Rankings for ClueWeb09"
[19]: /blog/2016-11-06-vietsch-foundation/ "Vietsch Foundation funds Searsia"
