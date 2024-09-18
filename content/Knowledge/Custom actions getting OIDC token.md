Parent:: [[Github Actions OIDC]]
supports:: [[custom actions in Github actions]]

You can call `getIDToken` in the [[Github Actions Toolkit]]

you will need permission to be able to get the token 
> The job or workflow run requires a `permissions` setting with [`id-token: write`](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token). You won't be able to request the OIDC JWT ID token if the `permissions` setting for `id-token` is set to `read` or `none`. 