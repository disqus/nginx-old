FROM disqus/boilerplate:xenial

COPY image $IMAGE_ROOT
RUN build-parts "$IMAGE_ROOT/build.d"

# Setup nginx config
COPY etc /etc/

ENV PUBLIC_ROOT=$APP_ROOT/media \
    #PROXY_URL=unix:///run/disqus/web.sock
    PROXY_URL=http://app:8000

CMD [ \
    "dockerize", \
    "-template", "/etc/nginx/templates:/etc/nginx", \
    "-template", "/etc/nginx/sites-available/templates:/etc/nginx/sites-available", \
    "-template", "/etc/nginx/conf.d/templates:/etc/nginx/conf.d" \
    "-stdout", "/var/log/nginx/access.log", \
    "-stderr", "/var/log/nginx/error.log", \
    "nginx" \
]

EXPOSE 80 443

# CI docker is too old for this. Sigh.
#HEALTHCHECK --interval=1m --timeout=3s CMD curl -f http://localhost/server-status || exit 1
