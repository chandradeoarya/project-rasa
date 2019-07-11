# Rasa setup intallation guide

## Create virtual envroment in conda
$ conda create -n o activate
* extract obot.zip 
$ unzip obot.zip

$ cd obot

$ pip install - requirements.txt

$ pip install rasa

$ pip install rasa[spacy]

$ python -m spacy download en_core_web_md

$ python -m spacy link en_core_web_md en

$ pip install rasa-sdk

$ cd model

$ remove all available model

$ cd ..
$ rasa train nlu

$ rasa train core

$ rasa test

# 1.To deploy rasa model in slack bot download ngrok and replace it with your file with authenticate token
## 2. goto https://api.slack.com and 

a.build app -> Name your bot ->select work station->press enter->
(This is dashboard of your bot )
b. Click on bots ->Add bot User->Add Display name & Default Name->make it always online->Add bot User

c. From left navigaton bar click OAuth & Permission ->copy User bot authentication

 Open credential.yml and replace token with slack bot User OAuth token (token is be available in slack app dashbord)
open 4 different terminal with same directory
* terminal 1

$ rasa run actions

* get port number 5055
 switch to another terminal 2
* terminal 2

$ ./ngrok http 5055

 You will get similar url ("http://c97d4831.ngrok.io ") with black screen copy it and replace this url in endpoint.yml file with available save file.
* terminal 3

$ rasa run

 get port number 5002 or 5005 copy it 
* Keep run server  in termina 1 and stop terminal 2 because free ngrok will not work  with two different port at time

* terminal 2 

$ ./ngrock http 5002

 copy similary url you did brfore ngrok terminal http://c97d4831.ngrok.io add ("/webhooks/slack/webhook") with url

1. open dashboard of your slack bot in left side of Features bellow you will get Event Subscription turn it on and paste this url on it
2. bellow you will get #subscribe to bot events

# click Add Bot User and subscribe 
* app_mention
* message.im

click * save change below in your webpage and enjoy chatting with slack-bot 
