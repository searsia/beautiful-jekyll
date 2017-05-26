---
layout: post
title: Some thoughts on search advertising
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-desktop.jpg
share-img: http://searsia.org/blog/img/searsia-desktop.jpg
tags: [advertisements]
---

In many respects, advertisements drive the web. The biggest web
companies today — yes, Google and Facebook — get most of their revenue
from advertisements, but also many small web sites can exist because of
advertising. So, as we work at Searsia to provide developers with open
source tools to build beautiful search engines, we also want to provide
them with easy ways to include advertisements alongside the search results.
For, why would people make beautiful search engines if it only costs them?

## Advertisers and publishers

If you plan to put advertisements along-side your search results, then
the terminology used in online advertising can be confusing. The
Wikipedia page on [on-line advertising][1] distinguishes _advertisers_
that _buy_ advertisement space and _publishers_ that _sell_ advertisement
space. Obviously, if you are building a search engine that displays ads,
then you are a publisher — even though a search engine merely directs
users to the real publishers. As a publisher/seller you will interact
with advertisers/buyers through an [advertising network][2], a company
that connects advertisers to publishers. 

## Advertising platforms 

Online advertising is highly automated on platforms that facilitate
the buying and selling of advertisement space. Such platforms, often
called [ad exchanges][3], serve multiple ad networks. Platforms
are increasingly specializing towards either buying ad space or selling 
ad space, in which case they are called [demand-side platforms][4] or 
[supply-side platforms][5]. Platforms determine the prices of the 
advertisement space through _bidding_: Advertisers bid on advertisement
space by deciding what they are willing to pay for each impression of 
their ad or for each click on their ad. 

## Real-time bidding

This bidding process within an ad exchange can be very dynamic. 
In [real-time bidding][6], advertising space is bought and sold on a
per-impression basis. Real-time bidding sounds fascinating, but it is
really a search: The platform searches the best advertisement
based on various pieces of data, such as the user's demographic
information, browsing history, and location. The more accurate the
[behavioral targeting][7] of users, the more the advertisement network
earns. That's why networks _track_ users online. They profile users by
"following" them around to gather as much data on users as possible.
This way, when a user reads an article on a publisher's web site, say 
a real publisher like a newspaper, the advertisement network can guess 
what advertisement the user is willing to click, and ultimately what 
product a user is willing to buy.

## Real-time bidding without tracking

Real-time bidding for search engines is much easier than real-time
bidding for a newspaper site: Users of search engines tell the search
engine explicitly what they are willing to click on. What would be a good ad
for the query "car"? Right, an ad for the Tesla Model 3, for instance!
There is absolutely no real need to track users for search ads.
DuckDuckGo describes this aptly on the [DuckDuckGo company pages][8]:

> It is a myth that search engines need to track you to make money on
> Web search. When you type in a search, we can show an ad just based
> on that search term. For example, if you type in, "car" we show a
> car ad. That doesn't involve tracking because it is based on the
> keyword and not the person.

## OpenRTB: Open Real-Time Bidding

Interestingly, there is an open standard for real time bidding called
[OpenRTB][9]. OpenRTB was launched in late 2010 by six companies in 
online advertising, representing both demand-side and supply-side 
platforms. The standard is actively maintained by the Interactive 
Advertising Bureau ([IAB][10]), and its latest version, 
[OpenRTB version 2.5][11], was released in December 2016. 

Many advertisement platforms support OpenRTB, usually version 2.3, which 
is currently the most widely adopted release. Examples are [SSPHWY][12], 
[DataXu][13], [OpenX][14], [BrightRoll][15] (by Yahoo), [DoubleClick][16]
(by Google), and [RythmOne][17] that claimed last week that it provides 
the first [IAB certified][18] implementation of OpenRTB. 

## OpenRTB Native ads

One of the biggest changes in OpenRTB version 2.3 compared to previous 
versions is the support for native advertising. 
[Native advertising][19] provides ads that match the form and function of 
the site on which they appear. One of the main examples of native ads are 
_search ads_: ads that appear within search result pages.

The difference between native ads and traditional _display ads_ comes down 
to metadata. Display ads, such as the traditional banner ad, need only
an image of predefined size. Native ads however, provide
several separate pieces of information like a title, a summary, a thumbnail
image, and the brand's logo. This way, its appearance can be tailored 
to a publisher's content feed or a search engine's result page. 
Of course, advertisements should always be clearly marked such that they
are recognized as paid content by the users.

OpenRTB comes with a separate specification for native ads, 
[OpenRTB Native 1.2][20], which contains a detailed explanation of the
sub-protocol of the OpenRTB real-time bidding interface for native ads. 

## Conclusion

To conclude, on-line advertising using real-time bidding sounds fancy, but 
it really is just the  advertisement platform _searching_ its ads database 
for the best ad for a single impression. 
Furthermore, real-time bidding for a search site is more easy than real-time
bidding for many other sites, because the advertisement network can show an 
ad based on the user's search query, without the need to track the user.
Finally, there is an open standard for real-time bidding, fittingly called 
OpenRTB, that is used by many advertising networks and that includes a 
detailed subprotocol for native search ads.

At Searsia, we are currently investigating how to deliver native search ads
using the OpenRTB standard. Stay tuned if you want to monetize your Searsia
federated search engine.


[1]: https://en.wikipedia.org/wiki/Online_advertising "Wikipedia: Online advertising"
[2]: https://en.wikipedia.org/wiki/Advertising_network "Wikipedia: Advertising network"
[3]: https://en.wikipedia.org/wiki/Ad_exchange "Wikipedia: Ad Exchange"
[4]: https://en.wikipedia.org/wiki/Demand-side_platform "Wikipedia: Demand-side platform"
[5]: https://en.wikipedia.org/wiki/Supply-side_platform "Wikipedia: Supply-side platform"
[6]: https://en.wikipedia.org/wiki/Real-time_bidding "Wikipedia: Real-time bidding"
[7]: https://en.wikipedia.org/wiki/Behavioral_targeting "Wikipedia: Behavioral targeting"
[8]: https://duck.co/help/company/advertising-and-affiliates "DuckDuckGo: Advertising and Affiliates "
[9]: http://openrtb.github.io/OpenRTB/ "OpenRTB"
[10]: https://iab.com "Interactive Advertising Bureau"
[11]: https://iabtechlab.com/specifications-guidelines/openrtb/ "OpenRTB Specifications & Guidelines"
[12]: http://ssphwy.com/ "SSPHWY: One OpenRTB Integration, Many Ad Exchanges"
[13]: https://www.dataxu.com/tag/openrtb/ "DataXu OpenRTB"
[14]: http://openx.com "OpenX"
[15]: https://brightroll.com/blog/how-our-industry-approaches-standards-digital-advertising "BrightRoll"
[16]: https://developers.google.com/ad-exchange/rtb/openrtb-guide "Google: Ad Exchange OpenRTB Integration" 
[17]: https://www.rhythmone.com "RythmOne"
[18]: https://www.rhythmone.com/news/2017/05/16/rhythmone-first-to-achieve-iabs-openrtb-certification "RythmOne"
[19]: https://en.wikipedia.org/wiki/Native_advertising "Wikipedia: Native advertising"
[20]: https://www.iab.com/news/openrtb-native-1-2-adds-dynamic-creative-third-party-ad-serving-support/ "OpenRTB Native 1.2"






