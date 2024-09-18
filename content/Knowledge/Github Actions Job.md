Parent:: [[github actions ontology]]

# Summary
can be sequential or in order within a workflow. Each job will be executed within the same runner thus can share data with other jobs within the workflow.

> For example, you can have a step that builds your application followed by a step that tests the application that was built.

# Body
By default jobs have no dependencies and will all run in parallel to one another.