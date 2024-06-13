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
