## Pipeline Task

A custom Azure Pipelines Task is comprised generally of two main components--configuration and runtime behavior. All of this is provided via a few main files for an extension. First off, a manifest file must specify the pipeline task contribution. 

The key file for defining a task, however, is the `task.json` file (see schema [here](https://github.com/Microsoft/azure-pipelines-task-lib/blob/master/tasks.schema.json). This file defines the task metadata, version, inputs, and scripts to execute. See the docs and examples listed below for a better understanding of how to provide various inputs as part of task configuration. One item that is not covered in the docs but may be useful is allowing the user to select a service connection. To do this, you must add an input with the type `"connectedService:{service-connection-type}"` (replacing `{service-connection-type}` with the relevant service connection). If you want to populate input options with results from external calls, you will need to view use the `data source bindings' referenced in the above section. See documentation [here](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/dataSources.md#data-source-bindings). 

Now, we shift focus to the scripts themselves. The behavior before, during, and after a pipeline run is dictated by one or more JavaScript files. These scripts may be simple or more complex, but Azure DevOps provides some libraries and interfaces to make complex actions a bit easier. 

First, there is an SDK designed specifically for pipeline tasks. The main repo is [here](https://github.com/microsoft/azure-pipelines-task-lib/tree/master/node), the Node portion is [here](https://github.com/microsoft/azure-pipelines-task-lib/blob/master/node), and the documentation is [here](https://github.com/microsoft/azure-pipelines-task-lib/blob/master/node/docs/azure-pipelines-task-lib.md) (in addition to info from the README's). This library helps with a variety of tasks that may need to be performed inside a pipeline. Two of these include getting input parameters specified by the user and getting service connection information to make external calls. See the docs for more info on how to make these calls. 

Additionally, you may need to interact with the [Azure DevOps REST API](https://docs.microsoft.com/en-us/rest/api/azure/devops/?view=azure-devops-rest-6.1) as part of the pipeline task. You can certainly construct and send custom calls using axios or another library. However, Azure DevOps also provides a client library for interacting with the API via Node. You can view the library [here](https://github.com/microsoft/azure-devops-node-api) to view the README, some examples, and even the source code. This library provides a simpler way to make REST calls to Azure DevOps. (NOTE: You may have to investigate the source code to understand what methods are available. Cross-reference with the REST API reference [here](https://github.com/microsoft/azure-devops-node-api) to understand the relationships). 

To get started, the Azure DevOps documentation provides an example tasks [here](https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-build-task?view=azure-devops&viewFallbackFrom=vsts) and some general instruction (including info about task versioning) [here](https://docs.microsoft.com/en-us/azure/devops/extend/develop/integrate-build-task?view=azure-devops). 

It may also be useful to view some Open Source examples. [This repo](https://github.com/microsoft/azure-pipelines-extensions) contains some under the `Extension` folder, and [this repo](https://github.com/microsoft/azure-pipelines-tasks) has a number under the `Tasks` folder including some particularly good examples for [Docker](https://github.com/microsoft/azure-pipelines-tasks/blob/master/Tasks/DockerV2), [Azure CLI](https://github.com/microsoft/azure-pipelines-tasks/tree/master/Tasks/AzureCLIV2), and more.

### Useful Links
- [Pipelines Task SDK](https://github.com/microsoft/azure-pipelines-task-lib)
- [Pipelines Task SDK for Node](https://github.com/microsoft/azure-pipelines-task-lib/tree/master/node)
- [Typscript functions to be used inside pipelines](https://github.com/microsoft/azure-pipelines-task-lib/blob/master/node/docs/azure-pipelines-task-lib.md)
- [Step-by-step example](https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-build-task?view=azure-devops&viewFallbackFrom=vsts)
- [Task Schema](https://github.com/Microsoft/azure-pipelines-task-lib/blob/master/tasks.schema.json)
- [Custom Task Info + Versioning](https://docs.microsoft.com/en-us/azure/devops/extend/develop/integrate-build-task?view=azure-devops)
- [Official repo with good examples](https://github.com/microsoft/azure-pipelines-extensions)
- [Good Docker Task Example](https://github.com/microsoft/azure-pipelines-tasks/blob/master/Tasks/DockerV2/task.json)
- [Blog on retrieving work items associated with a release](https://devblogs.microsoft.com/premier-developer/how-to-retrieve-all-work-items-associated-with-a-release-pipeline-using-azure-devops-api/)
- [Work items linked to build and release pipelines](https://docs.microsoft.com/en-us/azure/devops/boards/queries/link-work-items-support-traceability?view=azure-devops&tabs=new-web-form#work-items-linked-to-code-artifacts-and-build-and-release-pipelines)
- [Azure DevOps Node API Client](https://github.com/microsoft/azure-devops-node-api)
