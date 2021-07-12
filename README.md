# Welcome to ahl-teams!
This is the source code for my submission to the Microsoft Engage 2021 program. 

I've built a web app on Django - deployed on Heroku - as a prototype Teams clone. Development has been in line with Agile and Scrum principles. 

You can find the video demonstration on [YouTube](https://youtu.be/1NOJ5IAnoS8).
You can visit the web app [here](https://ahl-teams.herokuapp.com).

My web app implements:
1. The required minimum functionality of two-person video call
2. The required "adopt" two-person chat feature
3. A two-person voice call feature. 
4. Authorization with your Microsoft account, just like in Teams. This is implemented with the Azure Active Directory and the Microsoft Graph API. 
5. Access to your account Calendar. You can view old events and add new ones. 
Voice call, video call and chat features are implemented with WebRTC and PeerJS.


## How is this Agile?
Each feature was planned and ordered by priority during the design phase, and assigned to its respective sprint backlog. Over the month of the mentorship, I've fit in all the pieces together, in spirit with Agile. 

I spent exactly a week - with my mentors' encouragement - in the design phase. I came up with the product backlog, with a list of all the features I wanted to see (along with the adopt feature) and how they'd all fit together. Then I divided it all into three sprint backlogs, each a week long. 

The first sprint I developed the two-person video call feature. The next sprint I worked on the Graph API features - authorization and calendar. Finally in the last sprint, as part of the adopt phase, I implemented the chat feature. I spent the final couple of days improving UI and focusing on deployment configuration. 

Throughout, I've found my model pretty responsive to adding on new features and welcoming change. At the end of each sprint, I had a fully functional model ready to deliver.

## Running the source code locally
[All steps here are for Windows.]
1. Download the source code.
2. From your CLI, start a new shell: `pipenv shell`
3. Install all required dependencies from requirements.txt: `pipenv install -r requirements.txt`

To enable Microsoft OAuth, do the following:
1. Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com/). Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.
5. Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.
6. Select  **New registration**. On the  **Register an application**  page, set the values as follows.

-   Set  **Name**  to  `ahl-teams demo`.
-   Set  **Supported account types**  to  **Accounts in any organizational directory and personal Microsoft accounts**.
-   Under  **Redirect URI**, set the first drop-down to  `Web`  and set the value to  `http://localhost:8000/callback`. This is to run the app locally. You can change this according to your deployment preferences.

4. Select **Register**. On the **ahl-teams demo** page, copy the value of the **Application (client) ID** and save it. This will be needed in the next step.
5. Select **Certificates & secrets** under **Manage**. Select the **New client secret** button. Enter a value in **Description** and select one of the options for **Expires** and select **Add**.
6. Copy the client secret value before leaving this page. This will be needed it in the next step.
7.   Create a new file in the root of the project named `oauth_settings.yml`, and add the following content: 
```
app_id: "YOUR_APP_ID_HERE"
app_secret: "YOUR_APP_SECRET_HERE"`
redirect: "http://localhost:8000/callback"`
scopes:`
  - user.read`
  - mailboxsettings.read`
  - calendars.readwrite`
authority: "https://login.microsoftonline.com/common"
```
8. Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal, and replace `YOUR_APP_SECRET_HERE` with the password generated.

Now run `python manage.py runserver` from your CLI. The web app should be up and running successfully!


## How to use the web app

Sign in with a Microsoft Account. You can only access the app's features once you're signed in.

Head over to **Calendar** on the navigation bar to view your old events or add a new one.

Go to **Meetings** to start a video or voice call, or chat, with online users. After you choose your meeting ID (which can be later changed) and allow access to your camera (if required), you can see the list of online users on the right of the screen.

Click on the user you'd like to talk to. This opens up a chat window. Send them a quick hello!

To video call or voice call them, click on the corresponding buttons at the top of the chat window. This takes you to a new screen and sends them an incoming call request. You can toggle video and audio on and off.

Once you're done, you can sign out by clicking on the teams logo on the top right.

Happy meets!

<br><br><br>

** *This is a cleaned repository. The original repository with all version commits is [here](https://github.com/ahlraf/teams-clone-v2)*