# Azure Services

- [Static Web Apps](#static-web-apps)
    - [Deployment using the Visual Studio Code extension](#deploy-an-application-using-the-visual-studio-code-extension)
    - [Deployment with Azure portal and Azure DevOps](#deploy-an-application-with-azure-portal-and-azure-devops)
    - [Deployment with SWA CLI](#deploy-an-application-with-swa-cli)
- [Function App](#function-app)
    - [Deployment using the Visual Code extension](#deploy-a-function-through-the-visual-studio-code-extension)
- [Container Registry](#container-registry)
    - [Configure Function App to work with Container Registry](#configure-function-app-to-work-with-container-registry)


## Static Web Apps

### [Deploy an application using the Visual Studio Code extension](https://learn.microsoft.com/en-us/azure/static-web-apps/getting-started?tabs=vanilla-javascript)

#### GitHub

1. Create a repository on GitHub
    - The repository you create in this step should include at least a single *index.html* file
2. Clone the repository
    - Replace ```<YOUR_GITHUB_ACCOUNT_NAME>``` with your GitHub username
```sh
git clone https://github.com/<YOUR_GITHUB_ACCOUNT_NAME>/my-first-static-web-app.git
```

#### Visual Studio Code

##### Install Azure Static Web Apps extension

1. Select View > Extensions
2. In the Search Extensions in Marketplace, type ```Azure Static Web Apps```
3. Select Install for Azure Static Web Apps

##### Create a static web app

1. Inside Visual Studio Code, select the Azure logo in the Activity Bar to open the Azure extensions window
![Azure extension icon](notes_images/SWA_1.png)
    - If you are not already authenticated in Azure and GitHub, the extension prompts you to sign in to both services during the creation process
2. Press the F1 key to open the Visual Studio Code command palette
3. Enter ```Create static web app``` in the command box
4. Select ```Azure Static Web Apps: Create static web app...```
5. Select your Azure subscription
6. Enter your application name
7. Choose a region nearest to the client
8. Enter the settings values that match your application:

Setting | Value
-|-
Framework | Select **Custom**
Location of application code | Enter ```\```
Build location | Leave blank

### [Deploy an application with Azure portal and Azure DevOps](https://learn.microsoft.com/en-us/azure/static-web-apps/get-started-portal?pivots=azure-devops&tabs=vanilla-javascript)

1. In the Azure portal, search for and create a new static web app
2. During the creation process, select "Azure DevOps" as the deployment source and select the DevOps repository and branch that contains the app
3. Select "Custom" for Build Presets, "/" for the App location, leave API location and Output location blank
4. Click the "Next: Advanced >" button, and then select the region closest to the client
5. Click the Review + create button and after passing the validation click the Create button

### [Deploy an application with SWA CLI](https://edi.wang/post/2022/11/17/deploy-to-azure-static-web-app-from-local-machine-without-github-action)

1. Initialization
```sh
swa init
```
2. Deployment
    - replace ./build with the directory of where you keep the build files
```sh
swa deploy ./build --env production
```


## Function App

### [Deploy a function through the Visual Studio Code Extension](https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-python)

#### Azure Functions Core Tools

1. Press the F1 key to open the command palette
2. Search for and select ```Azure Functions: Install or Update Core Tools```

#### Local

1. Choose the Azure icon in the Activity Bar and then in the **Workspace (local)** area, select the + button, choose **Create Function** in the dropdown
    - When prompted, choose **Create new project**
![Azure extension icon and plus button from workspace local are emphasized with red borders](notes_images/FA_1.png)
2. Choose the directory location for your project workspace and choose **Select**
    - You should either create a new folder or choose an empty folder for the project workspace
    - Don't choose a project folder that is already part of a workspace
3. Provide the following information at the prompts:

Prompt | Selection
-|-
Select a language | Choose ```Python (Programming Model V2)```
Select a Python interpreter to create a virtual environment | Choose your preferred Python interpreter (If an option isn't shown, type in the full path to your Python binary)
Select a template for your project's first function | Choose ```HTTP trigger```
Name of the function you want to create | Enter a name for your function
Authorization level | Choose ```ANONYMOUS```, which lets anyone call your function endpoint
Select how you would like to open your project | Choose ```Open in current window```

4. Open the local.settings.json project file and verify that the ```AzureWebJobsFeatureFlags``` setting has a value of ```EnableWorkerIndexing```
5. In the local.settings.json file, update the ```AzureWebJobsStorage``` setting as in the following example
```JSON
"AzureWebJobsStorage": "UseDevelopmentStorage=true"
```

#### Start the Emulator

1. In Visual Studio Code, press the F1 key to open the command palette. In the command palette, search for and select ```Azurite: Start```
2. Check the bottom bar and verify that Azurite emulation services are running, and if so, you can now run your function locally

#### Run the function locally

1. To start the function locally, press the F5 key or the Run and Debug icon in the left-hand side Activity bar
2. With the Terminal panel focused, press Ctrl + C to stop Core Tools and disconnect the debugger

#### Deployment

1. If you aren't already signed in, choose the Azure icon in the Activity bar, and then in the Resources area, choose **Sign in to Azure...**
![Azure extension icon and sign in to Azure from resources remote are emphasized with red borders](notes_images/FA_2.png)
2. Choose the Azure icon in the activity bar, and then in the **Resources** area, select the + icon and choose the **Create Function App in Azure** option
3. Provide the following information at the prompts:

Prompt | Selection
-|-
Select subscription | Choose the subscription to use, you won't see this prompt when you have only one subscription visible under **Resources**
Enter a globally unique name for the function app | Type a name that is valid in a URL path, the name you type is validated to make sure that it's unique in Azure Functions
Select a runtime stack | Choose the language version on which you've been running locally
Select a location for new resources | Choose a region nearest to the client

4. Go to the Azure portal and open your Azure Storage Account, select Access keys, and click on Show
![Access keys and show button from Azure portal are emphasized with red borders](notes_images/FA_3.png)
5. In the Azure portal, open your Function App, select Environment variables, select AzureWebJobsStorage, enter the connection string in the Value input field, and click on Apply
![Environment variables, AzureWebJobsStorage, value, and apply button from Azure portal are emphasized with red borders](notes_images/FA_4.png)
6. In the **Resources** area of the Azure activity, locate the function app resource, right-click the resource, and select **Deploy to function app...**
![Location of deploy to function app](notes_images/FA_5.png)
7. When prompted about overwriting previous deployments, select **Deploy** to deploy your function code to the new function app resource
