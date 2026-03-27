CSHMembersPortal
================

GLORIOUS REDESIGN of the internal CSH Members Portal. Uses [bootstrap-csh](https://github.com/ComputerScienceHouse/bootstrap-csh) for styles and [Icons8](https://icons8.github.io/welovesvg/) for icons. Made with [AngularJS](https://angularjs.org/).

Contributing
------------

### Local development
Set the env variables in your favorite way (I just put them with `ENV VAR_NAME=VALUE` in dockerfile, there might be a better way but idk; be careful not to commit them though)

Ask an RTP for OIDC creds, setting the cookie domain to localhost is needed because that's the domain it stores the cookies for and it freaks out if the domain isn't the same as the server name.
```
ENV SERVER_NAME=localhost:8080
ENV HTTP_SCHEME=http
ENV OIDC_CLIENT_ID=
ENV OIDC_CLIENT_SECRET=
ENV OIDC_COOKIE_DOMAIN=localhost
```

Run docker exposing port 8080

```
docker build . -t members && docker run -it -p 8080:8080 members
```

### Pull Requests
If you have an idea for a feature or have a bug that you'd like to fix, please fork this repo to a private repo of your own. If your contribution is more than some small tweak, create a branch. Do your thing, and then submit a pull request.

### Issue Tracking
Please make use of GitHub's issue tracker for this repo. Feel free to report any bugs, features, and feedback.

Updating Links
--------------

Instead of updating the markup directly, the "Members Resources" section is generated using data from `data/links.json`.

Here's what a normal link looks like:

```javascript
[
  	{ 
    	"name": "Info",
    	"links": [
    		...
        	{
        		"name": "Wiki",
        		"href": "https://wiki.csh.rit.edu",
        		"icon": "zocial:wikipedia",
        		"popular": true
        	},
        	...
    	]
  	},
  	...
]
```

The "icon" property maps to the icon's class name from [Icons8](https://icons8.github.io/welovesvg/). For example, `material:cloud` will render a cloud icon.

The "popular" property is optional. If included and set to `true`, the link will appear in the Popular section.

Some entries may link to multiple sites. Here's how to add a link with a dropdown:

```javascript
[
  	{ 
    	"name": "Info",
    	"links": [
    		...
        	{ 
		        "name": "Events",
		        "dropdown": [
		            {
		            	"name": "Calendar",
		            	"href": "https://www.google.com/calendar/embed?src=rti648k5hv7j3ae3a3rum8potk%40group.calendar.google.com&ctz=America/New_York"
		          	},
		          	{
		            	"name": "XML",
		            	"href": "http://www.google.com/calendar/ical/rti648k5hv7j3ae3a3rum8potk%40group.calendar.google.com/public/basic"
		          	},
		          	{
		            	"name": "iCal",
		            	"href": "http://www.google.com/calendar/ical/rti648k5hv7j3ae3a3rum8potk%40group.calendar.google.com/public/basic.ics"
		          	}
		        ],
		        "icon": "material:events",
		        "popular": true
        	...
    	]
  	},
  	...
]
```

Updating Meetings
-----------------

Like links, meetings are generated from the `data/meetings.json` file. A meeting entry looks like this:

```javascript
[
  { 
    "name": "House", 
    "day": "SUN", 
    "time": "7:00" 
  },
  ...
```

Using Grunt
-----------

Learn more about Grunt: http://gruntjs.com

First, install grunt-cli: `npm install -g grunt-cli`

Next, install dependencies: `npm install`

Available grunt tasks:
* `grunt` or `grunt serve`: Spin up a local web server at `http://localhost:9001` to test your changes
