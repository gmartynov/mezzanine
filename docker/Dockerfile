FROM ubuntu:18.04
RUN  apt-get update -y && apt-get install python3.6 git nginx python3-pip -y \
&& git clone https://github.com/gmartynov/mezzanine.git ~/mez \
&& cp ~/mez/nginxconf/mezan-container.conf /etc/nginx/conf.d/ \
&& pip3 install mezzanine && mezzanine-project --settings ~/mez/start/start/settings.py start2
RUN echo "service nginx start && cd /start2 && python3.6 manage.py migrate && python3.6 manage.py runserver" \
> /tmp/runstart.sh && chmod +x /tmp/runstart.sh
ENTRYPOINT /tmp/runstart.sh
