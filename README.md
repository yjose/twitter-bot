# twitter-bot

Node js twitter bot to send auto direct message

## how it works

* start the project
* fork the project
* customize you auto direct message
* create a simple heroku account
* create a twitter app
  * go to https://apps.twitter.com/ and click to the boutton "Create New App"
  * go to the setting section and give the app accesse to send messages by "read, Write and Access direct messages"
  * go to tab key and Access Tokens and click the "generate Acess Token buotton" in the page bottom.
  * Now copy all your key `Consumer Key` `Consumer Secret` `Access Token` and `Access Token Secret` we will need it later !!
* set all env variables from your heroku dashboard > twitter_bot > Settings
* go to resources section and activate the worker Dyno and disable the web dyno
