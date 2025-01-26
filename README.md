# backend_portfolio-project
# Project Title: Backend Web  Application built using Deno 
Project Overview:
Handless Https requests and managing authentication routes
Purpose :
Helps developers have base knowledge to develop backend server using Deno: A javascript runtime.
The server runs on:
. @oak oak niddleware Framework, 
. Perform CRUD operations with SQLite databases using @db/sqlite
. sign and verify using WebCrypto API for JWT with @zaubrik/djwt
. Hash passwords with @denosaurs/argontwo

GENERAL USE:
1: FIRST clone this repository
2: Once the repository is cloned locate the /backend-server-app
and follow the steps explained under 'USAGE'
USAGE:
main goal: doing CRUD operations with register, updateAccount and deleteAccount using sqlite module.
# .1 OPEN A Separate terminal and Generate a new TOKEN.

Run the following command.

deno run generateToken.ts
Paste the token to the .env file by replacing the old one. For example, if your new token is "ijkl", and your old token is "YOUR_NEW_TOKEN", you must replace it with your "YOUR_NEW_TOKEN" with "ijkl".

# .2 Restart the backend server

Close the previous one and run the following command.

deno run -A main.ts
# .3 Open a new terminal.
 Register a user with your desired username using curl command. 
 Replace "name" with your desired username  and "pwd" with your desired password,before running the command below. 

curl -i -XPOST -d '{"username": "name", "password": "pwd"}' --url http://127.0.0.1:5555/register 
# .4 Login the new user that has your desired Username

curl -i -XPOST -d '{"username": "name", "password": "pwd"}' --url http://127.0.0.1:5555/login --cookie-jar cookie.cookie
There will be a file created called cookie.cookie.
a jwt signature will also be created in the terminal  Open the file.  See screenshot below for what it looks like:

 You must copy the WHOLE string.


# .5 Update the user's username by appending "-Ready"

 e.g. "name-Ready". Replace "yourJWTString" with your JWT signature you copied previously before running the command below.

curl -i -XPUT -d '{"username": "name-Ready", "password": "pwd"}' --url http://127.0.0.1:5555/auth/update --cookie cookie.cookie -H "Authorization: Bearer yourJWTString"
You have to relogin after this with the new username. Replace "name" with your desired username before running the command below.

curl -i -XPOST -d '{"username": "name-Ready", "password": "pwd"}' --url http://127.0.0.1:5555/login --cookie-jar cookie.cookie
Copy the new JWT signature in cookie.cookie.

# .6 Delete the user by calling the appropriate route path. 
Replace "yourJWTString" with your JWT signature you copied previously before running the command below.
curl -i -XDELETE --url "http://127.0.0.1:5555/auth/delete" --cookie cookie