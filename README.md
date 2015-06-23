# stamplay-selfkickstarter
========================

![selfkickstarter](https://blog.stamplay.com/wp-content/uploads/2014/12/Screenshot-2014-11-27-10.52.53.png)

**This project is built on the [Stamplay](https://stamplay.com) platform and [AngularJS](http://angularjs.org) to show how to build a  landing page to raise funds leveraging Stripe integration,
let's say something similar to [KickStarter](http://kickstarter.com) but done in the blink of an eye.**

You can test it anytime simply creating a new project on Stamplay and uploading all the frontend assets with our client or our browser based code editor. 

Feel free to implement more cool features (see the last paragraph for ideas), contribute to this repo or clone it to use it by your own scopes. For any question drop an email to [giuliano.iacobelli@stamplay.com](mailto:giuliano.iacobelli@stamplay.com)

-----------------------
## KickStarter

This is a demo of what you can achieve with Stamplay,it's somewhat a clone of [kickStarter](http://kickstarter.com) and here you can see it up and running [https://kickstarter.stamplayapp.com](https://kickstarter.stamplayapp.com)

We love javascript and front end framework and this time we show you how you can create this app using [AngularJS](http://angularjs.org) to implement the client side logic. Here are the user stories for this example:

* Guest users can signup with Facebook
* Logged users can donate a fixed amount for you project
* Admins can set a goal of the campaign 
* Admins can see all payment details via Stripe dashboard

Best of all, we used AngularJS :) Prepare to be amazed.

-----------------------
# Anatomy

self-KickStarter is built around the following building blocks

* [User](https://stamplay.com/docs/rest-api#user)
* [Custom Objects](https://stamplay.com/docs/rest-api#custom-object-api)
* [Stripe](https://stamplay.com/docs/rest-api#stripe)


## Requirements

Go to [your account](https://editor.stamplay.com/apps) and create a new app.


## Configuring the components

After creating a new app on [Stamplay](https://editor.stamplay.com) let's start by picking the component we want to use in our app that are: **User**,**Custom Objects** and **Stripe**.

Lets see one-by-one how they are configured:

### User
the app leverages Facebook Login to provide an easy login to its users. In order to activate yours you need to get an APPID and APPSecret on [Facebook Developer's portal](https://developers.facebook.com/apps), create an app and add Stamplay.com as authorized domain as you can see in the pic below. 

![Facebook app settings](https://blog.stamplay.com/wp-content/uploads/2014/07/Schermata-2014-07-22-alle-17.43.24.png "Facebook app settings")

Now you have the data to configure Facebook Login on your app's user module. Go back on Stamplay, select the user component, add Facebook as signup service and then cut and paste the App ID and App Secret and click save.


### Custom Object
Let's define the entities for this app, we will define **Backer** and **Fund** that are defined as follows:

##### Backer

* Name: `lastfour`, Type: `string`, The last four of the credit card
* Name: `user`, Type: `user relation`, The user reference 

##### Fund

* Name: `money`, Type: `number`, The total amount raised until now

After setting up this Stamplay will instantly expose Restful APIs for our newly resources the following URIs: 

* `https://APPID.stamplayapp.com/api/cobject/v1/backer`
* `https://APPID.stamplayapp.com/api/cobject/v1/fund`

### Stripe

Connect your account simply by clicking on Connect button and choose between live or test mode.   

-----------------------


## Creating the server side logic with Tasks

Now let's add the tasks that will define the server side of our app. For our app we want that:

### When a user sign up, then create a new Stripe customer 

Trigger : User - Sign up

Action: Stripe - Create Customer

**Stripe Configuration**

	User ID : {{user._id}}


### When a customer is charged, then add an item to the cobject collection 

Trigger : Stripe - Charge

Action: Custom Object - Create 

**Custom Object Configuration**

	Cobject Schema: Backer

	lastfour:  {{payment.card.last4}}

	user: {{user._id}}

_______________________________

# Managing the app

Everytime you create reasource using Custom Object you can manage instances of the entities in the Admin section. This will let you to easily add edit.
First of all create from Admin section an custom Object instance from fund model, this instance will need to represent the amount raise until now. 
IMPORTANT: change the Stripe key on index.html 

-----------------------

# Cloning

First, clone this repository :

    git clone https://github.com/Stamplay/stamplay-selfkickstarter.git
    
Or download it as a zip file
	
	https://github.com/Stamplay/stamplay-selfkickstarter/archive/master.zip 

Then you need to upload the frontend files in your app by using the [CLI tool](https://github.com/Stamplay/stamplay-cli):

```js
cd your/path/to/stamplay-selfkickstarter
stamplay init
/*
 * You will need to insert your appId and your API key
 */
stamplay deploy
```


-----------------------
# Next steps

Here are a few ideas for further improvement :

* Add social login like Google or Twitter to enrich user's identity
* Add possibility to comment your project form logged User
* Add grunt or gulp task to minify all assets
* Add custom 404 page
* _Your idea here… ?_

Again, for any questions drop an email to [giuliano.iacobelli@stamplay.com](mailto:giuliano.iacobelli@stamplay.com) :)

Ciao!
