#Server interactions

This file explains the interactions between different php scripts and the server database

####Rules (rules.php)
This file is designed to provide a user interface to modify setting within the system. It has no access to the database, however submits actions to the submit script.

####Submit (resource/datahandling/submit.php)
This file is the backend for security and database access. It handles queries and data entry for rules, as well as the incoming data collection and initial processing.

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
  
The following get requests are recomended:
  ka, kb - keeps record of the keys
  redir - where to redirect when finished.
  act - the action that the submit script should preform. This is can be one of the predefined acions, or the query action.
  
#### Actions

<to come>
