# CastingAgency
Udacity Full Stack Developer Course Final Project

This API lets Casting Assistants, Casting Directors, Executive Producers read, add, change and delete movies and actors.

# Heroku
The App is deployed on Heroku on the following link:

# Backend
Once you have your virtual environment setup and running, install dependencies by running:
```
pip install -r requirements.txt
```
This will install all of the required packages we selected within the requirements.txt file.

# Running the server
Run the setup script with the required environment variables and initialize Flask:
```
source setup.sh
export FLASK_APP=app.py
flask run --reload
```

# Authentication
This app uses Auth0 as Authentication provider.
- Application Name: 
- Application Domain: 
- ClientID: 
- LoginLink: 

The Logininformation to update the JWT are as follows:
- 
- 
- 


# Roles:
## Casting Assistant
- Can view actors and movies

## Casting Director
- All permissions a Casting Assistant has and…
- Add or delete an actor from the database
- Modify actors or movies

## Executive Producer
- All permissions a Casting Director has and…
- Add or delete a movie from the database