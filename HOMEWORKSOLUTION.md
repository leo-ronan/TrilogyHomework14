 ==== Develop =====
|   --= server.js =--
|       This file requires all necessary npm packages, which are express and passport in this case. 
|       A port is set (8080), the database from "./models" is also required.
|       The express app is created, and express-session is used to because of the use of passport (tracks user login status).
|       Html and Api routes are required, and the previously required database is synced.
|
|   --= package.json =--
|       Contains info relevant to the project, such as the name, current version, main server file, and dependencies.
|       Dependencies: 
|           bcryptjs,
|		    express, 
|		    express-session, 
|		    mysql2, 
|		    passport, 
|		    passport-local, 
|		    sequelize
|
|
|    ==== Config =====
|   |
|   |    ==== middleware =====
|   |   |
|   |   |   --= isAuthenticated.js =--
|   |   |       This file restricts users who aren't logged in from accessing routes that require them to be.
|   |
|   |
|   |   --= passport.js =--
|   |       This file requires passport, using a Local Strategy, meaning the a user's email and password will be stored.
|   |       Once configured, passport is exported.
|   |
|   |   --= config.json =--
|   |       Provides database user credentials, database to use, host IP, and dialect (mySQL). 
|   |       There are three environments: development, test, and production.
|
|
|
|    ==== Models =====
|   |
|   |   --= index.js =--
|   |       This file requires fs, path, sequelize, config.json from the config folder.
|   |       Sequelize is used to set up the database to be used here. 
|   |
|   |   --= user.js =--
|   |       This file requires bcryptjs.
|   |       A User model is created, which must include email and password.
|   |       Using bcryptjs, passwords are hashed before a user is created.
|   |       Returns User.
|
|
|
|    ==== Public =====
|   |
|   |    ==== js =====
|   |	|
|   |   |   --= login.js =--
|   |   |       This file pulls values from the login form, which contains emailInput and passwordInput.
|   |   |       When the login form is submitted, the loginUser function posts the emailInput and passwordInput to the api route "/api/login".
|   |   |       On success, the user is sent to the html route /members. If there's an error, it is logged.
|   |   |
|   |   |   --= members.js =--
|   |   |       This file performs a GET request to api route "/api/user-data/ to figure out which user is logged in, 
|   |   |       and the page's html is updated to display the correct email.
|   |	|
|   |   |   --= signup.js =--
|   |   |       This file pulls values from the signup form, which contains emailInput and passwordInput (neither can be null).
|   |   |       On submit, the signUpUser function is ran with the email and password as its parameters.          
|   |   |       This function POSTS to api route "/api/signup", and on success the user is redirected to the html route "/members".
|   |   |       If an error occurs, a boostrap alert will appear.
|   |
|   |
|   |	 ==== stylesheets =====
|   |	|
|   |	|   --= style.css =--
|   |	|       CSS stylesheet for styling the page.
|   |   
|   |
|   |       --= login.html =--
|   |      	    HTML file for login page.  
|   |       	Requires login.js, style.css, bootstrap, and jQuery.
|   |
|   |       --= members.html =--
|   |       	HTML file for members page.
|   |       	Requires members.js, style.css, bootstrap, and jQuery.
|   |
|   |  	    --= signup.html =--
|   |       	HTML file for signup page.
|   | 		    Requires signup.js, style.css, bootstrap, and jQuery.
|
|
|
|    ==== routes =====
|   |
|   |   --= html-routes.js =--
|   |       This file requires path, and isAuthenticated (from the middleware folder).
|   |
|   |       Sets html routes: 
|   |           "/": Home page, but may send user to /members if they are already logged in.
|   |
|   |           "/login": Login page, but may send user to /members if they are already logged in.
|   |
|   |           "/members": Members page, but user must be authenticated (using isAuthenticated).
|   |
|   |   --= api-routes.js =--
|   |       This file requires the database in use, and passport.
|   |
|   |       Sets api routes:
|   |           "/api/login": Using passport.authenticate middleware with local strategy, checks if a user's credentials are valid. If valid, user is sent to /members, 
|   |                         if not the user will be given an error.
|   |           
|   |           "/api/signup": Allows user's to create a new account, where the password is hashed and stored before the sequelize User model is configured.
|   |
|   |           "/logout/: Logs the user out.
|   |           
|   |           "/api/user_data": Retrieves data about user to be used within on the client's side. Sends back user's email and id, NOT password. 
|   |                             If the user is not logged in, an empty json object is sent back.
                

    
