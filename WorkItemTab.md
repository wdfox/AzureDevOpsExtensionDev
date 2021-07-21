## Work Item Tab

In Azure Boards, the Work Item Form can be extended in a variety of ways (see some examples [here](https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-workitem-extension?view=azure-devops)). These views are essentially custom code running inside of an iFrame. This section is specific to adding an entirely new tab to the Work Item Form, but the same principles apply to other modifications as well.

Though new work item tabs can be created using plain HTML+Javascript, the most flexible route is to create a React application using some helpful libraries developed by the Azure DevOps team. The most critical of these libraries is the [azure-devops-extension-sdk](https://github.com/Microsoft/azure-devops-extension-sdk). This SDK is required for initializing your React app inside the iFrame, saving and retrieving state, and getting context about the user, organization, board, and work item. Follow the instructions from the GitHub repo to understand how to initialize the SDK.

Documentation on storing and retrieving state is more difficult to find, but several samples contain useful code. For example, in [this repository](https://github.com/microsoft/azure-devops-extension-sample) we can look into the Hub's [Extension Data Tab](https://github.com/microsoft/azure-devops-extension-sample/blob/master/src/Samples/Hub/ExtensionDataTab.tsx) for an idea. In this file, we can see the initialization of a `_dataManager` inside the `initializeState` method. This data manager then has methods to set or retrieve values and documents from the Azure DevOps state store. 

In addition to the SDK, Azure DevOps also has some prebuilt React components and predetermined styles available that can help match your extension's experience with the native UI. For components and sample usage, check out [this page](https://developer.microsoft.com/en-us/azure-devops/components), and for styling and development info see [here](https://developer.microsoft.com/en-us/azure-devops/develop/extensions) and [here](https://developer.microsoft.com/en-us/azure-devops/develop/styles). 

### Useful Links
- [Repo with web (html+js) examples](https://github.com/microsoft/azure-devops-extension-sample)
- [Microsoft Docs Tab example](https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-workitem-extension?view=azure-devops#add-a-page)
- [Azure DevOps UI React Components](https://developer.microsoft.com/en-us/azure-devops/components)
