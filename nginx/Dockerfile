FROM nginx

COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY static.json /usr/share/nginx/html/static.json
RUN chmod +r /usr/share/nginx/html/static.json

