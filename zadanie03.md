ZADANIE 1

docker inspect --format '{{json .Config.Labels}}' krystyna-kapelewska-frontend:v1
{"autor":"Krystyna Kapelewska","data":"2026-11-05","maintainer":"krystyna.kapelewska@example.com"}

docker inspect --format '{{json .Config.Labels}}' krystyna-kapelewska-frontend:latest
{"autor":"Krystyna Kapelewska","data":"2026-11-05","maintainer":"krystyna.kapelewska@example.com"}


docker history krystyna-kapelewska-frontend:v1
IMAGE          CREATED        CREATED BY                                      SIZE      COMMENT
ca42114c8876   17 hours ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      17 hours ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      17 hours ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      17 hours ago   RUN /bin/sh -c apk add --no-cache nodejs npm…   99.3MB    buildkit.dockerfile.v0
<missing>      17 hours ago   LABEL autor=Krystyna Kapelewska data=2026-11…   0B        buildkit.dockerfile.v0
<missing>      17 hours ago   LABEL maintainer=krystyna.kapelewska@example…   0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    RUN /bin/sh -c set -x     && apkArch="$(cat …   52.4MB    buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    RUN /bin/sh -c set -x     && addgroup -g 101…   5.75MB    buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ADD alpine-minirootfs-3.24.3-x86_64.tar.gz /…   9.08MB    buildkit.dockerfile.v0
PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker>

docker history krystyna-kapelewska-frontend:latest
IMAGE          CREATED        CREATED BY                                      SIZE      COMMENT
6cbafc9176ca   17 hours ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      17 hours ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      17 hours ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      17 hours ago   RUN /bin/sh -c apk add --no-cache nodejs npm…   99.3MB    buildkit.dockerfile.v0
<missing>      17 hours ago   LABEL autor=Krystyna Kapelewska data=2026-11…   0B        buildkit.dockerfile.v0
<missing>      17 hours ago   LABEL maintainer=krystyna.kapelewska@example…   0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    RUN /bin/sh -c set -x     && apkArch="$(cat …   52.4MB    buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      2 weeks ago    RUN /bin/sh -c set -x     && addgroup -g 101…   5.75MB    buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    ADD alpine-minirootfs-3.24.3-x86_64.tar.gz /…   9.08MB    buildkit.dockerfile.v0


Dlaczego w wyniku inspect widać tylko Twoją wartość?


Które warstwy pochodzą z obrazu bazowego, które z Twojego Dockerfile?
Te które posiadają 0B np. <missing>      17 hours ago   LABEL autor=Krystyna Kapelewska data=2026-11…   0B        buildkit.dockerfile.v0
<missing>      17 hours ago   LABEL maintainer=krystyna.kapelewska@example…   0B        buildkit.dockerfile.v0

Dlaczego niektóre mają rozmiar 0B?
Bo bazujemy na czymś, co już istnieje tak naprawdę - w sensie nie musimy tworzyć nowej operacji, zużywać zasobów , bo bazujemy na rzeczach już wcześniej w użyciu.

Dlaczego widać tylko Twoją wartość maintainer?


ZADANIE 2

Zawartosc build.txt:

Frontend:
Thu Nov  5 07:28:32 UTC 2026
Frontend2:
Thu Nov  5 07:28:32 UTC 2026

797e195672ee   zadanie2-frontend:v1   "/docker-entrypoint.…"   About a minute ago   Up About a minute         0.0.0.0:8081->80/tcp, [::]:8081->80/tcp       frontend2
928f33709d21   zadanie2-frontend:v1   "/docker-entrypoint.…"   2 minutes ago        Up 2 minutes              0.0.0.0:8080->80/tcp, [::]:8080->80/tcp       frontend

Dlaczego czas w build.txt jest taki sam w obu kontenerach i nie jest to czas ich uruchomienia?
Ponieważ są uruchomione z tego samego obrazu - jest to dokładnie czas powstania tego obrazu.

ZADANIE 3

/nginx/conf.d/default.conf
server {
    listen       80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

ODPOWIEDŹ: To domyślny katalog główny serwera WWW Nginx. Ma to związaek z tym, że łączymy się przez kontener - a w docker file była podana innna ścieżka.

ZADANIE 4


PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker> docker exec zadanie4 ls
bin
dev
docker-entrypoint.d
docker-entrypoint.sh
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker> docker exec zadanie4 ls /usr/share/nginx
html
PS C:\Users\krysia\metody_wirtualizacji_laby\projekt\breach-checker> docker exec zadanie4 ls /usr/share/nginx/html
50x.html
build.txt
index.html
script.js
style.css