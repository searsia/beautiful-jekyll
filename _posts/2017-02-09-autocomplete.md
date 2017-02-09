
---
layout: post
title: Query autocompletions considered harmful
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-autocomplete.jpg
tags: [autocompletions]
---

Search engines suggest completions of partially typed queries to help users speed up their searches, for instance by showing the suggested completions in a drop down box. These _query autocompletions_ enable the user to search faster, searching for long queries with relatively few key strokes. [Jakobsson (1986)][1] showed that for a library information system, users are able to identify items using as little as 4.3 characters on average. Query autocompletions are now widely used, either with a drop down box or as instant results ([Bast and Weber 2006][2]). While [Jakobsson (1986)][1] used the titles of documents as completions of user queries, web search engines today generally use large logs of queries submitted previously by their users. Using previous queries seems a common-sense choice: The best way to predict a query? Use previous queries! Several scientific studies use the AOL query log provided by [Pass et al. (2006)][20] to show that query autocompletion algorithms using query logs are effective ([Bar-Yossef and Kraus 2011][3]; [Shokouhi  and Radinsky 2012][4]; [Whiting and Jose 2014][5]; [Mitra and Craswell (2015)][17]; [Cai et al. 2016][15]). However, query autocompletion algorithms that are based on query logs are problematic in two important ways: 1) They return offensive and damaging results; 2) They suffer from a destructive feedback loop. Let's discuss these two problems in the following sections. 

## Offensive queries

Query autocompletion based on actual user queries may return offensive results. In 2010, a French appeals court ordered Google to remove the word arnaque, which translates roughly as "scam", from appearing in Google's autocompletions for CNFDI, the Centre National Privé de Formation a Distance ([McGee 2010][6]) Google's defense argued that its tool is based on an algorithm applied to actual search queries: It was users that searched for "cnfdi arnaque" that caused the algorithm to select offensive suggestions. The court however ruled that Google is responsible for the suggestions that it generates. Google lost a similar lawsuit in Italy, where queries for an unnamed plaintiff's name were presented with autocomplete suggestions including truffatore ("con man") and truffa ("fraud") ([Meyer 2011][7]). Google argued that it should not be held liable for terms that appear in autocomplete as these are predicted by computer algorithms based on searches from previous users, but the court viewed the autocomplete suggestions as being produced by Google itself. In another similar law suite, German's former first lady Bettina Wulff" sued Google for defamation when queries for her name completed with terms like "escort" and "prostitute" ([Lardinois 2012][8]). In yet another lawsuit in Japan, Google was ordered to disable autocomplete results for an unidentified man who could not find a job because a search for his name linked him with crimes he was not involved with ([BBC 2012][9]). Google has since updated its autocompletion results by filtering offensive completions for person names, no matter who the person is ([Yehoshua 2016][10]). But controversies over query autocompletions remain. A study by [Baker and Potts (2013)][13] highlights that autocompletions produce suggested terms which can be viewed as racist, sexist or homophobic. Baker and Pots analyzed the results of over 2,500 query prefixes and showed that completion algorithms inadvertently help to perpetuate negative stereotypes of certain identity groups. There is increasing evidence that  autocompletions play an important role in spreading fake news and propaganda. Query suggestions actively direct users to fake content on the web, even when they are not looking for it ([Roberts 2016][10]). Examples include bizarre completions for -- again -- person names, like "Michelle Obama is a man", but also completions like "Did the holocaust happen", which if selected, returns as its top result a link to the neo-Nazi site stormfront.org ([Cadwalladr 2016][12]). 

The examples show that query autocompletions can be harmful when they are based on searches by previous users. Harmful completions are suggested when ordinary users seek to expose or confirm rumors and conspiracy theories. Furthermore, there are indications that harmful query suggestions increasingly result from  computational propaganda, i.e., organizations use bots to game search engines and social networks ([Shorey and Howard 2016])[14].


## A destructive feedback loop

Morally unacceptable query completions are not only introduced by the searches of previous users, they are also mutually reinforced by the search engine and its users. When a query autocompletion algorithm suggests morally unacceptable queries, users are likely to select those, even if the users are only confused or stunned by the suggestion. But how does the search engine ever learn it was wrong? It might not ever. As soon as the system determined that some queries are recommended; they are more often selected by users, which in turn makes them end up in the training data that the search engine uses to train it's future query autocompletion algorithms. Such a destructive feedback loop is one of the features of a Weapon of Math Destruction, a term coined by [O'Neil (2016)][15] to define harmful statistical models. O'Neil sums up three elements of a Weapon of Math Destruction: Damage, Opacity, and Scale. Indeed, the _damage_ caused by query autocompletion algorithms is extensively discussed in the previous section. Query autocompletion algorithms are _opaque_ since they are based on the proprietary, previous searches known only by the search engine. If run by a search engine that has a big market share, the query completion algorithm also _scales_ to a large number of users. Query autocompletions of a search engine with a majority market share in a country might substantially alter the opinion of the country's citizens, for instance, a substantial number of people will start to doubt whether the holocaust really happened.


## Fixing morally unacceptable results using content-based autocompletions

It is instructive to view a query autocompletion algorithm as a recommender system, that is, the search engine recommends queries based on some input. Recommender systems are usually classified into two categories based on how recommendations are made ([Adomavicius and Tuzhilin 2005][22]): 1) Collaborative recommendations, and 2) Content-based recommendations. Collaborative query autocompletions are based on similarities between users: "People that typed this prefix often searched for: ...". Content-based query autocompletions are based on similarities with the content: "Web pages that contain this prefix are often about: ...". Until now, we only discussed collaborative query autocompletion algorithms. What would a content-based query autocompletion algorithm look like? [Bhatia et al. (2011)][19] proposed a system that generates autocompletions by using all N-grams of order 1, 2 and 3 (that is single words, word pairs, and word triples) from the documents. They tested their content-based autocompletions on newspaper data and on data from ubuntuforums.org. Instead of N-gram models from all text, [Kraft and Zien (2004)][21] built models for query reformulation solely from the anchor text, the clickable text from hyperlinks in web pages. Interestingly, [Dang and Croft (2010)][20] argue that anchor text can be an effective substitute for query logs. They studied the use of anchor texts for a range of query reformulation techniques, including query-based stemming and query reformulation, treating the anchor text as if it were a query log.

At Searsia, we develop open source tools that allow search engine developers to easily develop content-based autocompletions, so autocompletions without the need to track users. A first demo of content-based autocompletions using anchor texts now runs on: [U. Twente Search][24]. In the coming weeks, we will evaluate our content-based recommendations for U. Twente search, and we will investigate whether content-based autocompletions can replace collaborative autocompletions on web scale. The first results look promising: We believe content-based recommendations can provide high quality query autocompletions, and fix some of the harmful effects of today's query autocompletion algorithms.


## References

* M. Jakobsson (1986) [Autocompletion in full text transaction entry: a method for humanized input][1]. In: _Proceedings of the ACM SIGCHI Conference on Human Factors in Computing Systems_.
* H. Bast and I. Weber (2006) [Type less, find more: fast autocompletion search with a succinct index][2], In: _Proceedings of the ACM SIGIR Conference on Research and Advanced Technology for Information Retrieval_. 
* Z. Bar-Yossef and N. Kraus (2011) [Context-sensitive query auto-completion][3]. In: _Proceedings of the World Wide Web Conference (WWW)_, 107–116
* M. Shokouhi and K. Radinsky (2012) [Time-sensitive query auto-completion][4]. In: _Proceedings of the ACM SIGIR Conference on Research and Advanced Technology for Information Retrieval_, pages 601–610
* S. Whiting and J.M. Jose (2014) [Recent and robust query auto-completion][5]. In: _Proceedings of the World Wide Web Conference (WWW)_, 971–982
* M. McGee (2010) [Google Loses French Lawsuit Over Google Suggest][6]. _Search Engine Land 6 January 2010_.
* D. Meyer (2011) [Google loses autocomplete defamation case in Italy][7]. _ZDNet 5 April 2011_.
* F. Lardinois (2012) [Germany's Former First Lady Sues Google For Defamation Over Autocomplete Suggestions][8], _TechCrunch_, 7 September 2012.
* BBC (2012) [Google ordered to change autocomplete function in Japan][9]. _BBC 26 March 2012_.
* T. Yehoshua (2016) [Google Search Autocomplete][10]. _Google Blog 10 June 2016_.
* H. Roberts (2016) [How Google's 'autocomplete' search results spread fake news around the web][11]. _Business Insider 5 December 2016_.
* C. Cadwalladr (2016) [Google is not 'just' a platform. It frames, shapes and distorts how we see the world][12]. _The Guardian 11 December 2016_.
* P. Baker and A. Potts (2013). [Why do White people have thin lips? Google and the perpetuation of stereotypes via auto-complete search forms][13]. _Critical Discourse Studies 10_(2), 187–204.
* S. Shorey and P.N. Howard (2016) [Automation, Big Data, and Politics: A Research Review][14]. _International Journal of Communication 10_(2016), 5032–5055 
* C. O'Neil (2016) [Weapons of math destruction: how big data increases inequality and threatens democracy][15]. _Crown_.
* F. Cai, S. Liang, and M. de Rijke (2016) [Prefix-adaptive and time-sensitive personalized query auto completion][16]. _IEEE Transaction on Knowledge and Data Engineering_
* B. Mitra and N. Craswell (2015) [Query Auto-Completion for Rare Prefixes][17]. In: _Proceedings of the 24th ACM International on Conference on Information and Knowledge Management (CIKM), 1755-1758 
* G. Di Santo,  R. McCreadie, C. Macdonald, and I Ounis (2015) [Comparing Approaches for Query Autocompletion][18]. In: _Proceedings of the 38th International ACM SIGIR Conference on Research and Development in Information Retrieval_, 775-778 
* S. Bhatia, D. Majumdar, and P. Mitra (2011) [Query suggestions in the absence of query logs][19]. In: _Proceedings of the 34th international ACM SIGIR conference on Research and development in Information Retrieval_, 795-804
* V. Dang, and W.B. Croft (2010) [Query reformulation using anchor text][20]. In: _Proceedings of the third ACM international conference on Web search and data mining_
* R. Kraft and J. Zien (2004) [Mining anchor text for query refinement][21]. In: _Proceedings of the 13th International World Wide Web Conference_, 666–674.
* G. Adomavicius and A. Tuzhilin (2005) [Toward the next generation of recommender systems: a survey of the state-of-the-art and possible extensions][22], _IEEE Transaction on Knowledge and Data Engineering 17_(6),  734-749
* A. Zhang, A. Goyal, W. Kong, H. Deng, A. Dong, Y. Chang, C.A. Gunter, and J. Han (2015) [Adaptive query auto-completion via implicit negative feedback][23]. In: _Proceedings of the 38th International ACM SIGIR Conference on Research and Development in Information Retrieval_, 143–152

[1]: https://doi.org/10.1145/22339.22391 "SIGCHI 1986" 
[2]: https://doi.org/10.1145/1148170.1148234 "SIGIR 2006"
[3]: http://wwwconference.org/proceedings/www2011/proceedings/p107.pdf "WWW 2011"
[4]: https://doi.org/10.1145/2348283.2348364 "SIGIR 2012"
[5]: http://wwwconference.org/proceedings/www2014/proceedings/p971.pdf "WWW 2014"
[6]: http://searchengineland.com/google-loses-french-lawsuit-over-google-suggest-32994 "Search Engine Land 2010"
[7]: http://www.zdnet.com/article/google-loses-autocomplete-defamation-case-in-italy/ "ZDNet 2011"
[8]: https://techcrunch.com/2012/09/07/germanys-former-first-lady-sues-google-for-defamation-over-autocomplete-suggestions/ "TechCrunch 2012"
[9]: http://www.bbc.com/news/technology-17510651 "BBC 2012"
[10]: https://blog.google/products/search/google-search-autocomplete/ "Google Blog 2016"
[11]: https://www.businessinsider.com/autocomplete-feature-influenced-by-fake-news-stories-misleads-users-2016-12 "Business Insider 2016"
[12]: https://www.theguardian.com/commentisfree/2016/dec/11/google-frames-shapes-and-distorts-how-we-see-world "The Guardian 2016"
[13]: http://doi.org/10.1080/17405904.2012.744320 "Critical Discourse Studies 10"
[14]: http://ijoc.org/index.php/ijoc/article/view/6233/1812 "International Journal of Communication 10(2016)"
[15]: https://weaponsofmathdestructionbook.com "Crown 2016"
[16]: https://doi.org/10.1109/TKDE.2016.2568179 "IEEE Transactions on Knowledge and Data Engineering 2016"
[17]: https://doi.org/10.1145/2806416.2806599 "CIKM 2015"
[18]: https://doi.org/10.1145/2766462.2767829 "SIGIR 2015"
[19]: http://sumitbhatia.net/papers/sigir11.pdf "SIGIR 2011"
[20]: http://www.wsdm-conference.org/2010/proceedings/docs/p41.pdf "WSDM 2010"
[21]: http://wwwconference.org/proceedings/www2004/docs/1p666.pdf "WWW 2004"
[22]: http://ids.csom.umn.edu/faculty/gedas/papers/recommender-systems-survey-2005.pdf "IEEE Transactions on Knowledge and Data Engineering 17(6)"
[23]: http://yichang-cs.com/yahoo/SIGIR15_aQAC.pdf "SIGIR 2015"
[24]: https://search.utwente.nl "U. Twente Search"




