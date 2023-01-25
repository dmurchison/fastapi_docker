# Setup for FastAPI and Docker

**In order to get this environment up and running smoothly please follow the instructions in the specified order.**


## CLI
  - `docker install`
  - `mkdir app_name`
  - `cd app_name`
  - `pip3 install pipenv`
  - `pipenv shell`
  - `exit`


## Pip Environment
### `./Pipfile`
  ```pip
    [[source]]
    url = "https://pypi.org/simple"
    verify_ssl = true
    name = "pypi"

    [packages]
    uvicorn = "*"
    fastapi = "*"

    [dev-packages]

    [requires]
    python_version = "3.9"
  ```
  - `pipenv install`
  - `uvicorn main:app`
  - `CNTRL + C`


## Docker
### `./Dockerfile`
  ```docker
    FROM python:3.9-alpine

    RUN pip install pipenv
    RUN mkdir -p /usr/src/app/

    WORKDIR /usr/src/app
    COPY Pipfile Pipfile.lock main.py ./

    RUN pipenv install --system

    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
  ```
  - `docker`
  - `docker build -t app_name_dock:latest .`
  - `docker run --name app_name_cont -p 8080:8080 app_name_dock:latest`


## FastAPI
### `./main.py`
  ```python
    from fastapi import FastAPI

    app = FastAPI()
        
    @app.get("/")
    def home():
        return {"Hello": "World"}
  ```
  - `CNTRL + C`

