
# Create your own auto direct message Twitter Bot 💬💬

![](https://cdn-images-1.medium.com/max/2000/1*yAlQxm27HPR2qjRcqizY2w.png)


Create a welcome message for your new followers in twitter is the first step to get more people engage with your tweets and links, As you know there is a lot of online services that help you send auto direct message to your new followers but I think it’s crazy how online services charge between $5 to $15 for a simple tool that creates bots when you can build your own.

In this article, I will introduce my own Twitter bot that I built to send a welcome message to my new followers on Twitter and how it works for me very fine for 6 months.

By the end of this article, you can build your own twitter auto DM for free !! from creating your message to deploy the bot.

### What do you need?

To develop this bot we need:

-   Node js installed
-   [Twit](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Fttezel%2Ftwit) : Twitter API Client for node (REST & Streaming API)
-   [Github Account](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2F)
-   [Twitter Account](https://medium.com/r/?url=https%3A%2F%2Ftwitter.com%2F)
-   [Heroku Account](https://medium.com/r/?url=https%3A%2F%2Fwww.heroku.com%2F) to deploy the bot.

If you are not familiar with Nodejs. or maybe you are not a programmer, you can fork the project from GitHub and use it as your own.

> Let’s get started.

----------

### Create your Own Twitter Bot 🛠🛠

#### Step 1: Github.

-   Show you support by a simple star 
-   Fork the project repo in Github

-   Now, Customize your welcome message by updating the  `GenerateMessage`function and Commit your change.

#### Step 2 : Twitter

Create a Twitter app: Go to  [https://apps.twitter.com/](https://medium.com/r/?url=https%3A%2F%2Fapps.twitter.com%2F)  and click to the button  `Create New App`, then complete all the fields as the following:

![](https://cdn-images-1.medium.com/max/1600/1*Gr9ggwyDcJgSnK-T8U3_JQ.png)

Go to the  `Permissions`  section and give the app the access to send Direct messages by checking the option “Read, Write and Access direct messages”.

  

![](https://cdn-images-1.medium.com/max/1600/1*m8qV-_h0eK4yMSofD0qINQ.png)

Go to tab `key and Access Tokens` then click the `Generate Access Token` button at the bottom of the page.

Now copy all your keys  `Consumer Key`,  `Consumer Secret` ,  `Acess Token`A and  `Acess Token Secret`, because we need to add all of them later as Heroku vars.

#### Step 3: Heroku

-   Create a  [Heroku account](https://medium.com/r/?url=https%3A%2F%2Fdashboard.heroku.com%2F). it is free!
-   Connect to your Heroku account and create a new app by clicking the  `New`button, then the  `Create new App`  option.
-   Choose your app name then click  `Create App`

![](https://cdn-images-1.medium.com/max/2000/1*J7tbxXiRzeOZTlyzIvYxOg.png)

Choose Github as the Deployment method then click the connect button

![](https://cdn-images-1.medium.com/max/2000/1*QETgzVnscTLIxuD9XFEV5g.png)

Tab your bot repo name : `twitter-bot ` in your case.

![](https://cdn-images-1.medium.com/max/2000/1*nX4Zcbm77GVLmu9s7NWwSQ.png)

Now you need to add all keys as Heroku vars on the tab settings and config the Variables section.

![](https://cdn-images-1.medium.com/max/2000/1*VJgHnF6orcT1PGvyi_JxHA.png)

Return to the deploy section and click “enable automatic deploys”, then “deploy branch” button to deploy your app for the first time.

![](https://cdn-images-1.medium.com/max/2000/1*fbJDa_hPhcR5ZTByd4rIZQ.png)

Go to resources section and activate the worker Dyno and disable the web dyno.

![](https://cdn-images-1.medium.com/max/2000/1*rBSbnSWgrV0d0_lHh38JkQ.png)

To know if your app has been started successfully click to the  `more`  button at the top right of the page then click  `view logs`  option. you will found a simple console with some output similar to this screenshot, I have some new followers and the message has been sent successfully 🤓🤓.

![](https://cdn-images-1.medium.com/max/2000/1*_IH2z4FhXeew5u5PGgW8Nw.png)

----------

### Live Demo

To make sure that’s the hole project work perfectly you need just to  [**follow**](https://medium.com/r/?url=https%3A%2F%2Ftwitter.com%2FElaziziYoussouf)  me and my twitter bot will send you a welcome message 🤗🤗.

----------

### How it works 💡

If you have already cloned the project to your computer you will see this structure:
```sh
$ cd twitter-bot  
$ tree .     
.  
├── config.js  
├── index.js  
├── LICENSE  
├── package.json  
├── Procfile  
├── README.md  
└── src  
    ├── AutoDM.js  
    └── Twit.js
```
As you can see the project is a simple node js app with an index.js file as an entry point:
> infex.js file
![](https://cdn-images-1.medium.com/max/1600/1*Y-eOVjfnFZYCN5LQUblrhw.png)



The index file is a simple script that imports and calls the  `AutoDM`  function.

To make the app more fun we added a simple message when the app has started successfully.

As I have already mentioned I use the twit package to connect to the Twitter API, to do that we need to create a simple twitter app and init the Twit instance with your App config like the following:
> Twit.js file
![](https://cdn-images-1.medium.com/max/1600/1*X4jq7jTLSq346ho5Y7WJ5A.png)


> config.js file
![](https://cdn-images-1.medium.com/max/1600/1*gpIo0pnMOEGV_ApszXz-0A.png)



`process.env.XXXXXXX`  is an environment variable that we need to add to our Heroku app in deployment step.

Now the fun part is to Create the AutoDM function :

As you can see the  `AutoDM`  is a simple arrow function that listens to the stream  `follow`  event from the twitter API and executes the SendMessage function.
> AutoDM.js file
![](https://cdn-images-1.medium.com/max/1600/0*kGF0ObTjFW4zIVA2.)



The  `sendMessge`  function gets as a parameter the user who follows you. All we need here is to create an obj with  `screen_name`  and a text message and send a post request to the Twitter API for sending a Direct Message to  `@screen_name`as the following.
> SendMessge Function
![](https://cdn-images-1.medium.com/max/1600/1*8RHHjhuP5MMix6iyB1oFQA.png)



Now is you your turn to think how you would like to introduce yourself. You can modify the existing GenerateMessage Function to create your own welcome message, don’t forget to add some human behaviour in there, it makes more chance that the user clicks to your link or respond to your message.
> GenerateMessge Function
![](https://cdn-images-1.medium.com/max/1600/1*vsCpSy_gRmkKavZeyzF9WA.png)



It is easy, doesn’t it? you can read more code from the Github repo.
