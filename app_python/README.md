# FastAPi web api

## Overview

This app have been build for the lab01 of the "Devops Core course". It give service and
system information and do health check for monitoring

## Prerequisites

```markdown
python 3.14.4
```

## Installation

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Running the Application

```bash
python app.py
# Or with custom config
PORT=4999 HOST 127.0.0.1 python app.py
 ```

## API Endpoints

- GET / - Service and system information
- GET /health - Health check

## Configuration

|HOST|PORT|
|--------|----------|
|Host ip|tcp port number|

## Docker

To use the containerized application you can build it locally yourself and then run it or pull it from **docker hub** and run it 

- Building the image locally

```bash
docker build -t olaghost667/app_python:1.0.1 .
```

- Running the image

```bash
docker run -p 3000:5000 olaghost667/app_python:1.0.1 
```

- Pulling the docker image

```bash
docker pull olaghost667/app_python:1.0.1
```

And then you can run it.


