---
title: 'Bookmarklet and usage within Salesforce Org'
slug: 'sf-org-bookmarklets'
description: 'tools that I use with orgs to save time'
pubDate: 'Mar 01 2025'
heroImage: '/blog-placeholder-2.jpg'
---

Book *MARKS* are usually links, but Book *MARKLETS* are IIFE that excutes small code prefixed with `javascript:`.

When clicked, the script runs in the context of the active page, allowing modifications like hiding elements, filling forms, or fetching data.

```js
javascript:(function(){url = window.location.origin; window.open(url+'/lightning/page/home',"_blank")})()
```

Here's a list of some redirects that I have setup, so that I can access menus in all the salesforce orgs with one click.

```js
javascript:(function(){url = window.location.origin; window.open(url+'/lightning/page/home',&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/SetupOneHome/home?setupApp=all%27;%20window.open(url,%22_blank%22)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/SetupOneHome/home?setupApp=service%27;%20window.open(url,%22_blank%22)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/AppExchangeMarketplace/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/SetupNetworks/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/o/Account/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/o/Contact/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/InboundChangeSet/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/OutboundChangeSet/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/ApexDebugLogs/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/ObjectManager/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/Flows/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/EventObjects/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin+'/lightning/setup/CustomMetadata/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = window.location.origin.toString().replace('lightning.force.com','my.salesforce.com'); window.open(url+'/_ui/common/apex/debug/ApexCSIPage','_blank');})()";

javascript:(function(){url = window.location.origin+'/ltng/switcher?destination=classic&referrer=%2Flightning%2Fpage%2Fhome%27;%20window.open(url,%22_self%22)})()";

javascript:(function(){url = window.location.origin.toString().replace('lightning.force.com','my.salesforce.com'); window.open(url+'/0WO/o','_blank');})()";

javascript:(function(){url = window.location.origin.toString().replace('lightning.force.com','my.salesforce.com'); window.open(url+'/0Hh/o','_blank');})()";

javascript:(function(){url = window.location.origin.toString().replace('lightning.force.com','my.salesforce.com'); window.open(url+'/0Hn/o','_blank');})()";

javascript:(function(){url = window.location.origin+'/lightning/o/WorkOrder/list?filterName=Recent%27;%20window.open(url,%22_blank%22)})()";

javascript:(function(){url = window.location.origin+'/lightning/o/ServiceTerritory/home'; window.open(url,&quot;_blank&quot;)})()";

javascript:(function(){url = 'https://workbench.developerforce.com/login.php'; window.open(url,&quot;_blank&quot;)})()";

```
