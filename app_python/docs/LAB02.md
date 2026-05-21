# LAB 02

## Docker bests practices applied

- *.dockerignore*

This practice is very useful. In fact before reading the whole documentation
for this lab, I started it (*plus I'm new to docker so I didn't know about it*)
and when I pushed it my docker image size was **> 400Mb**. I knew something was off so I searched a figured out dockerignore could help and my image when from **400Mb** to **70Mb**.

- Non-root user

This practice really matters because from a security perspective it always better to implement least privilege.

## Image Information & Decisions

## Build & Run Process

- Terminal output from build process

```bash

docker build -t olaghost667/app_python:1.0.1 .

DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  1.714MB
Step 1/10 : FROM python:3.13-slim@sha256:664a24153d53a7a94fac6c52b1f2bb2283385df23135edf802fbf97a2cc64b36
 ---> 664a24153d53
Step 2/10 : WORKDIR /app
 ---> Using cache
 ---> 68415f59c855
Step 3/10 : COPY app.py requirements.txt /app/
 ---> Using cache
 ---> b31c4d86b38c
Step 4/10 : RUN pip install -r requirements.txt
 ---> Using cache
 ---> c9c1e97080cd
Step 5/10 : RUN groupadd -r appgroup && useradd -r -g appgroup appuser
 ---> Using cache
 ---> c406968beef7
Step 6/10 : RUN chown -R appuser:appgroup /app
 ---> Using cache
 ---> 47d9ee2713a6
Step 7/10 : USER appuser
 ---> Using cache
 ---> d02e79b4f8eb
Step 8/10 : ENV FLASK_APP=app.py
 ---> Using cache
 ---> 1a0f2417c5a6
Step 9/10 : EXPOSE 5000
 ---> Using cache
 ---> fd96d199135d
Step 10/10 : CMD ["python", "app.py"]
 ---> Using cache
 ---> 11398681f99b
Successfully built 11398681f99b
Successfully tagged olaghost667/app_python:1.0.1
```

- Terminal output showing container running

```bash
docker run -p 3000:5000 olaghost667/app_python:1.0.1

INFO:     Started server process [1]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:5000 (Press CTRL+C to quit)
INFO:     172.17.0.1:41316 - "GET / HTTP/1.1" 200 OK
INFO:     172.17.0.1:41316 - "GET /favicon.ico HTTP/1.1" 200 OK
```

- Terminal output from testing endpoints (curl)

```bash
curl 127.0.0.1:3000

{"service":{"name":"devops-info-service","version":"1.0.0","description":"DevOps course info service","framework":"Flask"},"system":{"hostname":"4b6171591c2d","platform":"Linux","platform_version":"#1 SMP PREEMPT_DYNAMIC Fri, 01 May 2026 15:49:22 +0000","architecture":"x86_64","cpu_count":8,"python_version":"3.13.13"},"runtime":{"uptime_seconds":129,"uptime_human":"0 hours, 2 minutes","current_time":"2026-05-21T11:35:18.472040","timezone":"UTC"},"request":{"client_ip":"172.17.0.1","user_agent":"curl/8.20.0","method":"GET","path":"/"},"endpoints":[{"path":"/","method":"GET","description":"Service information"},{"path":"/health","method":"GET","description":"Health check"}]}%                                                                          

curl 127.0.0.1:3000/health

{"status":"healthy","timestamp":"2026-05-21T11:35:28.388921","uptime_seconds":139}%
```

