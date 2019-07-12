
#/----setup environmentin you system.----

*To install rasa in your system I prerfer to use anaconda
Download it from ths url below:

//------------------ANACONDA--------------------------
------------------------------------------------------
1. https://www.anaconda.com/distribution/
Select Python 3.7 version with 64bit installer

##You will get  Anaconda3-2019.03-Linux-x86_64.sh file in download directory.

i) openn terminal locate your directory to download  directory follow this commands

$ sudo apt-get update -y && sudo apt-get upgrade -y

$ bash Anaconda3-2019.03-Linux-x86_64.sh

Once at the end type 'yes' accept the Agreement and continew with Enter to install default directory 
again answer "yes" for PATH 

To activate the installation type
$ source ~/.bashrc

Test installtion 
$ conda list

//-------virtual environment instruction -------------
Create a virtual environment:

$ conda create --name my_env_name python=3.7

activate your virtual environment

$ conda activate virtual environment
You will get 
(my_env_name) ai@ai:~$ 

To deativate virtualenv type conda deactivate


//---------------------NodeJs--------------------------------
//-----------------------------------------------------------

---> Run everthing with anaconda

Install latest Nodjs in your system from this commands

$ sudo apt-get install curl python-software-properties

$ sudo apt-get install curl software-properties-common

$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

$ sudo apt-get install -y nodejs

$ node -V


///--------------Sublime-Text 3------------------------
-------------------------------------------------------
open terminal type

$ wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

$ echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

$ sudo apt-get update
$ sudo apt-get install sublime-text

To launch sublime from terminal 

$ sudo ln -s /opt/sublime_text/sublime_text /usr/local/bin/subl

 check with 
$ subl hello.py

instruction -sublime -----------------
Create new file and open from terminal

$ subl filename.txt

open any existing file from sublime [try TAB button to search file like:  "subl s" or $ls to list all file  ]

$ subl file_name.txt



//--------------------------------------------------------
Congratulation to setup all tools in your system to work with rasa 

//-------------------------RASA  and RASA X-------------------------------
Now You have to install rasa in your system.
Note: This instrction is intallation without virtualenv

Direct URL
$ pip install rasa-x --extra-index-url https://pypi.rasa.com/simple

Create new diretory 

$ mkdir rasa
$ cd rasa 
$ git clone https://github.com/RasaHQ/rasa.git
$ cd rasa 
$ ls 
You will get requirements.txt file in terminal results
$ pip install -r reuirements.txt 
$ pip install -e .

//Install spacy 
$ pip install rasa[spacy]
$ python -m spacy download en_core_web_md
$ python -m spacy link en_core_web_md en

check rasa vrsion 
$ rasa --version 

Now You have sucessfully installed rasa in yourr system.
// ----------------------------------------------------------------------------


//------------------------------------------------------------------------------
//---------------------START-PROJECT--------------------------------------------

To start any project in your system with rasa 
I prefer virtual enviroment

*Create a directory 


$ rasaProject
$ cd rasaProject
$ mkdir Project1
$ cd Project1

$ conda create -n rasa_venv python=3.7
$ conda activate rasa_venv

*You will get similar things in terminal 

::(rasa_venv) ai@ai:~/rasaProject/Project1$::

Put requirement.txt file from this url: "https://raw.githubusercontent.com/RasaHQ/rasa/master/requirements.txt"
to your Project1 directory then

$ ls
$ pip install -r requirements.txt
$ pip install rasa

#Install spacy 
$ pip install rasa[spacy]
$ python -m spacy download en_core_web_md
$ python -m spacy link en_core_web_md en

------------RASA PROJECT-------------------------------------------------
--*Create you first project and train it with GUI and text both ....... :)

$ rasa init --no-prompt
$ ls
////////////////////////////////////////////////////////////////////
////// if you want to - train rasa with gui -- without rasa X///////

->convert nlu.md to data.json

$ cd data 
/--------------------------------------------------------------
/*convert your json to md and md to json with these commands */

$ rasa data convert nlu --data nlu.md --out data.json -f "json"

$ rasa data convert nlu --data data.json --out nlu.md -f "md"
/--------------------------------------------------------------
$ ls
$ cd .. 

//setting up node for gui--------------------------------------

$ sudo npm i -g rasa-nlu-trainer

$ cd data

$ rasa-nlu-trainer

------------------------------------------------------------------------------
/*You will get an interface  in browser add some intent and entity to train you module save it.
----------------------------------------------------

Always click on terminal middle screen and then press ctrl+alt+T to open same directory in terminal
or 
locate to  your project directory then activate your virtual environment:
suggestion (3 more terminal similarly to run multiple server and test model)
(Make sure you are in Project1 Directory)
//----------------------------------------------------------------------------
(Make sure you are in Project1 Directory and virtual environment activate )

In new terminal :)

$ conda activate rasa_env

$ cd data

$ rasa data convert nlu --data data.json --out nlu.md -f "md"


Your json now converterd into nlu.md(latest rasa is not support json formate )
Conversion is used for only GUI interface to train your model

$ cd .. 
//train your model
$ rasa train
//chat with your module 
$ rasa shell 
//check flow chart of your module
$ rasa visualize
//train rasa in chat by intractiong with it 
// not nessary --export it in nlu.md ,stories.md and  domain.md[]
$ rasa interactive

To check your rasa bot test it with (it will repot you all error acuracy)

$ rasa test 

//-------------integrate you api with you ai-bots------------------------
--------------------------------------------------------------------------
$ subl action.py

It will open in sublime
copy paste my action.py api code paste into it and then save it

->This is used for retriving data from api(not fo slack integration)
//-------------------------------------------------------------------------

//--------------------SLACK-INTEGRATION------------------------------------
///////////////////////////////////////////////////////////////////////////

Go to slack api website  https://api.slack.com/apps
1.Craete your account 
2.Create app
3.select bots 
and give name of bot
4.insall your app to workstation

Go to app dhashboard
select OAuth & Permissions
You will get tokens

go terminal and type 
$ ls
you will get 
credentials.yml

 update it with 

slack:
  slack_token: "<your slack bot user OAuth Token>"
  slack_channel:

Save it or copy paste my file and update tocken

Open new tab in your browser and download Ngrok from website : https://ngrok.com/download
get your token

got to download directory
open terminal
$ ls 

ngrok-stable-linux-amd64.zip will be there

$ unzip ngrok-stable-linux-amd64.zip
$ls
ngrok 

$ ./ngrok authtoken "your ng rocke token"
$ ./ngrok http 80

Cool now you need copy that file ngrock and put it in main project file project 1


start server with

$ python -m rasa_core_sdk.endpoint --actions actions
and keep run this server you will port 5055

/* open new terminal with same directory activate vertual env and run 
1.
$ ./ngrock http 5055
/*
you will get black terminal screen 
keep run the this server 

copy "http://2dbd308d.ngrok.io"

or similar url from Forwarding[make sure it's http not https]

/*update your endpoints.yml of project file with url like this [add url /webhook]

action_endpoint:
  url: 'http://2dbd308d.ngrok.io/webhook'

save it 

 click on any terminal press ctrl+alt+T 

$ conda activate rasa_venv

make sure you are in project1 directory in terminal 

Deploy your code 

$ rasa run
you will get port 5005 or 5002 
keep run this server open new terminal and 
$ ./ngrock http 5002

Ngrock is not work with two terminal free version
two run this 

$ ./ngrock http 5002
you have terminate other runing server of terminal (black screen ngrock)

copy same http url you did before 

/*Go to app dashboard of slack in web browser 
from left navigation bar of webpage you will get Event Subscriptions
Enable it and then
update your Request URL like this 

add this url +/webhooks/slack/webhook


http://b20fb01a.ngrok.io/webhooks/slack/webhook









