#Server interactions

This file explains the interactions between different php scripts and the server database

####Rules (rules.php)
This file is designed to provide a user interface to modify setting within the system. It has no access to the database, however submits actions to the submit script.

####Submit (resource/datahandling/submit.php)
This file isthe backend for security and database access. It handles queries and data entry for rules, as well as the incoming data collection and initial processing.

####text editor (text-editor.php)
edits large-text database entries, saves through submit and accessed/returns to rules.

####index (index.php)
Graphes data, with direct, read only, access to the database.

####status (status.php)
Read-only access to database, pulls in data to show alerts. Users able to write custom html and js.

####generatecsv (resource/datahandling/generatecsv.php)
Creates a csv of the selected sensor and redirects to its download. Read only database access.

See the video below for an overall explaination of how these connect.

<to come>

###Submit api

There are 3 types of requests:
  - 1) key request, returns public key.
  - 2) data submition, used by collector to submit data. See collector documentation.
  - 3) action request, this is used by other parts of the website to as a backend to modify database data.

The following GET options are needed for an action request:
  stage=3
  token - the login token, see login documentation
  session - the session id, see login documentation
  act - the action that the submit script should preform. This is can be one of the predefined acions, or the query action.
  
The following get requests are recomended:
  ka, kb - keeps record of the keys
  redir - where to redirect when finished.
  
#### Actions

To preform an action, a request is sent to resource/datahandling/submit.php?stage=3&session=[sessionID]&token=[loginToken]&act[ACTION NAME]
In very special cases, such as loging in, the token and session are not required, but in this case an encrypted pass feild will be.
Note that all actions are CAPIALISED

##### DOWNLOAD

downloads a file, this can be used to download protected files that cannot be accessed without authonication. To do this, a copy of the file is made in an accessible publically accessible location for the download then deleted afterwards.

additon parameters are:
GET 'name' = file/path/to/download

##### AND_SENSOR

Adds or updates a sensor

additonal parameters are:
POST 'oid' [the old sensor id, used to update existing sensors] = number (0-15) or 'new' if not updating.
POST 'nid' [new id, the id number to be used for the sensor] = number (0-15)
POST 'lat' = latidude
POST 'lng' = Longitiude
POST 'hrn' = human readable name (eg: workshop temperature sensor)


##### TEST_SMS

Sends a text message (designed to test the system)

GET 'msg' = the message to send
GET 'number' = a number with country code


##### ADD_NUMBER

adds a number to the contact list. Please note this will also send a text to the number to say it has been added.

POST 'cc' = country code
POST 'number' = number without country code 
POST 'phone_name' = the name feild of the contact list


##### SENSOR_TYPE

adds a new sensor type

POST 'nid' = id number
POST 'stn' = sensor type name


##### RULE

adds a rule

POST 'eh' = end hour (24h time)
POST 'em' = end minute
POST 'sh' = start hour (24h time)
POST 'sm' = start minute (note all time feild can be ignored if no required)
POST 'delay' = delay
POST 'send_clear' = 'on'/any other value
POST 'node' = node hr name
POST 'sensor' = sensor type name
POST 'op' = operation (Greater than/Less than/Equal to)
POST 'value' = numerical value
POST 'contact' = phone name
POST 'msg' = you message here


##### DEL_NUM

Deletes a contact

GET 'num' = number to delete (will delete name entries alongside given number)


##### WRITE_FILE

Writes a file to the server

GET 'f' = path/to/file (note this is relative to the web directory, not the datahandling directory)
GET 'contents' = what will be inside the file


##### QUERY

a generic database query

GET 'q' = an sql query

(note, the results will not be returned, so this is more designed for manipulating data you know exists.)

##### DEL_SENSOR

deletes a sensor

GET 'id' = sensor id number (note this is a referernce used to find the sensor, all assocated data will also be erased)

<and more>




