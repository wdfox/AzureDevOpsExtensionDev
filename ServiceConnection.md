## Service Connection
Service connections provide a secure way to make authenticated calls to external backends from Azure DevOps. You may require a custom service connection if your extension will be sending calls to an API that does not allow anonymous access. A user will create the service connection and all future calls to that backend will include a token, password, or OAuth flow.

For a basic example, see step-by-step instructions [here](https://docs.microsoft.com/en-us/azure/devops/extend/develop/service-endpoints?view=azure-devops&viewFallbackFrom=vsts). 

You also have the ability to customize various aspects of service connection creation and operation. You can view more detailed documentation about those capabilities [here](https://github.com/Microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/serviceEndpoints.md). As a part of this customization, you have the option to choose one of several authentication schemes including basic, token-based, OAuth2, and others. To see the options in more detail, visit the documentation [here](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/authenticationSchemes.md).

'Data sources' is one other critical attribute of the service connection. A data source points to an external endpoint which the service connection can make authenticated calls to. This is applicable in two important scenarios:

1. If you want to prevent a user from saving a service connection with incorrect information (incomplete token, wrong password, etc.), you can add a 'verification' step to the service connection creation. This verification involved a call to an external endpoint which validates the authentication info provided by the user. To make this call, we add the validation endpoint as a 'data source' called `TestConnection`. See instructions [here](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/dataSources.md#test-service-endpoint) for more information. 
2.  If your extension includes an Azure Pipelines task, you can use data sources (in the service connection) and data source bindings (in the task definition) to populate the input dropdowns for your tasks. See more detailed instructions [here](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/dataSources.md) (data sources) and [here](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/dataSources.md#defining-url-inline-within-datasourcebinding) (data source bindings). In short, data sources indicate where to retrieve the data while data source bindings indicate how the UI should display that data as task inputs. 

### Useful Links
- [Step-by-step example](https://docs.microsoft.com/en-us/azure/devops/extend/develop/service-endpoints?view=azure-devops&viewFallbackFrom=vsts)
- [Detailed docs with specific instructions](https://github.com/Microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/serviceEndpoints.md)
- [Authentication scheme details](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/authenticationSchemes.md)
- [Data sources details](https://github.com/microsoft/azure-pipelines-extensions/blob/master/docs/authoring/endpoints/dataSources.md)
