---
parent:
  - "[[Be the king of content]]"
aliases: 
tags:
  - blog
---
# Summary 
 need to work on the title but likely a pun to be found there.
 
The idea is to talk about the options for rollback in [[CAP]]. Mainly focusing on the benefit gained from stack level rollbacks.

Need to think about the small notes that then sum up into an overall post or paper -> listened to the How to take notes [[Zettelkasten]] guy [[Sönke Ahrens]].  
# Body
## Problem of only having Canary
- You may be able to redirect traffic but that won't save you from a bucket policy failure or an ALB issue
	- Likely going to use the ALB issue as that is applicable to [[RulesLab]]
## Enter the Stack
- [AWS link](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-rollback-triggers.html)
## Example
- Live example of rollbacks working in Capital one
## Look ahead
- CloudDoctor based rollbacks
