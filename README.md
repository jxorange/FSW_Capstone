# CastingAgency
This project is backend web application following Udacity Fullstack Developer Nanodegree guidelines. It's a web app for a casting agency where users can add movies, actors, and relate each actor to the movies he/she acted in, and vice versa. This project uses python, flask and postgresql for it's backend and hosted on heruko.

All backend code follows PEP8 style guidelines.
As of now, there is no frontend for this app. You can test it using cURL or Postman.
This app is deployed on heroku under this link.


# Pre-requisites and Local Development
- Python 3.7
- Virtual Environment
- PIP Dependencies
- Flask
- SQLAlchemy and Flask-SQLAlchemy

# Heroku
The App is deployed on Heroku on the following link:https://fsw-capstone.herokuapp.com/

# Backend
Once you have your virtual environment setup and running, install dependencies by running:
```
pip3 install -r requirements.txt
```
This will install all of the required packages we selected within the requirements.txt file.

# Running the server
Run the setup script with the required environment variables and initialize Flask:
```
source setup.sh
export FLASK_APP=app.py FLASK_DEBUG=true
flask run 
```

# Endpoints
## Actor Endpoints
### GET /actors
- A Public Endpoint that fetches a list of all actors. If there are no actors, it will return an empty list.
- Permissions required: None
- Request Arguments: None

### DELETE /actors
- A Public Endpoint that deletes an existing actor from the database. Returns a 404 if the actor <id> is not found.
- Permissions required:'delete:actors'
- Request Arguments: None

### POST /actors
- Creates a new actors and stores it in the database. It will throw a 400 if the incorrect parameters are passed.
- Permissions required:'post:actors'
- Request Arguments:
'name': A string that is the full name of the actor.
'age': An Integer that is the age of the actor.
'gender': A string that is the gender of the actor.

### PATCH /actors/<id>
- Updates an existing actor. It will throw a 404 if <id> is not found.
- Permissions required:'patch:actors'
- Request Arguments:
	- [Optional] 'name': A string that is the full name of the actor.
	- [Optional] 'age': An Integer that is the age of the actor.
	- [Optional] 'gender': A string that is the gender of the actor.
	- The actor information will not change if none of the request arguments are supplied. However, a 200 will still be returned.

## Movie Endpoints
### GET /movies
- A Public Endpoint that fetches a list of all movies. If there are no movies, it will return an empty list.
- Permissions required: None
- Request Arguments: None


### DELETE /movies
- A Public Endpoint that deletes an existing movie from the database. Returns a 404 if the movie <id> is not found.
- Permissions required:'delete:movies'
- Request Arguments: None

### POST /movies
- Creates a new movies and stores it in the database. It will throw a 400 if the incorrect parameters are passed.
- Permissions required:'post:movies'
- Request Arguments:
'title': A string that is the full title of the movie.
'release_date': A string of the release date of the movie, in the format "YYYY-MM-DD"

### PATCH /movies/<id>
- Updates an existing movie. It will throw a 404 if <id> is not found.
- Permissions required:'patch:movies'
- Request Arguments:
    -  [Optional] 'title': A string that is the full title of the movie.
	- [Optional] 'release_date': A string of the release date of the movie, in the format "YYYY-MM-DD"
	- The movie information will not change if none of the request arguments are supplied. However, a 200 will still be returned.

# Authentication
This app uses Auth0 as Authentication provider.
- LoginLink: https://fsw-final.us.auth0.com/authorize?audience=myapp&response_type=token&client_id=AEznY1DMZyVH60GCqSUKvdscz53ajIL8&redirect_uri=https://fsw-capstone.herokuapp.com/

follow below account in [login page](https://fsw-final.us.auth0.com/authorize?audience=myapp&response_type=token&client_id=AEznY1DMZyVH60GCqSUKvdscz53ajIL8&redirect_uri=https://fsw-capstone.herokuapp.com/) to get JWT token:
|account|password|
|-------|--------|
| CastingDirector@email.com | CastingDirector@email.com |
|CastingAssistant@test.com|G!!h+V++GPQ6MNn|
|ExecutiveProducer@test.com |ExecutiveProducer@test.com|

Or find the token in `setup.sh`

## Permissions
- post:actors: create a new actor
- patch:actors: modify an existing actor
- delete:actors: delete an actor
- post:movies: create a new movie
- patch:movies: modify an existing movie
- delete:movies: delete a movie  

## Roles
1. Casting Assistant
    - Can view actors and movies.
    - Has permissions:
        - None, get actors/movies are public endpoints
2. Casting Director
    - All permissions a Casting Assistant has and…
    - Add or delete an actor from the database
    - Modify actors or movies
    - Has permissions:
        - post:actors
        - patch:actors
        - delete:actors
        - post:movies
        - patch:movies
        - delete:movies
3. Executive Producer
    - All permissions a Casting Director has and…
    - Add or delete a movie from the database
    - Has permissions:
        - post:actors
        - delete:actors
        - post:movies
        - delete:movies
        
# Unit Tests
- All the tests were implemented in test_app.py:
```
dropdb casting_test
source setup.sh
python test_app.py
```

# Tech Stack
This is the full tech stack for this application.

## Operating system
I wrote this application using macOS Catalina 10.15.7. It should work on most UNIX-based Operating Systems.
All dependencies can be installed using either the `pip` package manager or the brew package manager.

## Web server
The web server technology I used is Flask.
I am using Flask, Flask CORS for Cross-Origin Resource Sharing, and gunicorn for Heroku deployment.

## Database Management
I am using PostgreSQL 13.1 for the Database system. For integration with flask and python, I am using SQLAlchemy and Flask-SQLAlchemy.
I am using Flask-Migrate to manage database versions. Then I'm using alembic for the actual versioning scheme. Finally, I'm using `psycopg2` to manage the database upgrades.

## Script interpreter
I am using Python 3.7 As well as the following python modules:
- pycodestyle for codestyle
