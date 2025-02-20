# Notion Synchronise with Google Calendar

Do you find yourself juggling between Notion and Google Calendar to manage your events? Fret not! This awesome code is here to save your day. It magically extracts event details from your Notion Dashboard and seamlessly integrates them into your Google Calendar events. But wait, there's more! It even adds a handy URL to your GCal event, so you can effortlessly jump back to the specific Notion Page related to the event. How cool is that?

**Warning**: Proceed with caution! This repo wields the power to make changes to your Notion database and Google Calendar. So, if you're not confident about what you're doing, buckle up and brace yourself for some unexpected surprises.

## What you will need to get started

- google account
- Notion account
- github account (optional)
- python3 (or Docker)

## Current Capabilities:

- update events from google cal to notion
- update events from notion to google cal

### Functions:

- Ability to change timezones by changing `timecode` and `timezone` in `notion_setting`
- Ability to change the date range by changing `goback_days` and `goforward_days` in `notion_setting.json` (If you are a new IT guy here, please use 1 and 2 days respectively before you understand the code)
- Able to decide the default length of new GCal events by changing `event_length` in `notion_setting.json`
- Option to delete gCal events if checked off as `Done?` column in Notion
- Sync across _multiple calendars_ and choose which calendar you would like to sync by changing `gcal_dic` and `gcal_dic_key_to_value` in `notion_setting.json`
- Able to name the required Notion columns whatever you want and have the code work by changing `page_property` in `notion_setting.json`
- credential and OAuth consent screen with google calendar scope

Inspired by [akarri2001](https://github.com/akarri2001/Notion-and-Google-Calendar-2-Way-Sync)

## How to install it

- Step1: Fork or Clone git repository

  For beginners, you can download this repository directly.

  1. Click the green `Code` button on the top-right corner of the page, and then click `Download ZIP`

     <img src="./assets/download.png" width="600" height="auto">

     You can unzip it and then change the folder name to whatever you want. Have a look these files and folders. We will change some of them later.

     <img src="./assets/folder.png" width="600" height="auto">

     <video src="./assets/NotionStep1.mp4" width="600" height="auto" controls="controls"></video>

  For advanced users, you can fork this repository and then clone it.

  1. In the top-right corner of the page, click Fork.

    <img src="./assets/fork.png" width="600" height="auto">

  2. Select an owner for the forked repository.

  3. Choose the main branch

  4. Click `Create Fork`.

  5. Clone your forked repository

    <img src="./assets/code.png" width="600" height="auto">

  6. Open the terminal, and type:

  ```bash
  git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME
  ```

  7. Change directory to where you download, and then install packages

  ```bash
  cd YOUR-REPOSITORY-NAME
  pip3 install -r requirements.txt
  ```

  If you update the requirements.txt, you can use the following commend to update it.

  ```bash
  pip3 freeze > requirements.txt
  ```

- Step2: Duplicate the Notion template as the initial database [NotionGCal](https://huixin.notion.site/aa639e48cfee4216976756f33cf57c8e?v=6db9353f3bc54029807c539ffc3dfdb4)
  If you are familar with the entire code, you are welcome to customise your own template. However, I recommend you to use my template and do not change the property names at the first time.

  <video src="./assets/NotionStep2.mp4" width="600" height="auto" controls="controls"></video>

- Step3: Notion Connection Setting

  1. Visit Notion Developer website

  - Directly click [Notion Developer](https://www.notion.so/my-integrations), and make sure you are logged in, or
  - Via Notion App, open your Notion and click `Settings and members`, and then click here
    <img src="./assets/connection.png" width="600" height="auto">

  2. Create `New integration` and then `Submit`
     <img src="./assets/newintegration.png" width="600" height="auto">

  3. Open the template page, click `...`, then click `Add connection`. (Select what you name your connection)
     <img src="./assets/notionconnect.png" width="600" height="auto">

  <video src="./assets/NotionStep3.mp4" width="600" height="auto" controls="controls"></video>

- Step4: Complete the `notion_setting.json` in the `token_blank` folder, and then rename the folder `token_blank` with `token` (.gitignore will exclude files in this `token` folder to protect your sensitive information when you push your code to github. If you don't want to use github, you can still need to rename the folder but can ignore the reason why we do this)

  - "notion_token": "Paste your Internal Integration Token which starts with `secret*...`",
    <img src="./assets/secrets.png" width="600" height="auto">

  - "urlroot": "https://www.notion.so/{YOURNOTIONNAME}/{databaseID}?XXXXX",
    <img src="./assets/copylink.png" width="600" height="auto">

  - the following items is up to you. If you are the first time using terminal or python, I recommend you to use 1 or 2 fir "goforward_days". This mean that the code will synchromise the events from 1 day before to 2 days after today. If you are familar with python, you can change them as you want.

    - "timecode": "+08:00",
    - "timezone": "Asia/Taipei",
    - "goback_days": 1,
    - "goforward_days": 2,
    - "delete_option": 0,
    - "event_length": 60,
    - "start_time": 8,
    - "allday_option": 0,

  - Go to your google calendar page, and then click `Settings` on the top-right, next, scroll the left bar to find `Setting for my calendar`. Click it, calendar `Name` is on the top, and scroll down to find `Calendar ID`

  - Enter your default calendar at least. If you want to add multiple calendars, separate them by `,`

    - "gcal_dic": [{"YOUR CALENDAR NAME1": "YOUR CALENDAR ID1", "YOUR CALENDAR NAME2": "YOUR CALENDAR ID2"}],

    If you set up multiple calendars, it will look like this:
    <img src="./assets/multiplecal.png" width="600" height="auto">

  - The following items are column names in notion based on my template. The `page_property` section is setting these column name.

    - "Task_Notion_Name": "Task Name",
    - "Date_Notion_Name": "Date",
    - "Initiative_Notion_Name": "Initiative",
    - "ExtraInfo_Notion_Name": "Extra Info",
    - "Location_Notion_Name": "Location",
    - "On_GCal_Notion_Name": "On GCal?",
    - "NeedGCalUpdate_Notion_Name": "NeedGCalUpdate",
    - "GCalEventId_Notion_Name": "GCal Event Id",
    - "LastUpdatedTime_Notion_Name" : "Last Updated Time",
    - "Calendar_Notion_Name": "Calendar",
    - "Current_Calendar_Id_Notion_Name": "Current Calendar Id",
    - "Delete_Notion_Name": "Done?",
    - "Status_Notion_Name": "Status",
    - "Page_ID_Notion_Name": "PageID",
    - "CompleteIcon_Notion_Name": "CompleteIcon"
      You can change the column name without modifying the main code zone as long as you alter this section and notion columns consistently.

    <video src="./assets/NotionStep4.mp4" width="600" height="auto" controls="controls"></video>

- Step5: Create a google token, and make sure your scope include google calendar

  1. Go to [google developers](https://console.developers.google.com/)

  2. Create a New Project, and select it
     <img src="./assets/library.png" width="600" height="auto">
     <img src="./assets/newproject.png" width="600" height="auto">
     <img src="./assets/selectproject.png" width="600" height="auto">

  3. Clikc `+ ENABLE APIS AND SERVICES` to enable google calendar API, and then add your email
     <img src="./assets/library.png" width="600" height="auto">
     <img src="./assets/searchapi.png" width="600" height="auto">

  4. You enabled google calendar API successfully if you see this
     <img src="./assets/enabled.png" width="600" height="auto">

  5. Click `+ CREATE CREDENTIALS`
     <img src="./assets/OAuthID.png" width="600" height="auto">

  6. Click `CONFIGURE CONSENT SCREEN`, and then select `External` and click `CREATE`

  7. Name whatever you want, and select your email as `User support email`. Next, type your email to `Developer contact information`, and then click `SAVE & CONTINUE`

  8. Click `ADD OR REMOVE SCOPES`, and then Select the scope as belows. Scroll down and click `UPDATE`
     <img src="./assets/addscope.png" width="600" height="auto">
     <img src="./assets/searchscope.png" width="600" height="auto">
     <img src="./assets/googleapi.png" width="600" height="auto">

  9. Scroll down, and click `Save and Continue`

  10. Click `+ ADD USERS` and click `Save and Continue`
      <img src="./assets/adduser.png" width="600" height="auto">

  11. Create the OAuth client ID
      <img src="./assets/createcredential.png" width="600" height="auto">

  12. Name your application, and then click `CREATE`
      <img src="./assets/credentialname.png" width="600" height="auto">

  13. Download `.json` (Note: Dont show with others otherwise they may access your account)
      <img src="./assets/credentialdownload.png" width="600" height="auto">

  14. Rename `client_secret_XXXXXXXXXXXX.json` to `client_secret.json`, and then move it into `token` folder

  <video src="./assets/NotionStep5.mp4" width="600" height="auto" controls="controls"></video>

- Step6: Download [python](https://www.python.org/downloads/) (or skip this step if you use Docker)

  1. Visit the official Python website at https://www.python.org/downloads/.

  2. On the Downloads page, you will see the latest version of Python available for download. The website will automatically detect your operating system and suggest the appropriate version for your platform (Windows, macOS, or Linux). If you want to download a different version, click on the "Looking for a specific release?" link.

  3. Click on the download link for the version of Python you want to install. You will typically have two options: one for the latest stable release (e.g., Python 3.x.x) and one for the latest legacy release (e.g., Python 2.7.x). It is recommended to choose the latest stable release unless you have specific requirements for using Python 2.

  4. After clicking the download link, you will be redirected to the download page. Scroll down to find the files for your operating system. Choose the installer appropriate for your system architecture (32-bit or 64-bit).

  5. Once the installer is downloaded, run the installer executable (.exe file on Windows or .pkg file on macOS) by double-clicking on it.

  6. Follow the installation instructions provided by the installer. You can usually accept the default settings unless you have specific requirements. Make sure to check the box that says "Add Python to PATH" during the installation process, as this will make it easier to use Python from the command line.

  7. After the installation is complete, open a new command prompt (Windows) or terminal (macOS/Linux)

  <img src="./assets/terminal.png" width="600" height="auto">

  8. type python --version to verify that Python is installed correctly. You should see the version number of Python displayed.

  <img src="./assets/pythonversion.png" width="600" height="auto">

  9. Install python packages

  ```bash
  pip3 install -r requirements.txt
  ```

  There are a lot of videos on youtube to teach you how to install python. I recommend you to watch them if you are not familar with python.

- Step7: If you are familar with Docker, you can use Docker instaed of python to run this code.

  - Warning: if you use docker, change "docker": true, in `notion_setting.json`. Otherwise, the creds will not work when you activated it at the first time.

  1. download [Docker](https://www.docker.com/products/docker-desktop).

  2. open the terminal and type:

  ```bash
  docker build -t sync .
  ```

  3. Third, type to run default script:

  ```bash
  docker run -it sync
  ```

  or add the following commend to update from google calendar time only. You can check the commend in `main.py` or the following Sychronise Notion with Google Calendar section.

  ```bash
  docker run -it sync src/main.py -gt
  ```

  - At the first time, you need to copy the creds from brower to terminal. And copy the code and paste it into the `token.pkl` in token folder. Run the above code again, and then you can use docker to run the code.

  - clear all Docker containers after you finish it.

  ```bash
  docker rm $(docker ps -aq)
  ```

  4. Other commend to check the container. You can start the docker container and then run the code in the container.

  ```bash
  docker ps -a
  ```

  ```bash
  docker start <CONTAINER ID>
  ```

  ```bash
  docker exec -it <CONTAINER ID> sh
  ```

  You are in docker container
  ```docker
  # python src/main.py
  ```

  Exit docker container
  ```docker
  exit
  ```

  Stop docker container
  ```docker
  docker stop <CONTAINER ID>
  ```

  Clear all Docker containers
  ```docker
  docker rm $(docker ps -aq)
  ```

Congraduations! All settings are done! Let's run the program.

# Sychronise Notion with Google Calendar

Go to the terminal, and change the folder to where these script are.:

```bash
cd src
```

Run the code to activate the connection between Notion and Google Calendar:

```bash
python3 main.py
```

At the first time, the page will be redirected to `Choose an account` page, and then click or log in your account. Just click `Continue`, and then `Continue`. Finally, close the authentication window. Go back to the terminal, you will see:

  <img src="./assets/refresh.png" width="600" height="auto">

All commends and its comment in main.py are in `main.py`. You can change them as you want. I will explain most of them.

  <img src="./assets/main.png" width="600" height="auto">

- Update from notion event needed to updated to google calendar (default)

  ```bash
  python3 main.py
  ```

  You will see the following message if you successfully connect to your google calendar. Type enter to continue and the code will start to run. If you do not want it run, type `Ctrl + C` to stop it.

  <img src="./assets/success.png" width="600" height="auto">

  If you hit enter, you will see the following message. It means that the code is running. You can check your google calendar to see if it works.

  <img src="./assets/running.png" width="600" height="auto">

- Update from all notion tasks to google calendar

  ```bash
  python3 main.py -na
  ```

- Update from google time which is in Notion, and create google new events which is not in Notion

  ```bash
  python3 main.py -gt
  ```

- Create google new events only

  ```bash
  python3 main.py -gc
  ```

- Replace all content of google event
  (I don't recommend using this function since my most contents are made by Notion tasks. However, it is still needed sometimes such as downloading events into notion at the first time)

  ```bash
  python3 main.py -ga
  ```

- Delete google events which is ticked in Notion

  ```bash
  python3 main.py -r
  ```

## Test

Change the folder to where these script are:

```bash
cd tests
```

### Test Notion Connection

Run specific test file:

```bash
python3 test_notion_setting.py
```

With unittest, you can use the -m flag and specify the test directory to run all test files in that directory. For example, if your test files are located in a folder named tests, you can run the following command:

```bash
python3 -m unittest discover -s .
```

### Test Google Calendar Connection

To be continued...

## Prettier

You can use prettier to format your code. It is a good tool to make your code more readable. In this `.prettierrc` configuration, we use the "overrides" key to specify formatting rules for different file types.

Note: Prettier is primarily designed for formatting JavaScript, TypeScript, CSS, and other web-related languages. It does not have built-in support for formatting Python code.

Install Prettier

```bash
npm install -g prettier
```

```bash
prettier -w .
```

## Black

Black is a Python code formatter. It is a good tool to make your code more readable.

```bash
black .
```
