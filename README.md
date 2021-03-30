# CastingAgency
Udacity Full Stack Developer Course Final Project

This API lets Casting Assistants, Casting Directors, Executive Producers read, add, change and delete movies and actors.

# Heroku
The App is deployed on Heroku on the following link:https://fsw-capstone.herokuapp.com/

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

The Logininformation to update the JWT are as follows:
- CastingDirector@email.com / CastingDirector@email.com 
- CastingAssistant@test.com / G!!h+V++GPQ6MNn
- ExecutiveProducer@test.com / ExecutiveProducer@test.com

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