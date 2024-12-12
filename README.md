# Shared To-Do List Full Stack Web App

Demo Site: https://stl-demo.techdude101.com

## Technologies
- Frontend 
  - HTML5
  - CSS
  - JavaScript
  - Web Components
- Backend
  - Microservice - data service
  - Microservice - authentication & authorization service (coming soon)
  - Database - MySQL
- Proxy / Load Balancer
  - NGINX
- Deployment
  - docker


## Quickstart
`git clone --recursive https://github.com/techdude101/fullstack-shared-todo-list.git`  

### Development
`docker-compose -f docker-compose-dev.yaml up -d`  

URLs:  
- [frontend via nginx](http://localhost)  
- [dataservice via nginx](http://localhost/api/)  
- [frontend](http://localhost:8000)  
- [dataservice](http://localhost:8080)  

### Demo
1. Change the DB password for the root user in file:
  - db_password.txt  
  `sed -i "s/<changeme>/<new password>/g" db_password.txt`
2. Change the DB password for user todo_user in files:  
  - shared-todo-list-db/06_ADD_DB_USER.sql  
  - docker-compose-demo.yaml  
  ```
  new_pwd=<new password>
  sed -i "s/<changeme>/$new_pwd/g" shared-todo-list-db/06_ADD_DB_USER.sql
  sed -i "s/<changeme_todo_user>/$new_pwd/g" docker-compose-demo.yaml
  ```
3. Configure certbot
  - Add your email and domain name to the docker compose file `docker-compose-demo.yaml`
  - Change server_name in `proxy/nginx.conf` to match your domain name
  - Configure `ssl_certificate` & `ssl_certificate_key` in `proxy/nginx.conf`

  ```
  ssl_certificate     /etc/nginx/ssl/live/<your domain name>/fullchain.pem;
  ssl_certificate_key /etc/nginx/ssl/live/<your domain name>/privkey.pem;
  ```
4. Create & start the containers  
`docker-compose -f docker-compose-demo.yaml up -d`  