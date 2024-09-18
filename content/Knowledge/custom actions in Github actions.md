Parent:: [[Github Actions Action]]

# Summary
You can have custom built actions that interact with your repo, github api, and third party apis. 

If building to share with others they recommend let the action have it's own repo. If you will not be sharing then you should put it in `.github/actions/<action name>`


> [!tip] When calling github in custom actions
> You should use `GITHUB_API_URL` for the api basename and `GITHUB_GRAPHQL_URL` for graphql basename. This will ensure your action works with [[Github Enterprise Server]]

# Body
There are three types of custom actions.

## [[Docker Container Action]]
![[Docker Container Action#Summary]]
## [[Javascript Action]]
![[Javascript Action#Summary]]
## [[Composite Actions]]
![[Composite Actions#Summary]]