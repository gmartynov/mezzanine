ITS JUST A TRAINING NOOB CI/CD

PREPARE AND MAKE LOCAL TESTS:
1. Fork github project - Done
2. Run and check on local server - Done
3. Edit - Done
 3.1 created db (default params) and user root
 3.2 created project name "start"
4. Make nginx proxy pass config - Done
5. Tested - it works - Done

######
APP WITH REPO WAS FORKED, BUT WAS USELESS ACTION ATM, CAUSE ANYWAY APP STARTING ONLY AFTER PIP3 INSTALL MEZZANINE, CREATING PROJ AND ACTIONS WITH MANAGE.PY
SETTINGS.PY CAN BE USED TO IMPORT SETTINGS (MIGRATE)
DONT KNOW HOW TO IMPORT ALREADY CREATED DB FROM LOCAL TESTS
######

CI/CD
0. git clone to workspace - Done
1. PREPARE REMOTE MACHINE - install nginx and docker and copy remote nginx config. - Done
2. RUN SOME CODE AUTOTESTS IN JENKINS WORKSPACE [FAKE-TESTED AT REMOTE MACHINE BECAUSE OF BAD PYTHON ON LOCAL - ### NOT TESTED AT REMOTE TOO :D] - Done
3. BUILD DOCKER IMAGE WITH DOCKERFILE AND PUSH TO HUB - Done
4. RUN DOCKER IMAGE ON REMOTE MACHINE - Done
5. CHECK REMOTE IP 192.168.1.63:8000 - itworks

######
AFTER CI/CD IS COMPLETE, APP IS ACCESSIBLE AT REMOTE MACHINES IP
THERES 2 NGINX CONFS WITH REV PROXY:
1. REMOTE CONF - FROM REMOTE MACHINE IP -> TO CONTAILER IP
2. CONTAIN CONF - FROM CONTAINER IP -> TO CONTAINER LOOPBACK
CRAPPY BUT IT WORKS :DD
######

######
LATER MAYBE
1. BUILD AND RUN PY APP FROM FORKED ORIGIN, NOT PIP3
2. NEW DB CREATE IN CONTAINER WITH VARS OR SMTH
3. DB SAVE TO VOLUME
4. TRY WITH COMPOSE
5. MOVE TO KUBER

#######
DOCKER, JENKINS AND NGINX CONF FILES -> IN NAMED FOLDERS

REPEAT DOCKERFILE HERE->
FROM ubuntu:18.04
RUN  apt-get update -y && apt-get install python3.6 git nginx python3-pip -y \
&& git clone https://github.com/gmartynov/mezzanine.git ~/mez \
&& cp ~/mez/nginxconf/mezan-container.conf /etc/nginx/conf.d/ \
&& pip3 install mezzanine && mezzanine-project --settings ~/mez/start/start/settings.py start2
RUN echo "service nginx start && cd /start2 && python3.6 manage.py migrate && python3.6 manage.py runserver" \
> /tmp/runstart.sh && chmod +x /tmp/runstart.sh
ENTRYPOINT /tmp/runstart.sh
