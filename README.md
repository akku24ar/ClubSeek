
# ClubSeek

ClubSeek is service that specializes in recommending bars based on user preferences of quality and occupancy. Clients can use the API to view available Bars and get recommendations based on their personal preferences. Bar Owners can use the API to perform CRUD operations on Bars and view clients assigned to their bar

## Quick Start
1. Install Docker. See [Docker Installation Instructions](https://docs.docker.com/get-docker/)

2. Clone into GitHub Repo with: 
```git clone https://github.com/radical-teach/minor-project-team-4.git```

3. Run `make run` in the root folder of the project
4. Install the [Postman API Collection](https://documenter.getpostman.com/view/16583544/UyrGBZmX) and follow API Documentation to interact with API endpoint

## API Documentation
API documentation is located on [Postman](https://documenter.getpostman.com/view/16583544/UyrGBZmX). 

## Testing 

- To run integration tests, run `make integrationtest` in the root folder of the project
- To run unit tests, run `make unittest` in the root folder of the project

## File Tree
📦 **YelpHelp**
┣ 📂 **.github**
┃ ┗ 📂 **workflows** - GitHub Workflows
┃ ┃ ┣ **integration.yml** - GitHub Action Integration Tests Workflow
┃ ┃ ┗ **unit.yml** - GitHub Action Unit Test Workflow
┣ 📂 **ClubSeek** - Python Code for ClubSeek Application
┃ ┣ 📂 **clubseek** - Poetry Project
┃ ┃ ┣ **api.py** - All API Endpoints for all CRUD Operations in Application
┃ ┃ ┣ **constants.py** - Schemas and DB Classes for API Request Schemas and SQLAlchemy
┃ ┃ ┣ **helpers.py** - Helper Functions for API Endpoints
┃ ┃ ┗ **main.py** - Initializes Flask API and connects to Database
┃ ┣ 📂 **tests**
┃ ┃ ┣ **test_integration_clubseek.py** - Integration Tests
┃ ┃ ┗ **test_unit_clubseek.py** - Unit Tests
┃ ┣ **poetry.lock** - Poetry Metadata File
┃ ┗ **pyproject.toml** - Poetry Dependency File
┣ 📂 **databaseInit** - Script to Initialize Database
┃ ┗ **init.sql** - Initialization Script for Database to create Users and Bars Table
┣ 📂 **dockerTestingFiles** - Docker Build and Compose Files for Unit and Integration File
┃ ┣ **Dockerfile** - Build File for Poetry Project with Developer Dependencies
┃ ┣ **docker-compose.integrationtest.yml** - Integration Test Docker Compose File
┃ ┗ **docker-compose.unittest.yml** - Unit Test Docker Compose File
┣ 📂 **secrets** - Location where secrets are stored and read from
┃ ┣ **application_credentials** - Credentials for AuthZ with API
┃ ┣ **db_password** - Password for DB 
┃ ┣ **db_root_password** - Root Password for DB
┃ ┗ **db_user** - Username for DB 
┣ **Dockerfile** - Main Docker Build File for ClubSeek Image
┣ **Makefile** - Makefile for command shortcuts
┗ **docker-compose.yml** - Main Docker Compose File for ClubSeek Application

## Technical Overview

The ClubSeek Application runs on Python and the uses the following packages:
- [Flask](https://pypi.org/project/Flask/): Python web application framework used for API Endpoints
- [SQLAlchemy](https://pypi.org/project/SQLAlchemy/): Used to connect and preform CRUD operations on MySQL Database
- [Flask-SQLAlchemy](https://pypi.org/project/Flask-SQLAlchemy/): extension for [Flask](https://palletsprojects.com/p/flask/) that adds support for [SQLAlchemy](https://www.sqlalchemy.org/) to an application
- [Flask-HTTPAuth](https://pypi.org/project/Flask-HTTPAuth/): Flask extension that provides Basic HTTP authentication for Flask routes
- [flask-expects-json](https://pypi.org/project/flask-expects-json/): JSON Schema Validation for API Requests
- [Werkzeug](https://pypi.org/project/Werkzeug/): Used for text hashing in AuthZ
- [get-docker-secret](https://pypi.org/project/get-docker-secret/): Used to Pull Docker Secrets in Container

Developer Dependencies:
- [pytest](https://pypi.org/project/pytest/) - Testing Framework for Unit Testing
- [requests](https://pypi.org/project/requests/) - HTTP library for Integration Testing

The Application Image is created with a [Dockerfile](https://github.com/radical-teach/major-project-group-4/blob/main/Dockerfile) and the MySQL Database as well as the application containers are declared in a the [docker-compose.yml](https://github.com/radical-teach/major-project-group-4/blob/main/docker-compose.yml) file.

## Features
### Docker Secrets
Docker Secrets are declared in the [secrets](https://github.com/radical-teach/major-project-group-4/tree/main/secrets) folder and is used to store Database and API Endpoint Credentials
### GitHub Actions
GitHub Actions are declared in the [.github/workflows](https://github.com/radical-teach/major-project-group-4/tree/main/.github/workflows) folder. The `main` branch is protected and GitHub Actions are used to ensure that all Unit Tests and Integration Tests have passed before a PR can be merged into `main`. 

GitHub Actions work by running Unit Testing and Integration Testing containers that are declared in [dockerTestingFiles](https://github.com/radical-teach/major-project-group-4/tree/main/dockerTestingFiles "dockerTestingFiles") and read their error codes to determine if tests have failed or passed