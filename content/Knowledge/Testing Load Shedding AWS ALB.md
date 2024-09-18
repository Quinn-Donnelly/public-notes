Parent:: [[Load shedding]]
# Summary 
Testing setting up [[Load shedding]] on my AWS account for a simple use case test.
# Body
I was able to set it up using listener rules. Set the default rule to a 404 set the healthy traffic rule to path based route to a lambda and set the priority to 20. 

Then I made a rule that returned a fixed response with a retry limit and time window. That was set to priority 100. Then when enabled I moved it from priority 100 to 1 which kicked in the load shedding. I had it based on the header priority and value NON_CRITICAL. Similarly I could have many different shedding rules at play that I could move into priority order.

Fixed response only allowed me to set the status code and the body though so I couldn't set the http headers with that method.