An example of a simple flask application which runs an API end point which you can perform CRUD (Create, Read, Update and Delete) operations on a PostgreSQL DB back end.

The application is containerized using Docker containers and Docker compose to orchestrate the containers

The application runs in 3 containers 

- NGINX
- WEB (Flask app with a Gunicorn WSGI server)
- DB (PostgreSQL)

to use just perform the following bash commands on your terminal

clone repository `git clone https://github.com/pedrojunqueira/Flask-Nginx-PostgreSQL-on-Docker.git`

CD into the directory

`cd Flask-Nginx-PostgreSQL-on-Docker`

**Note** : You have to have [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) installed on your machine

``` bash
$ docker-compose up -d --build
$ docker-compose exec web python manage.py create_db
```
then access app on `http://localhost:1337/`

Database will be empty but to retrieve data

`http://localhost:1337/cars`

To create a new record

Make a post request to the `http://localhost:1337/cars` end point passing a json data on the payload if you are using python requests

``` py
# example post method
import requests
import json

url = "http://localhost:1337/cars"

payload = {"name": "Mercedes Benz", "model": "C63", "doors": 4}
headers = {
  'Content-Type': 'application/json'
}

response = requests.post(url, headers=headers, data=json.dumps(payload))

print(response.text.encode('utf8'))

```

or you can just use postman

to bring container down

``` bash 
docker-compose down -v
```