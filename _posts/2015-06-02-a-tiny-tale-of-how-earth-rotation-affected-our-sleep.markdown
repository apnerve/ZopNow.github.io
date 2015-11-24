---
layout: post
title:  "A tiny tale of how earth rotation affected our sleep"
date:   2015-07-02 20:43:29 +0530
categories: devops
---
I woke up from a call from Mukesh apparently the website was not working for some of the people. In ZopNow’s history, it’s one of those rare occurrences which can be termed as the blue moon event. For Ujjawal and I, all hell broke lose. This was important as we had just rolled out our new website to all our visitors after doing an A/B test. We had released it for 25% of our visitors first and after carefully monitoring for a day, we declared it is good to go. That was last night.

As we are all human and by nature we tend to relate any shifts from equilibrium with the most recent change, we started investigating from that context. We had just faced slow http ddos attacks as well in past fortnight, which had made our mysql server connection count very high in the duration of the attack. So, after making sure its not the case, we thought it has something to do with the new website codebase and started looking at the usual associated stats. CPU was high but process list was not showing any processes. We went through slow query logs, open TCP connections on the servers, disk io stat, mysql temporary table sizes, any potential large rollbacks and all other kind of things which we knew in our heart should not affect but load average was crazy. Everything was fine except the CPU usages. 

When we exhausted every option inside the box, it was time to crawl out of it. I typed ’30 Jun 2015’ in google. I looked at the first result which was “NASA explains why 30 June will get an extra leapsecond…”. Time has messed with me so many times - once it was simple timezone, once it was daylight saving time, once it was different time on different servers - that I take very seriously to any time changes. So, I read about Leap Second (https://en.wikipedia.org/wiki/Leap_second)  - it was done last in 2012. So searched for "leap second 2012 bug” and well, there it was, staring at the face.

We just stopped ntp and did date -s "`date`” and it got fixed. 

Next time when CPU usages on mysql servers are very high and everything else looks correct, we shall remember to look for leap second. Not for couple of years though. :) 

