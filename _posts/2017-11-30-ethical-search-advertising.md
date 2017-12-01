---
layout: post
title: Search advertising without tracking users
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-underwater.jpg
share-img: http://searsia.org/blog/img/searsia-underwater.jpg
tags: [advertisements, privacy]
---

The past months Searsia investigated ways for small search engines to provide search advertisements without
participating in the large advertisement networks of Google and Facebook, and more importantly, without
the need for small search engines to track their users. Large advertisement networks operate by [pay-per-impression][1]
or [pay-per-click][2] schemes that need third-party [tracking bugs][3] and third-party [cookies][4] to track 
users, even if they are not actively engaging with the advertisements. Large advertisement networks try to
track their user also outside their own web sites by running code on other sites, such as like buttons 
(Facebook) and analytics code (Google). Tracking users is needed to provide targeted advertisements, but 
it is also needed to combat [click fraud][5].

_Our solution provides sites that run their own search engine the means to include advertisements without the need to track their users with third-party trackers._


## Affiliate programs as ethical advertising

In our previous blog post, we argued that [affiliate marketing][6] can serve as an alternative to
tracking-based advertisements. 

> Affiliate marketing is a type of on-line marketing where an affiliate (also called the publisher) 
> is paid a commission for each sale that is closed based on a link or advertisement on the affiliate's 
> web site. Running an affiliate program is often as easy as putting a hyperlink to a merchant's 
> product on your site that contains your affiliate identifier. 

Because we run our affiliate advertisements in a search engine, we will still show _targeted_ 
advertisements. If the user types "car", we show a car advertisement. The ad is based on the keyword, 
not on the person, so it does not involve tracking.


## Affiliate programs in Searsia: example implementations

In what follows, we show the configuration files for 5 search advertisement programs. The
examples use: 
_1)_ affiliate programs of multinational corporations like Amazon, 
_2)_ affiliate networks like ShareASale, and 
_3)_ any other information that we would like to advertise.
Our configuration files are based on [Searsia Server version 1.0][7], which is not released yet,
but already available on Github. The affiliate programs described here are demonstrated by
[Dr. Sheet Music][8], a federated search engine for sheet music.

### Affiliate programs: Amazon and eBay

Many large sites run their own affiliate programs. Let's have a look at two of the biggest players
in affiliate land: Amazon and eBay.

**Amazon Affiliate Program**

[Amazon's affiliate program][9] can be joined for free. 
Publishers earn up to 10% advertising fees with Amazon and its trusted merchants. Like many of 
the bigger affiliate programs, Amazon provides an Product Advertising API that can be found under
"Tools" once you are logged in. The API can be configured as a Searsia engine with the following
configuration file (which runs on-line [here][10]).

```json
{
  "resource": {
    "id": "amazon",
    "name": "Amazon",
    "favicon": "https://amazon.com/favicon.ico",
    "apitemplate": "http://webservices.amazon.com/onca/xml?Service=AWSECommerceService&Operation=ItemSearch&AWSAccessKeyId={accesskey}&AssociateTag={associateid}&SearchIndex=Music&Keywords={q}",
    "testquery": "verdi",
    "mimetype": "application/xml",
    "signature": "HmacSHA256({secretkey})",
    "itempath": "//Items/Item",
    "extractors": {
      "title": "./ItemAttributes/Title",
      "description": "./ItemAttributes/Artist|./ItemAttributes/Manufacturer|./ItemAttributes/Creator",
      "tags": "'advertisement'",
      "url": "./DetailPageURL"
    },
    "privateparameters": {
      "associateid": "VALUE MISSING",
      "accesskey": "VALUE MISSING",
      "secretkey": "VALUE MISSING"
    }
  },
  "searsia": "v1.0.0"
}
```


To use this configuration file, get your Associate Id, Access Key and Secret Key from Amazon's affiliate program
and fill them in under `"privateparameters"`.
The `"apitemplate"` contains the URL parameter `SearchIndex=Music` to restrict the search to include only 
products in Amazon's Music category.

One of the keys of `"extractors"` is `"tags"` with as its value `"'advertisement'"` (the value needs to be an
XPath query, hence the single quote to denote the result is a constant string): This will add the key value
pair `"tags": "advertisement"` to the search output, which is used by the Searsia Client to show advertisements
differently from ordinary search results.

Most of the attributes of this configuration file are also supported by [Searsia Server version 0.4][11], except
`"signature"`, which signs the API request with the Secret Key using a [HMAC-SHA256 signature][12] as required by Amazon.
Testing a Searsia engine in SearsiaServer version 1 is easy and can be done as follows:

        java -jar searsiaserver.jar -m amazon.json -t json


**eBay Partner Network**

Another big online ecommerce site, eBay, offers an affiliate program called the [eBay Partner Network][13]. 
Like Amazon, eBay also offers a [Shopping Services API][14]. The API can be configured as a Searsia engine with the following
configuration file (which runs on-line [here][15]).

~~~json
{
  "resource": {
    "id": "ebay",
    "name": "eBay",
    "favicon": "https://www.ebay.com/favicon.ico",
    "apitemplate": "http://svcs.ebay.com/services/search/FindingService/v1?OPERATION-NAME=findItemsAdvanced&SERVICE-VERSION=1.0.0&SECURITY-APPNAME={appId}&RESPONSE-DATA-FORMAT=XML&REST-PAYLOAD&keywords={q}&categoryId=180015&descriptionSearch=true&affiliate.trackingId={affiliateId}&affiliate.networkId=9",
    "testquery": "mozart",
    "itempath": "//item",
    "extractors": {
      "title": "./title",
      "image": "./galleryURL",
      "description":".//categoryName|.//conditionDisplayName|.//currentPrice/@currencyId|.//currentPrice",
      "price": "concat(string(.//currentPrice/@currencyId),' ',string(.//currentPrice))",
      "url": "./viewItemURL"
    },
    "privateparameters": {
      "appId": "VALUE MISSING",
      "affiliateId": "VALUE MISSING"
    },
    "mimetype": "application/xml"
  },
  "searsia": "v1.0.0"
}
~~~

To use this configuration file, get your App Id and Affiliate Id from eBay and fill them in 
under `"privateparameters"`.The `"apitemplate"` contains the URL parameter `categoryId=180015` 
to restrict the search to include only products in eBay's Sheet Music category.
This configuration file produces several custom attributes like `"image"` and `"price"`.


### Affiliate networks: ShareASale

Many smaller sites offer affiliate programs through an affiliate network. We will look here at 
[ShareASale][16], an affiliate network that brings together merchants (that run the affiliate programs), 
affiliates (that publish the advertisements, i.e., us) and users (the users of our search engine).
As an affiliate at ShareASale, you have to apply to the program of a merchant. As we run a search engine
for sheet music, we applied to the program of [Music Box Attic][17], a wonderful site that offers 
music boxes with custom tunes.

Unlike the affiliate programs of Amazon and eBay, ShareASale does not offer an API to search the 
products of Music Box Attic. Instead, it offers a comma-separated file with products. To search
the advertisements of Music Box Attic, we create a Searsia configuration / result file that contains 
all the advertisements as follows. 

```json
{
  "hits": [
    {
     "title": "Music Box I Hope You Dance",
     "description": "Handcrafted Ercolano Music Box with 18 Note Tune-I Hope You Dance",
     "tags": "advertisement",
     "url": "http://www.shareasale.com/m-pr.cfm?merchantID=40198&userID=1640777&productID=588034773"
    },
    {
     "title": "Music Box Can't Help Falling in Love",
     "description": "Romantic Jewelry Box with 30 Note Tune Can't Help Falling in Love",
     "tags": "advertisement",
     "url": "http://www.shareasale.com/m-pr.cfm?merchantID=40198&userID=1640777&productID=588034774"
    },
...
  ],
  "searsia": "v1.0.0",
  "resource": {
    "id": "musicboxattic",
    "mimetype": "application/searsia+json",
    "name": "MusicBoxAttic",
    "testquery": "box",
    "rerank": "bestrandom",
    "urltemplate": "https://www.musicboxattic.com"
  }
}
```

This configuration contains the `"rerank"` parameter, which 
instructs Searsia to search and rerank the results. The parameter value `"bestrandom"` instructs
Searsia to retrieve the best results or, if there are no matching results, to retrieve some random
results (so there is always an advertisement to be shown).

We described this approach in our blog post: [A search engine in your browser][18].
In this case however, it is not the Searsia Client that reranks the 
results, but the Searsia Server. That's why the on-line engine at Dr. Sheet Music -- [here][19] -- only 
shows the top 10 results for a query.
 

### Affiliate of charities: CharityChoice

Searsia provides full control of what is shown in advertisements. 
If you do not want to make money with your search engine, but instead want
to have some positive societal impact, you might advertise for instance charities.
Below you find a configuration file
for [CharityChoice][20], a site with a search engine for 160,000 registered UK charities.
The configuration file below shows how Searsia scrapes search results from CharityChoice.

```json
{
  "resource": {
    "id": "charitychoice-uk",
    "name": "CharityChoice",
    "apitemplate": "http://www.charitychoice.co.uk/charities/search?t=qsearch&q={q}",
    "testquery": "child",
    "itempath": "//div[@class='search-listings']/div[./h2/a]",
    "extractors": {
      "title": "./h2/a",
      "tags": "'advertisement'",
      "description":"./p/text()",
      "message": "'CharityChoice, the premier guide to Charities in the UK'",
      "banner": "./div[@class='banner-ad']/a/img/@src",
      "url": "concat('http://www.charitychoice.co.uk',string(./h2/a/@href))"
    },
    "mimetype": "text/html",
    "maxqueriesperday": 150,
    "rerank": "random",
    "urltemplate": "http://www.charitychoice.co.uk/charities/search?t=qsearch&q={q}"
  },
  "searsia": "v1.0.0"
}
```

Here, the `"rerank"` parameter is again used to rerank, but in this case only the top
results already provided by CharityChoice are reranked. The parameter `"maxqueriesperday"`
instructs Searsia to send no more then 150 queries per day to CharityChoice, so Searsia 
will not put too much load on the site. Searsia might show cached results
if the maximum is reached.

## Sheet Music & Advertisements

Search advertising with tracking users is demonstrated by [Dr. Sheet Music][8], a
federated search engine that searches more than 50 search engines for sheet music.
Dr. Sheet Music participates in the affiliate programs of Amazon, eBay, and Music 
Box Attic (via ShareASale). The results for eBay are not marked as advertisements, 
because they only show sheet music, but Dr. Sheet Music will receive a commission 
from eBay if sheet music is purchased through the site. 

Occasionally, Dr. Sheet Music shows advertisements for charities, including CharityChoice 
and GoedeDoelen.nl (a similar site for Dutch charities). A query for [amazon][21] 
shows two affiliate programs and two charity advertisements on a single page.

Dr. Sheet Music is configured to show advertisements without third-party tracking cookies, 
web bugs, and other tracking code. Searsia makes sure that user information
is not leaked to e-commerce sites that run affiliate programs, for instance by
downloading images and banners via the Searsia server, and by following a strict 
HTTP referrer policy. We described this in our previous post on 
[privacy implications of federated search][22].


## Conclusion

We showed that ethical search advertising is possible, and we showed how to configure
Searsia to show advertisements from a diverse set of affiliate programs, affiliate 
networks and charities. 
There are [many more affiliate programs and networks][23] to choose from.

As a final "advertisement" for ethical advertising it is good to note that 
currently, Dr. Sheet Music's advertisement are _not_ blocked by ad blockers like 
Adblock Plus. In countries like Germany, ad blockers are used by almost 30% of 
desktop users, so ethical advertising using Searsia will substantially increase 
the audience for your search ads.


## Acknowledgements

We are grateful to the [Vietsch Foundation][24] and [NLnet Foundation][25] for
funding our work on search advertising without tracking users.

[1]: https://en.wikipedia.org/wiki/Cost_per_impression "Cost per impression on Wikipedia"
[2]: https://en.wikipedia.org/wiki/Pay-per-click "Pay-per-click on Wikipedia"
[3]: https://en.wikipedia.org/wiki/Tracking_bug "Tracking bug aka Web Beacon on Wikipedia"
[4]: https://en.wikipedia.org/wiki/HTTP_cookie#Third-party_cookie "Third-party HTTP cookie on Wikipedia"
[5]: /blog/2017-11-08-affiliate-marketing-as-ethical-advertising/ "Affiliate marketing as ethical advertising"
[6]: https://blogs.cornell.edu/info2040/2017/10/18/click-farms-and-the-value-of-online-advertisements/ "Click farms and the value of online ads"
[7]: https://github.com/searsia/searsiaserver/tree/v1 "Searsia Server v1 on Github"
[8]: https://drsheetmusic.com "Dr. Sheet Music"
[9]: https://affiliate-program.amazon.com/ "Amazon affiliate program"
[10]: https://drsheetmusic.com/searsia/amazon.json "Amazon affiliate results at Dr. Sheet Music"
[11]: http://searsia.org/engines.html "Searsia Engines version 0.4"
[12]: http://docs.aws.amazon.com/AWSECommerceService/latest/DG/HMACSignatures.html "HMAC-SHA256 Signatures for REST Requests"
[13]: https://epn.ebay.com "eBay Partner Network"
[14]: http://developer.ebay.com/DevZone/finding/CallRef/index.html "eBay developers network API reference"
[15]: https://drsheetmusic.com/searsia/ebay.json "eBay affiliate results at Dr. Sheet Music"
[16]: https://www.shareasale.com/ "ShareASale"
[17]: https://www.musicboxattic.com/ "Music Box Attic"
[18]: /blog/2017-04-21-search-engine-in-your-browser/ "A search engine in your browser"
[19]: https://drsheetmusic.com/searsia/musicboxattic.json "Music Box Attic affiliate results at Dr. Sheet Music"
[20]: http://www.charitychoice.co.uk/ "Charity Choice"
[21]: https://drsheetmusic.com/sheet-music/amazon "Dr. Sheet Music - amazon"
[22]: /blog/2017-10-02-privacy-implications-of-federated-search/ "Privacy implications of federated search"
[23]: https://www.highstreet.io/affiliate-networks-europe-quick-list/ "Affiliate networks in Europe: a short list"
[24]: http://vietsch-foundation.org/ "Vietsch Foundation"
[25]: https://nlnet.nl/ "NLnet Foundation"

