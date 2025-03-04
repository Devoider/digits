<img src="doc/landing.PNG">

## Installation

First, [install Meteor](https://www.meteor.com/install).

Second, go to [https://github.com/Devoider/digits](https://github.com/Devoider/digits), and clone it to your own repository.

Third, go to your newly created repository, and click the "Clone or download" button to download your new GitHub repo to your local file system.  Using [GitHub Desktop](https://desktop.github.com/) is a great choice if you use MacOS or Windows.

Fourth, cd into the app/ directory of your local copy of the repo, and install third party libraries with:

```
$ meteor npm install
```

## Running the system

Once the libraries are installed, you can run the application by invoking the "start" script in the [package.json file](https://github.com/ics-software-engineering/meteor-application-template-react/blob/master/app/package.json):

```
$ meteor npm run start
```

The first time you run the app, it will create some default users and data. Here is the output:

```
meteor npm run start

> meteor-application-template-react@ start C:\Users\drako\Documents\GitHub\digits\app
> meteor --no-release-check --settings ../config/settings.development.json

[[[[[ C:\Users\drako\Documents\GitHub\digits\app ]]]]]

=> Started proxy.
=> Started MongoDB.
W20200407-16:52:04.193(-10)? (STDERR) Note: you are using a pure-JavaScript implementation of bcrypt.
W20200407-16:52:04.236(-10)? (STDERR) While this implementation will work correctly, it is known to be
W20200407-16:52:04.237(-10)? (STDERR) approximately three times slower than the native implementation.
W20200407-16:52:04.238(-10)? (STDERR) In order to use the native implementation instead, run
W20200407-16:52:04.239(-10)? (STDERR)
W20200407-16:52:04.240(-10)? (STDERR)   meteor npm install --save bcrypt
W20200407-16:52:04.241(-10)? (STDERR)
W20200407-16:52:04.242(-10)? (STDERR) in the root directory of your application.
I20200407-16:52:04.440(-10)? Creating the default user(s)
I20200407-16:52:04.441(-10)?   Creating user admin@foo.com.
I20200407-16:52:04.654(-10)?   Creating user john@foo.com.
I20200407-16:52:04.853(-10)? Creating default data.
I20200407-16:52:04.854(-10)?   Adding: Johnson (john@foo.com)
I20200407-16:52:04.867(-10)?   Adding: Casanova (john@foo.com)
I20200407-16:52:04.870(-10)?   Adding: Binsted (admin@foo.com)
=> Started your app.

=> App running at: http://localhost:3000/
   Type Control-C twice to stop.
```


### Note regarding "bcrypt warning":

You will also get the following message when you run this application:

```
Note: you are using a pure-JavaScript implementation of bcrypt.
While this implementation will work correctly, it is known to be
approximately three times slower than the native implementation.
In order to use the native implementation instead, run

  meteor npm install --save bcrypt

in the root directory of your application.
```

On some operating systems (particularly Windows), installing bcrypt is much more difficult than implied by the above message. Bcrypt is only used in Meteor for password checking, so the performance implications are negligible until your site has very high traffic. You can safely ignore this warning without any problems during initial stages of development.

### Viewing the running app

If all goes well, the template application will appear at [http://localhost:3000](http://localhost:3000).  You can login using the credentials in [settings.development.json](https://github.com/ics-software-engineering/meteor-application-template-react/blob/master/config/settings.development.json), or else register a new account.

## Walkthrough

The following sections describe the major features of this template.

### Directory structure

The top-level directory structure is:

```
app/        # holds the Meteor application sources
config/     # holds configuration files, such as settings.development.json
doc/        # holds developer documentation, user guides, etc.
.gitignore  # don't commit IntelliJ project files, node_modules, and settings.production.json
```

This structure separates documentation files (such as screenshots) and configuration files (such as the settings files) from the actual Meteor application.

The app/ directory has this structure:

```
client/
  main.html      # The boilerplate HTML with a "root" div to be manipulated by React.
  main.js        # import startup files.

imports/
  api/           # Define collections
    stuff/       # The Stuff collection definition
  startup/       # Define code to run when system starts up (client-only, server-only, both)
    client/
    server/
  ui/
    layouts/     # Contains top-level layout (<App> component).
    pages/       # Contains components for each page.
    components/  # Contains page elements, some of which could appear on multiple pages.

node_modules/    # managed by npm

public/          # static assets (like images) can go here.

server/
   main.js       # import the server-side js files.
```

### Import conventions

This system adheres to the Meteor guideline of putting all application code in the imports/ directory, and using client/main.js and server/main.js to import the code appropriate for the client and server in an appropriate order.

### Application functionality

The application implements a simple CRUD application for managing "Stuff", which is a Mongo Collection consisting of a name (String), a quantity (Number), and a condition (one of 'excellent', 'good', 'fair', or 'poor').

By default, each user only sees the Stuff that they have created.  However, the settings file enables you to define default accounts.  If you define a user with the role "admin", then that user gets access to a special page which lists all the Stuff defined by all users.

#### Landing page

When you retrieve the app at http://localhost:3000, this is what should be displayed:

<img src="doc/landing.PNG">

The next step is to use the Login menu to either Login to an existing account or register a new account.

#### Login page

Clicking on the Login link, then on the Sign In menu item displays this page:

<img src="doc/signin-page.PNG">

#### Register page

Alternatively, clicking on the Login link, then on the Sign Up menu item displays this page:

<img src="doc/signin-page.PNG">


#### Landing (after Login) page, non-Admin user

Once you log in (either to an existing account or by creating a new one), the navbar changes as follows:

<img src="doc/landing-after-login.PNG">

You can now add new Stuff documents, and list the Stuff you have created. Note you cannot see any Stuff created by other users.

#### Add Contact page

After logging in, here is the page that allows you to add new Stuff:

<img src="doc/add-contact.PNG">

#### List Contact page

After logging in, here is the page that allows you to list all the Stuff you have created:

<img src="doc/list-contact.PNG">

You click the "Edit" link to go to the Edit Stuff page, shown next.

#### Edit Contact page

After clicking on the "Edit" link associated with an item, this page displays that allows you to change and save it:

<img src="doc/edit-contact.PNG">

#### Landing (after Login), Admin user

You can define an "admin" user in the settings.json file. This user, after logging in, gets a special entry in the navbar:

<img src="doc/admin-landing.PNG">

#### Admin page (list all users stuff)

To provide a simple example of a "super power" for Admin users, the Admin page lists all of the Stuff by all of the users:

Note that non-admin users cannot get to this page, even if they type in the URL by hand.
