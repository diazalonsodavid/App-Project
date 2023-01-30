# Example application in Python and Django

## Description
This application is developed in python using Django as framework. The only use it has is to serve as an example for testing with the SRE tools in the repository:

https://github.com/diazalonsodavid/app-project-devops

## Requirements
* Python 3.x
* Docker

## Installation
1. Clone the repository
git clone https://github.com/diazalonsodavid/App-Project


2. Build the Docker image
docker build -t app-project .

3. Run the Docker container
docker run -p 80:5005 project_name


4. Visit http://localhost in your web browser to access the application

## Use
For the correct functioning of the application it will be necessary to connect to a MySQL server whose parameters are set in the settings.py file located in core/settings.py

## Dockerfile
```Dockerfile
FROM python:3.9

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the default workdir
WORKDIR /usr/src/app

COPY requirements.txt .
# install python dependencies
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
EXPOSE 5005
# running migrations (with mysql required to execute migration manually)
# RUN python manage.py migrate


# gunicorn
CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]

```

