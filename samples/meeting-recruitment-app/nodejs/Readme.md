---
page_type: sample
description: "This sample illustrates a meeting experience for recruitment scenario using Apps In Meetings. This app also uses bot for sending notifications."
products:
- office-teams
- office
- office-365
languages:
- nodejs
- javascript
extensions:
  contentType: samples
  createdDate: "10/01/2021 02:36:57 PM"
urlFragment: officedev-microsoft-teams-samples-meeting-recruitment-app-nodejs
---

# Recruitment App Sample using Apps in Meetings

This sample illustrates a meeting experience for recruitment.

It has meeting details and in-meeting app that helps in the interview process.

## Interact with app

![Details](Images/meetingrecruitment.gif)

## Try it yourself - experience the App in your Microsoft Teams client
Please find below demo manifest which is deployed on Microsoft Azure and you can try it yourself by uploading the app package (.zip file link below) to your teams and/or as a personal app. (Sideloading must be enabled for your tenant, [see steps here](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)).

**Recruitment App Sample:** [Manifest](/samples/meeting-recruitment-app/csharp/demo-manifest/Meeting-Recruitment-App.zip)

## Prerequisites

- [NodeJS](https://nodejs.org/en/) must be installed on your development machine (version 16.14.2  or higher).
- [ngrok](https://ngrok.com/download) or equivalent tunnelling solution
- [Teams](https://teams.microsoft.com) Microsoft Teams is installed and you have an account

## Setup

 1. Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal. 
  
         Go to App registrations and create a new app registration in a different tab.
      Register an application.
      Fill out name and select third option for supported account type and click "Register".

      ![AppRegistration](Images/AppRegistration.png)

      * Copy and paste the App Id and Tenant ID somewhere safe. You will need it in a future step.

      - Create Client Secret.
         * Navigate to the "Certificates & secrets" blade and add a client secret by clicking "New Client Secret".

      ![ClientSecret](Images/clientsecret.png) 

      * Copy and paste the secret somewhere safe. You will need it in a future step.

 
 2. Setup for Bot
    - In Azure portal, create a [Azure Bot resource](https://docs.microsoft.com/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp%2Caadv2).
    - Ensure that you've [enabled the Teams Channel](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0)
    - While registering the bot, use `https://<your_ngrok_url>/api/messages` as the messaging endpoint.
    **NOTE:** When you create app registration, you will create an App ID and App password - make sure you keep these for later.
    
 3. Create a Azure Storage account(This is needed to store/retrieve data that's used in the app) 
  [Create storage account](https://docs.microsoft.com/azure/storage/common/storage-account-create?tabs=azure-portal)

   This step will create a storage account. You will require storage account name and keys in next steps.
  
   Please follow [View account keys](https://docs.microsoft.com/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys) to see the   
   keys info.

4. Setup NGROK
   - Run ngrok - point to port 3978

    ```bash
    ngrok http -host-header=rewrite 3978
    ```
5. Setup for code

  - Clone the repository

    ```bash
    git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
    ```
   
   -Modify the `keys.js` file in the location `samples/meeting-app/nodejs/api/server` and fill in the `[STORAGE ACCOUNT NAME]` and `[ACCESS KEY]` for azure table storage.
 

  - We have two different solutions to run so follow below steps:
 
    A) In a terminal, navigate to `samples/meeting-recruitment-app/nodejs/api`

    B) In a different terminal, navigate to `samples/meeting-recruitment-app/nodejs/clientapp`

     * In both the terminal run 
   
       npm install

       npm start

6. Setup Manifest for Teams
- __*This step is specific to Teams.*__
    - **Edit** the `manifest.json` contained in the ./AppPackage folder to replace your Microsoft App Id (that was created when you registered your app registration earlier) *everywhere* you see the place holder string `<<APP-ID>>` (depending on the scenario the Microsoft App Id may occur multiple times in the `manifest.json`)
    - **Edit** the `manifest.json` for `<<BASE-URL>>` and replace `<<BASE-URL>>` with base Url of your domain. E.g. if you are using ngrok it would be `https://1234.ngrok.io` then your domain-name will be `1234.ngrok.io`.
    - **Zip** up the contents of the `AppPackage` folder to create a `manifest.zip` (Make sure that zip file does not contains any subfolder otherwise you will get error while uploading your .zip package)    
    
- Upload the manifest.zip to Teams (in the Apps view click "Upload a custom app")
   - Go to Microsoft Teams. From the lower left corner, select Apps
   - From the lower left corner, choose Upload a custom App
   - Go to your project directory, the ./AppPackage folder, select the zip folder, and choose Open.
   - Select Add in the pop-up dialog box. Your app is uploaded to Teams.

**Note**: If you are facing any issue in your app, please uncomment [this](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/meeting-recruitment-app/nodejs/api/server/index.js#L55) line and put your debugger for local debug.

## Running the sample

1) Details page:
   The details page shows basic information of the candidate, timeline, Questions (that can be added for meeting), Notes (provided by peers)

   ![Details](Images/details.png)

2) Action on Questions:
   
   - The interviewer can Add/Edit or Delete question.

   ![Add Question](Images/add_question.png)

   - Add Questions Task Module
   
   ![Add Question Task](Images/add_task.png)

   ![Edit Delete Question](Images/edit_questions.png)

   - Edit Question Task Module
   
   ![Edit Task](Images/edit_task.png)

3) Add Notes:
   
   The interviewer can add notes that will appear to other peers.

   ![Add Notes](Images/add_note.png)

   Add Note Task Module
  
   ![Add Notes](Images/add_note_task.png)

4) Sidepanel:
    
    The in-meeting side panel shows two sections as follows:
    
    A) Overview: Shows the basic details of the candidate.
    
    B) Questions: The questions set in the details page appear here. The interviewer can use this to provide rating and submit final feedback.

    ![Sidepanel Overview](Images/sidepanel_overview.png)

    ![Sidepanel Questions](Images/sidepanel_questions.png)

5) Share assets:

   This is used to share assets to the candidate.
   
   ![Share Assets](Images/share_assets.png)

6) Mobile view: Details tab

   ![Details tab](Images/details_tab_mobile.png)

   ![Note](Images/Note_mobile.png)

   ![Share Doc](Images/ShareDoc_mobile.png)
   
   - Sidepanel view
   
   ![Sidepanel Overview mobile](Images/sidepanel_mobile.png)

   ![Sidepanel Question mobile](Images/question_mobile.png)


## Further reading

- [Meeting apps APIs](https://learn.microsoft.com/microsoftteams/platform/apps-in-teams-meetings/meeting-apps-apis?tabs=dotnet)
- [Install the App in Teams Meeting](https://docs.microsoft.com/microsoftteams/platform/apps-in-teams-meetings/teams-apps-in-meetings?view=msteams-client-js-latest#meeting-lifecycle-scenarios)