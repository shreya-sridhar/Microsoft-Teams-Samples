---
page_type: sample
description: This sample shows the contents of meeting tab context object in a meeting tab and using bot's meeting API, meeting participant details and meeting details are sent to user.
products:
- office-teams
- office
- office-365
languages:
- nodejs
extensions:
 contentType: samples
 createdDate: "01/07/2022 05:00:25 PM"
urlFragment: officedev-microsoft-teams-samples-meetings-context-app-nodejs

---

# Teams Meeting Context Sample Node.js

This sample shows the contents of meeting tab context object in a meeting tab and shows the output of Meeting's API `TeamsInfo.getMeetingParticipant` and `TeamsInfo.getMeetingInfo` using bot commands.

- **Interaction with bot**
![meeting-context](Images/meeting-context.gif)

## Try it yourself - experience the App in your Microsoft Teams client
Please find below demo manifest which is deployed on Microsoft Azure and you can try it yourself by uploading the app package (.zip file link below) to your teams and/or as a personal app. (Sideloading must be enabled for your tenant, [see steps here](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)).

**Teams Meeting Context Sample:** [Manifest](/samples/meetings-context-app/csharp/demo-manifest/meetings-context-app.zip)

## Prerequisites

- [NodeJS](https://nodejs.org/en/)
- [ngrok](https://ngrok.com/) or equivalent tunnelling solution

### Setup 
> Note these instructions are for running the sample on your local machine.

1) Run ngrok - point to port 3978

    ```bash
    ngrok http -host-header=rewrite 3978
    ```

2) Setup for Bot

Register your application with Azure AD

- Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.
- On the overview page, copy and save the **Application (client) ID, Directory (tenant) ID**. You’ll need those later when updating your Teams application manifest and in the appsettings.json.
- Navigate to the **Certificates & secrets**. In the Client secrets section, click on "+ New client secret". Add a description (Name of the secret) for the secret and select “Never” for Expires. Click "Add". Once the client secret is created, copy its value, it need to be placed in the .env file.

- In Azure portal, create a [Azure Bot resource](https://docs.microsoft.com/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp%2Caadv2).

- Ensure that you've [enabled the Teams Channel](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0)

3) Clone the repository

    ```bash
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```

   A) If you are using Visual Studio Code

    - Launch Visual Studio code
    - File -> Open Folder
    - Navigate to `samples/meeting-context-app` folder
    - Select `nodejs` folder

   B) Install node modules For Server

   Inside node js folder, open your local terminal and run the below command to install node modules. You can do the same in Visual Studio code terminal by opening the project in Visual Studio code.

    ```bash
    npm install
    ```

   C) Install node modules For Client

   Navigate to folder `client` folder, open your local terminal and run the below command to install node modules. You can do the same in Visual Studio code terminal by opening the project in Visual Studio code.

    ```bash
    npm install
    ```


4) Update the `.env` configuration file.

   Update configuration with the ```MicrosoftAppId```,  ```MicrosoftAppPassword``` and ```MicrosoftAppTenantId```.

6) Run your app for server and client

    ```bash
    npm start
    ```

    - Your server will start running on 3000 PORT
    - Your client will start running on 3978 PORT.

7) __*This step is specific to Teams.*__
    - **Edit** the `manifest.json` contained in the  `TeamsAppManifest` folder to replace your Microsoft App Id (that was created when you registered your bot earlier) *everywhere* you see the place holder string `<<YOUR-MICROSOFT-APP-ID>>` (depending on the scenario the Microsoft App Id may occur multiple times in the `manifest.json`)
    - **Edit** the `manifest.json` for `validDomains` with base Url domain. E.g. if you are using ngrok it would be `https://1234.ngrok.io` then your domain-name will be `1234.ngrok.io`.
    - **Zip** up the contents of the `TeamsAppManifest` folder to create a `manifest.zip` (Make sure that zip file does not contains any subfolder otherwise you will get error while uploading your .zip package)
    - **Upload** the `manifest.zip` to Teams (In Teams Apps/Manage your apps click "Upload an app". Browse to and Open the .zip file. At the next dialog, click the Add button.)
    - Add the app to personal/team/groupChat scope (Supported scopes)
     

## Running the sample

- Add the app in meeting/group channel.
- The details of the meeting context object will be shown on tab based.
![participant context](Images/Setup-Tab-Bot.png)

- You can expand/reduce the JSON for the context object and can also copy a particular object slice.
- You can send one of these two commands: **Meeting Context** or **Participant Context**
- It will send you the output of `TeamsInfo.getMeetingInfo` and `TeamsInfo.getMeetingParticipant`

1. **Particpant Details :** User can see the details of current participant by the name id and other feilds respectively.
![participant context](Images/Participant-Details.png)

2. **Meeting Details :** In this user can track the detials of meeting start time, end time, joining url and other details respectively.
![meeting context](Images/Meeting-Details.png) 

**Note**: If you are facing any issue in your app, please uncomment [this](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meetings-context-app/nodejs/server/index.js#L44) line and put your debugger for local debug.

## Further reading

- [Tab Basics](https://docs.microsoft.com/microsoftteams/platform/tabs/how-to/create-channel-group-tab?pivots=node-java-script)
- [Azure Portal](https://portal.azure.com)
- [Get-context-for-tabs](https://docs.microsoft.com/microsoftteams/platform/tabs/how-to/access-teams-context#retrieve-context-in-private-channels)
- [Meeting API reference](https://docs.microsoft.com/microsoftteams/platform/apps-in-teams-meetings/api-references?tabs=dotnet)