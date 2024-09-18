Parent:: [[Load shedding 1]]
supports:: [[Netflix]] [[Job Search 2024]]
author:: [[Manuel Correa]] [[Arthur Gonigberg]] [[Daniel West]]
# Summary 

# Body
[Link to the article](https://netflixtechblog.com/keeping-netflix-reliable-using-prioritized-load-shedding-6cc827b02f94)
The high level arc is the following 
![[netflix load shedding arc.png]]

requests are divided into three categories
1. NON_CRITICAL
2. DEGRADED_EXPERIENCE
3. CRITICAL

They then use [[Zuul]] to categorize the requests. It then scores the request from 1 to 100 given it's individual characteristics. It is done as first step of request lifecycle so that it may be used there after.

Their implementation is analogous to a [[priority queue]] implementation

They dynamically set the priority that will be dropped. If less than X where X is dynamically set then they will drop the traffic. 

They throttle on the service level as well as the global level. They seem to leave this decision to [[Zuul]] to make.

For Service level shedding they base it on 
- failures 
- latency

For global level shedding they base it on
- CPU Utilization
- Concurrent requesxts
- connection count

Cubic function of shedding so it can throttle rather aggressively if things get bad

In the event you are shedding [[Zuul]] informs the client to back off and how many retries they get and what time window. This allows the gateway to provide [[Back pressure]]. This is how they prevent [[Retry Storm]]s  

They then have the ability to use a [[Failure Injection Tool]] which tells [[Zuul]] to drop ranges of priority for specific devices or members. This allows them to test the experience for the taxonomy of requests and test which requests are safe to drop. 

They use their infrastructure experimentation platform [[ChAP]] to A/B test the implementation of [[Load shedding 1]]. They select a control group to apply the throttle to and measure whether the KPIs are affected for those users based against the baseline. 

If they find deviation they can fix it then schedule that experiment to happen on a schedule. 