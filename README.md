#Azure Active Directory OIDC Web Sample

This Node.js app will give you with a quick and easy way to set up a Web application in node.js with Express using OpenID Connect. The sample server included in the download are designed to run on any platform.

We've released all of the source code for this example in GitHub under an MIT license, so feel free to clone (or even better, fork!) and provide feedback on the forums.


## Quick Start

Getting started with the sample is easy. It is configured to run out of the box with minimal setup.

### Step 1: Register a web application in B2C Azure AD Tenant

If you don't have an Azure AD B2C Tenant yet, please [create one](https://docs.microsoft.com/en-us/azure/active-directory-b2c/tutorial-create-tenant).

Next let's register a web application in your tenant.

* In the main page of your tenant, click `Azure B2C settings`, and you will be redirected to the settings page.

* Click `App registrations (preview)`, then click `Add`. Enter a name like 'my_b2c_app', Choose `Accounts in any organizational directory or any identity provider`, Under redirect URI select `Web` and enter 'http://localhost:3000/auth/openid/return' into the field. Click `Register` to create the application.

* Click the application you just created, copy the `Application ID` field and save it somewhere. This value is the clientID of your application.

* Then click `Certificates & secrets` to generate a client secret and save it somewhere. This app key is the client secret of your application.

* Click `Authentication` and where it says `Implicit Grant` check both boxes for `Access tokens` and `ID tokens`.

* Now let's add some policies we will use for this sample. From your B2C tenant Overview page you will cick `User flows (policies)`.  Add a sign-in policy, a sign-up policy, a profile-editing policy and a password-reset policy. When you add the policies, in step 1 use the names 'signin', 'signup', 'updateprofile' and 'resetpassword' respectively; For step 2 `Identity providers`, choose `Email signup`; in step 4 choose `Show more...` and then in the `Return claim` column be sure to check, choose `Email Addresses`, `User's Object ID` and any other claims you want; for `Sign-up attributes`, choose `Email Address` and anything else you like.

* Now we have a B2C web application and policies registered. Note that Azure AD adds a 'B2C_1_' prefix automatically to all policy names, so the policy names we will use are actually 'B2C_1_signin', 'B2C_1_signup', 'B2C_1_updateprofile' and 'B2C_1_resetpassword'.

### Step 2: Download node.js for your platform
To successfully use this sample, you need a working installation of Node.js.

### Step 3: Download the Sample application and modules

Next, clone the sample repo and install the NPM.

From your shell or command line:

* `$ git clone git@github.com:HaroldPutman/B2C-WebApp-OpenIDConnect-NodeJS.git`
* `$ npm install`

### Step 4: Configure your server

* Create a file `.env` in same folder as app.js like this:

```txt
TENANT_NAME=your-tenant-name
CLIENT_ID=692dc0f8-SAMPLE-b6d5-5e3c8f5cd0e4
CLIENT_SECRET=Hvhe5-uuMw33SAMPLEzkL[?RcQEkxq-bd6
```

You can also add any of these optional values:

```txt
SERVER_NAME=https://partnernet-dev.lexmark.com
RETURN_PATH=/callback/j_security_check
POLICY_SIGNIN=B2C_1_SI2
```

* `exports.useMongoDBSessionStore` is set to false in config.js, set this to true and update `exports.databaseUri`, if you want to use mongoDB session store and a different database uri.

* Update `exports.mongoDBSessionMaxAge`. Here you can specify how long you want
to keep a session in mongoDB. The unit is second(s).

* **SSL** if your servername has to be https you should provide self-signed keyfiles `server.key` and `server.cert`. You generate those by running this:

```sh
openssl req -nodes -new -x509 -keyout server.key -out server.cert
```

### Step 5: Run the application

* Run the app.

Use the following command in terminal.

* `$ node app.js`

**Is the server output hard to understand?:** We use `bunyan` for logging in this sample. The console won't make much sense to you unless you also install bunyan and run the server like above but pipe it through the bunyan binary:

* `$ npm install -g bunyan`
* `$ node app.js | bunyan`

### You're done!

You will have a server successfully running on `http://localhost:3000`.

### Acknowledgements

We would like to acknowledge the folks who own/contribute to the following projects for their support of Azure Active Directory and their libraries that were used to build this sample. In places where we forked these libraries to add additional functionality, we ensured that the chain of forking remains intact so you can navigate back to the original package. Working with such great partners in the open source community clearly illustrates what open collaboration can accomplish. Thank you!


## About The Code

Code hosted on GitHub under MIT license
