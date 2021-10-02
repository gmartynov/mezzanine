DOCKERFILE
FROM ubuntu:latest
RUN apt update -y && apt install python3.6 git nginx -y 
RUN git clone https://github.com/gmartynov/mezzanine.git /
COPY ./mezanine/nginxconf/mezan-container.conf /etc/nginx/conf.d/
RUN echo "cd /mezzanine/start && python manage.py runserver" > /tmp/runstart.sh && chmod +x /tmp/runstart.sh
ENTRYPOINT /tmp/runstart.sh
