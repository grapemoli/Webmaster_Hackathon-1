# Summary
:trophy: Alpha Arcade was a winning entry in IUPUI's 2023 Full-Stack Webmasters Hackathon. 

Below is the documentation for the hackathon, which includes the database structure, framework, and security measures.

# Hackathon Documentation
Click this link to be redirected to the website: [Alpha Arcade](https://alphahackathon.pythonanywhere.com/mysite/alpha/templates/registration/login.html)

## Prototyping Documents
### [(Unprofessional) Page Design & Flow](https://indiana-my.sharepoint.com/:p:/g/personal/gtnguyen_iu_edu/EXiy6fiQHO5Kk-9V8cNp_3sBMFEhdBp_koodIPwh8Hpe1A?e=6vHVMn)
### [Database Structure v1](https://github.com/alexbrahos/Webmaster_Hackathon/blob/main/erd.jpg)
### [Database Structure v2](https://github.com/alexbrahos/Webmaster_Hackathon/blob/main/erd_updated.png)
#### NOTE ABOUT FILES❗️❗️
The entire repository holds the client-side-only files. The zip file contains the entire website's source files with server-side operations and frameworking.
To experience a static version of *Alpha Arcade*, clone the respository and open "index.html." To experience the full functionality, click the link; all of the now-Django-i-fied sources files are included, as well as Django structural files. 
**If you are looking at the static version, make sure to clear your cookies often, or certain browsers will not reflect your changes 100% of the time.**

If you're creating an account or logging in, and you get an error, simply clear your cookies and retry.

## Documentation 
### Summary
*Alpha Arcade* is a web application that allows for the user to create accounts, play games, and earn money. The money is used to buy and unlock more games. The website was tested across multiple browsers (Microsoft Edge, Firefox, Chrome) and multiple screen sizes (mobile, desktop). Overall, the website scales well across relatively updated version of browsers, however *Alpha Arcade* is not mobile-friendly. Older browsers were not tested and may have problems supporting certain design choices made. 

Creators: Grace Nguyen, Alex Brahos

The games avaliable are:
1. Clicker (free): The users try to beat the AI and tapping the button faster.
2. Rock, Paper, Scissors
3. Tic-Tac-Toe
4. Aim-Trainer 

###  Specifics
#### Framework
*Alpha Arcade* uses the Django framework hosted on [pythonanywhere](https://www.pythonanywhere.com/). Django allows for CRUD opeations to be done on ALPHA, a SQLite3 database (see *Data Structure* for more information); however, *Alpha Arcade* will only require for the Create, Read, and Update operations. To keep the project within a scope of a one-week project, there is limited user updating/deletion options.
#### Client-Side
The front end is created using the standard web development HTML/CSS/JavaScript languages. The front-end was created from scratch with no assistance from a CSS library or JavaScript extension. The Create Account page uses  a combination of jQuery for client-side validation and the Django validators for server-side valiation. 
The jQuery plug-in version used is 1.19.5.
#### Server-Side
*To keep user login credentials persistent through a session, cookies are used in tandem with the ALPHA database.* While most objects on the website are created and shown by the Client-Side, objects specific to user permissions are managed by the back end. For example, the library of games will only show games the user has permissions for. The back-end also maintains the database of users, permissions, and information about the games. Forms are generated by the back-end, as well. 
#### Security
A side effect of allowing the users to input their information in the Create Account page is the lack of protection against a SQL injection attack. Because Django is the framework, Django Object Relational Mapping (ORM) is an available measure that has stong protection against SQL injections. *Alpha Arcade* created its ALPHA database using Djano's models, so no operations are done without the safety of the API. 
Another side effect of the ORM is that all passwords are hashed. This, alongside the strict client and server validation requirements, keep the user safe throughout their session. A "session" is the duratation a user is logged in. This duration is also the lifespan of the cookie used to grant the user access to *Alpha Arcade* pages. The user may remove the cookies anytime by selecting the "log out" option in the hamburger menu.
#### Images & Fonts
To keep the theme of the website persistent, as well as to prevent plagiarism, all images were made by hand. All fonts were taken from Google's publically avaliable [API](https://developers.google.com/fonts)
<br>
### User Cases
There is only one type of user—the players. Players may want to create an account, as an account will ensure that in-game currency and games bought will be maintained outside of page refreshment. No player who registers under the 'Create Account' menu may gain is_staff or is_superuser permissions. This may only be done throught the Django administrator, who has access to grant permissions, update, and delete users.

### Data Structure
To keep user login and accredited information persistent, cookies are used. All user information are appropriately stored in a relational database. Because of the complexity of Dganjo models, the [original](https://github.com/alexbrahos/Webmaster_Hackathon/blob/main/erd.jpg) ERD was [simplified](https://github.com/alexbrahos/Webmaster_Hackathon/blob/main/erd_updated.png).
<br>
The USER table is an implementation of Django's AbstractBaseUser class, which requires for the user to define multiple additional fields they may not need. For *Alpha Arcade,* these member variables were email, date_joined, and last_login. These variables were defaulted to 'None.' Because the username must be a unique primary key, no two usernames will be used concurrently. Additionally, because the passwords are hashed, there is no way to retreive a forgotten password. 
### Work Flow
The functions available are: Login, Play Game, Buy Game, View Profile, Log Out, or Create Account.
#### Login 
<br>1.1 Has an Account
<br>1.1.1 Correct credentials 
<br>1.1.1.1 Successfully logged in
<br>1.1.1.1.1 Redirected to 2.1
<br>1.1.2 Incorrect credentials 
<br>1.1.2.1 Redirected to 1.1
<br>1.2 Does not have an Account
<br>1.2.1 Redirected to 4.1
#### Main
<br>2.1 Library
<br>2.1.1 Select a permissable game
<br>2.1.1.1 Redirected to GAME
<br>2.2 Select a non-permissable game
<br>2.2.1 User has enough money
<br>2.2.1.1 User now has access to the game, currency is appropiately taken away
<br>2.2.2 User does not have enough money
<br>2.2.2.1 Nothing happens
#### Playing a Game 
<br>3.1 Game loads 
<br>3.1.1 User plays the game 
<br>3.1.1.1 User wins
<br>3.1.1.1.1 User wins in-game currency 
<br>3.1.1.1.1.1 User may eturn home
<br>3.1.1.1.1.1.1 User returns home
<br>3.1.1.1.1.1.1.1 Redirected to 2.1
<br>3.1.1.2 User loses
<br>3.1.1.2.1 User wins no in-game currency
<br>3.1.1.2.1.1 User may return home 
<br>3.1.1.2.1.1.1 User returns home
<br>3.1.1.2.1.1.1.1 Redirected to 2.1
#### Create an Account
<br>4.1 Username is taken or passwords do not match
<br>4.1.1 User must try again
<br>4.2 Username is not taken, passwords match
<br>4.2.1 Account is made in ALPHA
<br>4.2.1.1 User is logged in
<br>4.2.1.1.1 Redirected to 2.1
#### Profile 
<br>5.1 Profile loads
#### Log Out
<br>6.1 User logs out
<br>6.1.1 User is redirected to a temporary "logging out..." page
<br>6.1.1.1 User is redirected to <1.1>
