FROM nginx:1.17-alpine

RUN apk add --no-cache openssl

RUN mkdir -p /etc/nginx/templates

COPY default.conf.template /etc/nginx/
COPY options-ssl-nginx.conf /etc/nginx/
COPY hsts.conf /etc/nginx/
COPY nginx.sh /customization/

RUN chmod +x /customization/nginx.sh
EXPOSE 80

CMD ["/customization/nginx.sh"]