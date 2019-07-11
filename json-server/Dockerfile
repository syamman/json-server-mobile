#
# Dockerfile for json-server
#

FROM alpine

WORKDIR /data

RUN set -xe \
    && apk add --no-cache nodejs nodejs-npm \
    && npm install -g json-server \
    && rm -rf /tmp/npm* /var/cache/apk/*

# 2nd Stage

FROM nginx:latest

COPY nginx/default.conf /etc/nginx/conf.d/

RUN rm -rf /usr/share/nginx/html/*

COPY --from=builder ./data /usr/share/nginx/html

ENTRYPOINT ["json-server"]
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
