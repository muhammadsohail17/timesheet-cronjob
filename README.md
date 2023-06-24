﻿# Timesheet Cronjob
A cronjob app written to fetch loggings data from Redbooth and store that into your own MongoDB database and then use that data to generate invoices. The script uses lots of node packages to make that happen. Initially now the app has been created with a web server functionality where you can perform different tasks by visiting certain routes and pass them certain parameters through query string to make them happen but the upcoming functionality will be to turn this into a cronjob based script where the data will be synced on a scheduled basis using the cronjob functionality of the script.

## Installation - Step 1

Run the following commands to install the script.

    git clone https://github.com/nicefellow1234/timesheet-cronjob.git
    cd timesheet-cronjob
    npm i

Rename `.env.sample` to `.env` and configure `MongoDB_URI` in there:

    MONGODB_URI='mongodb://127.0.0.1:27017/dbname'

## Installation - Step 2 - Create Redbooth API Console App

Next thing we need to do is create Redbooth API Console App so that we can get access to Redbooth API and be able to fetch data from within there.

Headover to Redbooth API Console at: https://redbooth.com/oauth2/applications/

If you do not have an existing app registered in there then headover to the following to create one: https://redbooth.com/oauth2/applications/new

![Register New Redbooth API App](https://github.com/nicefellow1234/timesheet-cronjob/assets/10282608/c50286eb-3b1b-4fff-ac41-19340b7587f8)

If you already have an existing app registered in there then modify the `Return URI` to match up with our own one in `.env` i.e. **RB_REDIRECT_URI**. Keep in mind that this `Return Uri` is only for local installation, if you have deployed the script in a live server then you will need to match up with your deployed app URL.

![Created Redbooth API App](https://github.com/nicefellow1234/timesheet-cronjob/assets/10282608/f3b3283f-5ef1-40d2-a250-e14e787a7202)

Once you create your Redbooth API Console app so get your `Client ID` & `Client Secret` from in there and update them in your `.env` file according next to `RB_CLIENT_ID` & `RB_CLIENT_SECRET`.

    RB_CLIENT_ID='RB_CLIENT_ID'
    RB_CLIENT_SECRET='RB_CLIENT_SECRET'
    RB_REDIRECT_URI='http://localhost:3000/authorize'

Once you do that then now it's time to fire up the app and authenticate redbooth to start fetching the data to populate our database. 

Execute the following command to start the app:

    node app.js

## Installation - Step 3 - Authenticate Redbooth (Get Access Token from Redbooth)

Now Headover to Redbooth API Console at: https://redbooth.com/oauth2/applications/

Open your Redbooth API Console App by clicking on `Show` button next to the app. Next click on `Authorize` button to authenticate the app and get access token.

![image](https://github.com/nicefellow1234/timesheet-cronjob/assets/10282608/160b8800-dfc6-4732-8959-551bcef82f1a)


Once you click on `Authorize` button you will be forwarded to the `Return URI` for further processing.

![image](https://github.com/nicefellow1234/timesheet-cronjob/assets/10282608/d10ed045-10f1-4521-b036-feb08e00b1a9)

We have completed the installation now we can move ahead to start populating the database by fetching data from redbooth.
