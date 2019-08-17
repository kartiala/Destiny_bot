# Shop tg bot
TG Bot for sales. 

# How to install and run
1) Open nginx conf file `nano nginx/sites-enabled/django` and set server IP in `location /admin` block.
2) Open bot env file  `nano bot/env` and set bot info:  
    - `BOT_TOKEN` token by TG bot father.
    - `WEB_HOOK` server IP where bot running.
    - `REF_BOT_URL` Your bot nick. For example, if your bot nick is `test_bot` this should be `t.me/test_bot?start=`
3) Create webhooks `cd bot; mkdir webhooks; cd webhooks; openssl genrsa -out webhook_pkey.pem 2048; openssl req -new -x509 -days 3650 -key webhook_pkey.pem -out webhook_cert.pem
`. Leave all fields blank, but when asked for `Common Name (e.g. server FQDN or YOUR name)` you should reply with the same value in you put in `WEB_HOOK` in `env` file.
   
4) Build all services: from root project path `docker-compose build`
5) Up all services `docker-compose up -d`
5) Create superuser for admin page: `docker-compose exec web python3 manage.py createsuperuser`
6) Go to `YOUR_SERVER_IP/admin/` and login. 

 
# Tests backend
1) Recomended use venv or virtualenv for better isolation.\
      Venv setup example: \
      `python3 -m venv myenv`\
      `source myenv/bin/activate`
2) Install requirements: `pip3 install -r requirements.txt`
3) Make sure you run Postgres `docker-compose up postgres`. 
4) Add to environ db info: `source env_l`
5) Then `python3 web/bot_back/manage.py test`
