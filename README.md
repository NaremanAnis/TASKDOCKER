###docker task
## Prerequisites:
- Docker Desktop ([Install](https://www.docker.com/products/docker-desktop))
- Docker Compose (included with Docker Desktop)
- Git ([Install](https://git-scm.com/downloads))
steps:
1.flask app
  from flask import Flask
import os
app = Flask(__name__)
@app.route('/')
def hello():
    message = os.getenv("APP_MESSAGE", "Hello, Docker!")
    return f"<h1>{message}</h1>"
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
2.Dependencies (requirements):
  flask
  psycopg2-binary
3.Nginx Configuration (in docker file)
  FROM nginx:alpine
  COPY index.html /usr/share/nginx/html
4.Nginx Landing Page: (we use html language)
  <h1>Free Palestine NAREMAN ANIS</h1>
  also we can add any thing else and we can add body to this page 
5. then we make docker configuration :
   5.1.Flask Dockerfile:
    FROM python:3.11-slim
    WORKDIR /app
    COPY requirements.txt .
    RUN python -m pip install --upgrade pip && \
     pip install --no-cache-dir -r requirements.txt
    COPY . .
    EXPOSE 5000
    CMD ["flask", "run", "--host", "0.0.0.0"]
   5.2.Docker Compose configuration:
     code in docker-compose.yml file
6. Local Deployment:
   build and run : docker-compose up -d --build
7. check logs from docker desktop container and visit ( http://localhost:5000/)
8.  also vist http://127.0.0.1:5000/ and http://192.168.1.14:5000/ to check and test them lso

   note :
   ngnix port is 80 and flask docker port is 5000
   
  
