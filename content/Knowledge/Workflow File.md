Parent:: [[Github Actions Workflow]]

# Summary

# Body
Sections of a workflow file are as follows.

1. name
	1. This is the name of the workflow, if omitted the name of the file will be used
2. run-name
	1. Optional - The name for workflow runs generated from the workflow, which will appear in the list of workflow runs on your repository's "Actions" tab. This example uses an expression with the `github` context to display the username of the actor that triggered the workflow run. For more information, see "[Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#run-name)."
3. on
	1. The trigger for the workflow [[Github Actions Event]]
4. jobs
	1. Groups the jobs of the workflow
	2. `<Job Name>` 
		1. defines the job the following keys will configure this job
		2. on
			1. This will be the label to control what github runner will be used - [[Github Actions Runners]]
		3. steps
			1. Each item in list will be a seperate [[Github Actions Action]] or script
			2. uses
				1. This will specify a [[Github Actions Action]] to run
				2. with
					1. This will pass a map of input parameters to the action
				3. run
					1. This will execute the shell script specified

There are many more than just the above but the above are generally to loose structure of the file to see the full layout of options in the file see [docs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
