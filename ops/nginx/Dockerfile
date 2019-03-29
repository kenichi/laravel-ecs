FROM nginx:alpine

# replace nginx(100:101) with www-data(1000:1000)
ARG NAME=www-data
ENV NAME ${NAME}
RUN deluser nginx && \
    adduser -s /bin/sh -D -u 1000 -g '' ${NAME} ${NAME} && \
    chown -R www-data:www-data /var/cache/nginx

# remove default conf
RUN rm /etc/nginx/conf.d/default.conf

# add local conf
COPY nginx.conf /etc/nginx/nginx.conf

# fix perms
RUN mkdir -p /var/www && chown ${NAME}:${NAME} /var/www

CMD ["nginx"]
