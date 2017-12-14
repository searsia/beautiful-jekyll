---
layout: post
title: Searsia Version 1.0 released
bigimg: /img/searsia-github.jpg
share-img: http://searsia.org/blog/img/searsia-github.jpg
tags: [release]
---

Earlier this week we released Searsia Version 1.0, a major update of
our software that will make it a lot easier to configure your
federated search engine. The changes implemented in Searsia Version 1.0
were inspired by the need to support recommendations and advertisements 
without tracking the users of search engines.

### Release notes

The most important changes with the previous version, Version 0.4, are:

* A server can now be configured using simple JSON files, either locally or remotely on -- for instance -- Github; This breaks compatibility with earlier versions of Searsia;
* API templates now follow the [OpenSearch URL template syntax](http://www.opensearch.org/Specifications/OpenSearch/1.1#OpenSearch_URL_template_syntax); Old templates are still supported, but give a "deprecated" warning;
* Resources can be easily removed again from the federation;
* Engines can be tested by Searsia Server, outputting JSON or intermediate XML results for debugging purposes. There is also an option to test each resource in the federation;
* The server provides health statistics for each resource with the following information: time when the resource was started, time of last update, time of last successful query, time of last error, number of successful queries, number of errors, and the last error message;
* Results are provided from the server cache if a resource is used twice with the same query in a short period of time;
* The server's resource selection ranking now supports paging (not yet supported by the client);
* There is an option to sign API requests with a private key (with one implementation: Amazon's affiliate program API);
* Both the server and the client support linear search/reranking of search results. The client's in browser search is used for [Searsia Site Search](http://searsia.org/search.html) and by [NLNet search](https://nlnet.nl/search/); The server's linear search is used by for instance [ShareASale's affiliate program](http://searsia.org/blog/2017-11-30-ethical-search-advertising/#affiliate-networks-shareasale);
* The client supports query autocompletions, as well as advertisements in a separate column;
* The client provides improved privacy by instructing the browser not to leak the query string in the HTTP referrer header, and by an option for proxying of search result images;
* The server supports more API's and types of search engines, including results from various affiliate advertising programs;

Please read information on how to get started with Searsia on [Searsia's Start](http://searsia.org/start.html) page. 
We hope Searsia Version 1.0 will make it a lot easier for developers to run their own federated search engine.

### Acknowledgments

We thank the [Vietsch Foundation](http://vietsch-foundation.org/) and [NLnet Foundation](https://nlnet.nl/) for funding our work on 
recommendations and advertisements without tracking of users.


