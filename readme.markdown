Who is _DAVE_?
============

DAVE is an acronym that stands for Delete, Add, Edit, and View. These 4 methods make up the core functionality of many transactional web applications. The DAVE API aims to simplify and abstract may of the common tasks that these types of APIs require.

DAVE does the work for you, and he's not CRUD.  Dave was built to be both easy to use, but to be as simple as possible.  I was tiered of bloated frameworks that were designed to be monolithic applications which include the VIEW MVC layer. DAVE is lean and only MV.

The DAVE API was built to be a robust, multi-node capable framework for transactional APIs, appropriate for social networking, games, and more. This API represents the philosophy that a single "desktop" website will not be the only way that your consumers interact with your product. This traditional website is just one of many possible "views" that may be required of your application that might include raw API access for your users and developers, compiled applications, JSON lookups, and more.

To see how simple it is to handle basic actions, this package comes with a basic user system included. Look in /Actions to see the logic behind adding, editing, viewing, and deleting users. This includes logging in.

The DAVE API defines a single access point and accepts GET, POST, or COOKIE input. You define "Action's" that handle the input, such as "AddUser" or "GeoLocate". The DAVE API is NOT traditionally "RESTful", in that it does not use the normal verbs (Get, Put, etc). This was chosen to make it as simple as possible for devices/users to access the functions, including low-level embedded devices which may have trouble with all the HTTP verbs.

The DAVE API understands 2 types of security methodology. "Public" actions can be called by anyone, and then can implement optional user-based security (checking userIDs and PasswordHashes?). Optionally, certain Actions can be defined as "Private", and will require a defined developer to authenticate with every request. This requires your developers to provide an MD5 hash of their APIKey and private DeveloperID to authenticate with. You can mix private and public actions.

Features
--------
* Abstraction of basic DAVE (Delete, Add, Edit, View) actions
* Active Database Modeling on-the-fly or fixed per your requirements
* Objects for Database entities with DAVE abstraction
* Built with a Multi-Node system in mind, but works great on a single machine as well
* Developer-based authentication in tandem with user-level authentication
* Rate Limiting for client connections
* Class-based abstraction of mySQL connections
* Built-in support for multiple types of Caching (Flat File, mySQL, memcache)
* CRON processing of delayed events
* Simple error handling and input sanitization
* XML, JSON, Serialized PHP output types built in
* End-to-end spec testing framework for the API including custom assertions

Stand-Alone Development Webserver written in PHP [ SERVER.php & script_runner.php ]
-----------------------------------------------------------------------------------
To help with development, a single-threaded multi-request webserver is a part of this project.  This will allow you to locally run this framework in "development mode".  This webserver is written entirely in PHP and has support for basic static file-types (css, js, images, html) along with the sand-boxed execution of PHP scripts (including all of those required for this framework.).  The server currently provides the normal $_GET, $_POST, $_COOKIE, $_REQUEST arrays and a basic emulation of $SERVER.  Due to metaprogramming limitations in the default PHP installs on most servers/machines, it is impossible to modify the behavior of header() and setcookie().  To remedy this, please use _header() and _setcookie() in your DAVE projects.  These functions will first attempt to use the default versions of these functions, and if they fail (AKA when using the StandAlone server), will emulate their behavior in other ways.  This server implementation was inspired by nginx, and makes use of spawning OS-level processes to do the heavy lifting for each request

Run "php SERVER.php" from within the project directory to get started.  Point your browser at http://localhost:3000 

Requirements
------------
* PHP 5.2+
* mySQL server 5.1+
* Web-server (tested with Apache 2.0+)
* root access to web-server with CRON

Setup
-----
* Configure your database using mySQL.  Use standard mySQL types (like non-null and uniqueness) to inform DAVE of the rules on each column
* Setup the CONFIG.php file
* CHMOD the CACHE and LOG directory to 777
* Install the CRON.php file to run from CRONTAB
* Launch your webserver!

Actions you can try [[&Action=..]] which are included in the framework:
-----------------------------------------------------------------------
* DescribeActions: I will list all the actions available to the API
* DescribeTables: I am an introspection method that will show the results of the auto-described available tables and cols.  I will show weather or not a col is required and if it is unique
* Geocode: I will use your IP address and return geographic information about you
* CacheTest: Send a Hash [[ &Hash=MyString ]] and I will first store it in the cache, and on subsequent calls retrieve the vale from the cache until expired.  Change the value of the Hash and note the old value will be displayed until it expires
* LogIn: Example user system.  Follow returned error messages.
* UserAdd: Example user system.  Follow returned error messages.
* UserDelete: Example user system.  Follow returned error messages.
* UserEdit: Example user system.  Follow returned error messages.
* UserView: Example user system.  Follow returned error messages.
* ObjectTest: An example of on-the-fly database object manipulation.  Check the code for this file to see how simple it is.
* CookieTest: Will set cookies in your browser.  Use this to test SERVER's implementation of _setcookie()
* SlowAction: A simple action that will sleep for a number of seconds.  Use this to test SERVER's non-blocking implementation by making a slow request, and then other requests to ensure that a slow request will not block other actions from processing.
	
Example Site: http://dave.evantahler.com
----------------------------------------

Note on MaxMind GeoLocation
---------------------------
You will need the MaxMind? "GeoLiteCity?" database file for this to work. It's free! Get it here http://www.maxmind.com/app/geolitecity and put it in the /MaxMind? folder.