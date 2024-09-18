Parent:: [[Github Actions Action]]
supports:: [[custom actions in Github actions]]

# Summary
Javascipt actions run faster than Docker actions and run directly on the runner machine.


> [!warning] When writing JavaScript Actions
> You will need to use vaniella JavaScript and not rely on other binaries. This will ensure capability when running on a GitHub hosted runner.

# Body
> If you're developing a Node.js project, the GitHub Actions Toolkit provides packages that you can use in your project to speed up development. For more information, see the [actions/toolkit](https://github.com/actions/toolkit) repository.