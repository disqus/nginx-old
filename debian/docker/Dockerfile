FROM trevorj/boilerplate:xenial

COPY image $IMAGE_ROOT
RUN build-parts "$IMAGE_ROOT/build.d"

# Setup nginx config
COPY sites-available /etc/nginx/sites-available

RUN echo "daemon off;" >> /etc/nginx/nginx.conf && rm -f /etc/nginx/sites-available/default

ENV PUBLIC_ROOT=$APP_ROOT/media \
    #PROXY_URL=unix:///run/disqus/web.sock
    PROXY_URL=http://app:8000

CMD ["dockerize", "-template", "/etc/nginx/sites-available/default.tmpl:/etc/nginx/sites-available/default", "-stdout", "/var/log/nginx/access.log", "-stderr", "/var/log/nginx/error.log", "nginx"]

EXPOSE 80 443
HEALTHCHECK --interval=1m --timeout=3s CMD curl -f http://localhost/server-status || exit 1
