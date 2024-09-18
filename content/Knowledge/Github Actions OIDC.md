Parent:: [[Github Actions]]

# Summary
To control access to third parties github actions supports an [[OIDC]] provider. This means third parties that support [[OIDC]] can form a trust relation with [[Github Actions OIDC]]'s provider and use it to create short lived tokens.

# Body
The following are typically used in the conditions on the cloud provider. 

> - **Audience**: By default, this value uses the URL of the organization or repository owner. This can be used to set a condition that only the workflows in the specific organization can access the cloud role.
> - **Subject**: By default, has a predefined format and is a concatenation of some of the key metadata about the workflow, such as the GitHub organization, repository, branch, or associated [`job`](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idenvironment) environment. See "[Example subject claims](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect#example-subject-claims)" to see how the subject claim is assembled from concatenated metadata.

