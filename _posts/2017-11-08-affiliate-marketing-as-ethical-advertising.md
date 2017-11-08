---
layout: post
title: Affiliate marketing as ethical advertising
subtitle: by Djoerd Hiemstra
bigimg: /img/searsia-wood.jpg
share-img: http://searsia.org/blog/img/searsia-wood.jpg
tags: [advertisements, privacy]
---

Internet advertising is a completely messed-up, multi-trillion euro business 
that is controlled by a few big players, most notably Google and Facebook. 
Their business models are based on figuring out as much information about 
people as possible, and then using people's weaknesses and vulnerabilities 
to persuade them to click on advertisements. 

### A dystopia to make people click

The worrying implications of these 
companies' _persuasion architectures_ are wonderfully described by Zeynep 
Tufekci's TED talk: 
[We are building a dystopia just to make people click on ads][1], in which
she shows how companies like Facebook and Google manipulate people in hidden, 
subtle and unexpected ways. She also describes in detail how their 
advertising programs can be used not only to sell shoes, but also to swing 
elections and gain political influence.

### Trackers are really everywhere

In case you are wondering whether Tufekci overreacts, have a look at 
the number of trackers that Steven Englehardt and Arvind Narayanan found in 
[one million popular web sites][2]. Their study finds Google Analytics 
on 75% of the web sites. Even more worrying is that all 
of the top 5 third party trackers, and even 12 of the top 20 trackers, are 
owned by Google. Facebook and Twitter, while not as ubiquitously present as 
Google, still have trackers on more than 10% of sites they crawl.
 
So, Google is not only tracking what you search for and click on, they are 
also tracking other websites you visit, despite the fact that many 
users tell Google explicitly: [Do Not Track][3]. Google follows your online 
activities on millions of sites and stores your data indefinitely. That 
data can be subpoenaed by lawyers, even for civil cases like divorce. 
[Google answered over 100,000 such requests][4] last year. 

### Google's AdSense and other advertisement programs

Using Google's AdSense program is tempting, because it is effective: 
Google really _does_ manage to make people click on advertisements. 
But if you run a Searsia search engine like [Dr. Sheet Music][5], then using 
AdSense is not an attractive option for several reasons: 

1. Google bans search competitors by requiring [original content created from scratch][6], which a search engine typically does _not_ provide.
2. [Google does not allow the use of other third party advertisements][7], limiting your search engine to get its advertisements from Google only. (Remember that Searsia is a federated search engine that is designed to receive results from _multiple_ sources.) 
3. Google will approve an AdSense application faster if [the site uses Google Analytics][8], which as we saw, is the tracking software that is available on 75% of the web sites already.
4. AdSense does not give the site control over the advertisements that are displayed: AdSense shows whatever advertisement Google deems appropriate. 
5. Also, your site has to allow [third party cookies][9] to be set, that is, cookies from a site other than your own site.

At this point we may conclude that advertisement programs like Google's
AdSense are both unethical and unsuited for sites that run
a Searsia search engine. So, does this prevent people that build a 
search engine with Searsia from monetizing their sites? 
We don't think so. There is an alternative to the surveillance 
advertising model of Google that is often overlooked: the so-called 
_affiliate marketing_.


### Affiliate marketing

[Affiliate marketing][10] is a type of on-line marketing where an affiliate (also called the [publisher][11]) is paid a commission for each sale that is closed based on a link or advertisement on the affiliate's web site. Running an affiliate program is often as easy as putting a hyperlink to a merchant's product on your site that contains your _affiliate identifier_. When a visitor of your site clicks that link, the merchant (or affiliate network) will know from this identifier that the visitor originated from your site. If this user purchases the product (or any other product) on the site within a certain amount of time, then the affiliate receives a commission, which is often a percentage of the product's price.

Affiliate programs do track their users _after_ they have clicked an affiliate link or advertisement. This tracking is often done by cookies that are placed by the merchant's website, so these cookies are not third party cookies. Many affiliate programs use cookies that disappear after a limited time, say 14 days, so a purchase within 14 days after clicking will count for the affiliate program. Users will however not be tracked if they only use the search engine, nor will they see personalized advertisements.

One might argue that affiliate marketing is much like other on-line
advertising and marketing programs, but with the following differences: 

1. Not the [advertisement network][11] but the affiliate decides which advertisement or link is placed on the site.
2. Affiliate programs are less prone to [ad fraud][12] like impression fraud or click fraud, because the affiliate is only paid when the product is actually purchased and paid for. 
3. There are often little restricting conditions attached to affiliate programs such as the above mentioned need for original content, the ban of advertisements from other providers, or the need to allow third party cookies.
4. There is no incentive for affiliate programs or merchants to sell user data or share personal data, because they do not control advertisement placement, nor do they have to bother about advertisement fraud.

Many merchants run their own affiliate programs. Examples are the programs by [Amazon][13] or [eBay][14]. Many smaller merchant's affiliate programs are available through affiliate networks like [ShareASale][15] or [CJ Affiliate][16]. Most programs allow owners of small web sites, like personal blogs, to sign up for their programs. 


### Conclusion

Affiliate programs can be seen as advertising programs where the affiliate/publisher is in control of the advertisements that are placed on their site. The programs provide the affiliate with a fair share of the revenue of the merchant, without the need to track and target users. Affiliate marketing, implemented successfully, can serve as an ethical approach to providing advertisements in search engines, not based on excessive user tracking, but instead based on the mutual trust between affiliates and merchants.

In a future blog post we will describe in detail how Searsia supports affiliate 
programs. We will provide detailed examples of Searsia's [resource configurations][17] for big affiliate programs like [eBay's Partner Network][14] and for affiliate networks like [ShareASale][15]. Sharing Searsia's resource configurations for affiliate programs will give search engine developers quick access to several affiliate programs, and with some adaptation access many more.

### Acknowledgements

We thank the [Vietsch Foundation][18] and [NLnet Foundation][19] for funding our work on ethical search advertising.


[1]: https://www.ted.com/talks/zeynep_tufekci_we_re_building_a_dystopia_just_to_make_people_click_on_ads "Zeynep Tufekci, TED talk"
[2]: https://webtransparency.cs.princeton.edu/webcensus/ "Online tracking: A 1-million-site measurement and analysis"
[3]: https://en.wikipedia.org/wiki/Do_Not_Track "The Do Not Track http header"
[4]: https://donttrack.us/ "Don't track us! by Duckduckgo"
[5]: https://drsheetmusic.com "Dr. Sheet Music - Search"
[6]: https://www.google.com/adsense/start/get-started/ "Google AdSense getting started"
[7]: https://www.google.com/adsense/new/localized-terms "Google AdSense - Terms and Conditions"
[8]: http://technischblog.com/how-to-approve-google-adsense-account-within-3-working-days/ "Shubham Gupta: How to Approve Google AdSense Account within 3 Working Days"
[9]: https://en.wikipedia.org/wiki/HTTP_cookie#Privacy_and_third-party_cookies "HTTP Cookie on Wikipedia"
[10]: https://en.wikipedia.org/wiki/Affiliate_marketing#Performance.2FAffiliate_marketing "Performance Martketing / Affiliate Marketing"
[11]: /blog/2017-05-26-some-thoughts-on-search-advertising/ "Some thoughts on search advertising"
[12]: https://en.wikipedia.org/wiki/Ad_fraud "Ad fraud on Wikiepdia"
[13]: https://affiliate-program.amazon.com/ "Amazon Associatees"
[14]: https://partnernetwork.ebay.com/ "eBay Partner Network"
[15]: https://www.shareasale.com/ "ShareASale Affiliate marketing"
[16]: https://www.cj.com/ "CJ Affiliate"
[17]: http://searsia.org/engines.html "Searsia - Engines"
[18]: http://vietsch-foundation.org/ "Vietsch Foundation"
[19]: https://nlnet.nl/ "NLnet Foundation"

