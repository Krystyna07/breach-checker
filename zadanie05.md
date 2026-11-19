#zadanie 1

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose down
>> 
[+] down 6/6
 ✔ Container breach-checker-frontend-1 Removed                                                            1.1s
 ✔ Container breach-checker-backend-1  Removed                                                            0.1s
 ✔ Container breach-checker-backend-2  Removed                                                            0.1s
 ✔ Container breach-checker-backend-3  Removed                                                            0.2s
 ✔ Container breach-checker-db-1       Removed                                                            0.4s
 ✔ Network breach-checker_default      Removed                                                            0.4s
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose up -d --build
>> 
[+] Building 4.1s (23/23) FINISHED                                                                                                                               
 => [internal] load local bake definitions                                                                                                                  0.1s
 => => reading from stdin 1.10kB                                                                                                                            0.1s
 => [frontend internal] load build definition from Dockerfile                                                                                               0.1s
 => => transferring dockerfile: 340B                                                                                                                        0.0s
 => [backend internal] load build definition from Dockerfile                                                                                                0.1s
 => => transferring dockerfile: 207B                                                                                                                        0.0s
 => [frontend internal] load metadata for docker.io/library/nginx:alpine                                                                                    0.1s
 => [backend internal] load metadata for docker.io/library/python:3.12-slim                                                                                 0.1s
 => [frontend internal] load .dockerignore                                                                                                                  0.0s
 => => transferring context: 68B                                                                                                                            0.0s
 => [backend internal] load .dockerignore                                                                                                                   0.1s
 => => transferring context: 79B                                                                                                                            0.0s
 => [frontend 1/5] FROM docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698d2aed0606                              0.1s
 => => resolve docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698d2aed0606                                       0.1s
 => [frontend internal] load build context                                                                                                                  0.0s
 => => transferring context: 120B                                                                                                                           0.0s
 => [backend 1/5] FROM docker.io/library/python:3.12-slim@sha256:a6e34c598f2467ed0e9a8d349809fcd8b5c603269512df273a0bb1784edc11b1                           0.1s
 => => resolve docker.io/library/python:3.12-slim@sha256:a6e34c598f2467ed0e9a8d349809fcd8b5c603269512df273a0bb1784edc11b1                                   0.1s
 => [backend internal] load build context                                                                                                                   0.0s
 => => transferring context: 63B                                                                                                                            0.0s
 => CACHED [backend 2/5] WORKDIR /app                                                                                                                       0.0s
 => CACHED [backend 3/5] COPY requirements.txt .                                                                                                            0.0s
 => CACHED [backend 4/5] RUN pip install --no-cache-dir -r requirements.txt                                                                                 0.0s
 => CACHED [backend 5/5] COPY app.py .                                                                                                                      0.0s
 => [backend] exporting to image                                                                                                                            0.4s
 => => exporting layers                                                                                                                                     0.0s
 => => exporting manifest sha256:bc6793e08a58be89cf93254b59009dce966579ad9708c7cf5ae35786fa48a103                                                           0.0s
 => => exporting config sha256:a38612ef6a4e96bec18b8fe2ccf5a80c9213e290807d9ac5073d840c074fe81f                                                             0.0s
 => => exporting attestation manifest sha256:30a18f0df3041a57c5fd13a7e9537857914db8fe99282c906dc8a589cb53b5ce                                               0.1s
 => => exporting manifest list sha256:f5d8cd113f8a6dd37300d9ca6037cb5d7fcafb844504269193047512e1e3e479                                                      0.1s
 => => naming to docker.io/library/breach-checker-backend:latest                                                                                            0.0s
 => => unpacking to docker.io/library/breach-checker-backend:latest                                                                                         0.0s
 => CACHED [frontend 2/5] RUN apk add --no-cache nodejs npm && npm install -g htmlhint                                                                      0.0s
 => CACHED [frontend 3/5] COPY index.html style.css script.js /usr/share/nginx/html/                                                                        0.0s
 => CACHED [frontend 4/5] COPY nginx.conf /etc/nginx/conf.d/default.conf                                                                                    0.0s
 => CACHED [frontend 5/5] RUN htmlhint /usr/share/nginx/html/index.html                                                                                     0.0s
 => [frontend] exporting to image                                                                                                                           0.5s
 => => exporting layers                                                                                                                                     0.0s
 => => exporting manifest sha256:1268ee243c6d360fca21ed595e6e7341b106ed0d1cad4e5cb4b7812216e9edbf                                                           0.0s
 => => exporting config sha256:9b877e0e371508f5c15387669035534d3c455c84273970133593141d6943d1a4                                                             0.0s
 => => exporting attestation manifest sha256:5d74d43aff92ab74b4392e988919f3545b047e187e06887a11054fe6711a44c8                                               0.1s
 => => exporting manifest list sha256:9ca9c3dbdf0049cf072384efeccfc09bcf4b847de444b491d1a08fbacccc4600                                                      0.0s
 => => naming to docker.io/library/breach-checker-frontend:latest                                                                                           0.0s
 => => unpacking to docker.io/library/breach-checker-frontend:latest                                                                                        0.1s
 => [backend] resolving provenance for metadata file                                                                                                        0.0s
 => [frontend] resolving provenance for metadata file                                                                                                       0.0s
[+] up 5/5
 ✔ Image breach-checker-backend        Built                                                                                                                 4.8s
 ✔ Image breach-checker-frontend       Built                                                                                                                 4.9s
 ✔ Container breach-checker-frontend-1 Running                                                                                                               0.0s
 ✔ Container breach-checker-backend-1  Healthy                                                                                                               1.2s
 ✔ Container breach-checker-db-1       Healthy                                                                                                               0.7s
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose ps
>> 
NAME                        IMAGE                                                                     COMMAND                  SERVICE    CREATED              STATUS                        PORTS
breach-checker-backend-1    sha256:f6f756490b9c5bf00cea3b90eed137ca05b2a579649e551b459b8fb7e52ebf45   "python app.py"          backend    About a minute ago   Up About a minute (healthy)   5000/tcp
breach-checker-db-1         postgres:16-alpine                                                        "docker-entrypoint.s…"   db         About a minute ago   Up About a minute (healthy)   5432/tcp
breach-checker-frontend-1   sha256:c67edd1869b16ecfb254306edf91ebe03f19dfd94b47e757a645c78d5649c484   "/docker-entrypoint.…"   frontend   About a minute ago   Up About a minute             0.0.0.0:8080->80/tcp, [::]:8080->80/tcp

#zadanie 2

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose exec db psql -U breach -d breachdb -c "INSERT INTO leaked_hashes VALUES ('bc45408273d7e1914b741c3407b0b559764f7876');"
>> 
INSERT 0 1

PS C:\Users\krysia\Documents\GitHub\breach-checker> '{"hash":"bc45408273d7e1914b741c3407b0b559764f7876"}' | curl.exe -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
>> 
{"found":true}

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose down
[+] down 4/4
 ✔ Container breach-checker-frontend-1 Removed                                                            0.5s
 ✔ Container breach-checker-backend-1  Removed                                                            3.4s
 ✔ Container breach-checker-db-1       Removed                                                            0.4s
 ✔ Network breach-checker_default      Removed                                                            0.3s

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose up -d
[+] up 4/4
 ✔ Network breach-checker_default      Created                                                            0.1s
 ✔ Container breach-checker-db-1       Started                                                            1.3s
 ✔ Container breach-checker-backend-1  Healthy                                                            6.5s
 ✔ Container breach-checker-frontend-1 Started                                                            6.8s

PS C:\Users\krysia\Documents\GitHub\breach-checker> '{"hash":"bc45408273d7e1914b741c3407b0b559764f7876"}' | curl.exe -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
>> 
{"found":true}

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose down -v
[+] down 5/5
 ✔ Container breach-checker-frontend-1 Removed                                                            0.7s
 ✔ Container breach-checker-backend-1  Removed                                                            3.6s
 ✔ Container breach-checker-db-1       Removed                                                            0.4s
 ✔ Volume breach-checker_pgdata        Removed                                                            0.0s
 ✔ Network breach-checker_default      Removed                                                            0.4s
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose up -d
[+] up 5/5
 ✔ Network breach-checker_default      Created                                                                                                               0.1s
 ✔ Volume breach-checker_pgdata        Created                                                                                                               0.0s
 ✔ Container breach-checker-db-1       Healthy                                                                                                               6.5s
 ✔ Container breach-checker-backend-1  Healthy                                                                                                              11.7s
 ✔ Container breach-checker-frontend-1 Started                                                                                                              12.0s
PS C:\Users\krysia\Documents\GitHub\breach-checker> '{"hash":"bc45408273d7e1914b741c3407b0b559764f7876"}' | curl.exe -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
>> 
{"found":false}

Dlaczego skrót przetrwał down, a nie przetrwał down -v?
Ponieważ down -v usuwa również nazwy wolumenów zdefiniowane w docker.compose.yml. Stąd przy zwyklym down nie tracimy żadnych danych (bo zwyczajnie dalej jest połączenie z konkretnym wolumenie), a przy down -v już tak. 

Dlaczego po down -v w bazie znów są 89 skróty z próbki, choć cała baza została skasowana?
Ponieważ odtwarza baza init.sql była zapisana na bind mouncie

#zadanie 3

wynik docker compose ps z trzema replikami, 
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose up -d --scale backend=3
>> 
[+] up 6/6
 ✔ Container breach-checker-db-1       Healthy                                                           4.1s
 ✔ Container breach-checker-frontend-1 Running                                                           0.0s
 ✔ Container breach-checker-backend-1  Healthy                                                           4.6s
 ✔ Container breach-checker-backend-3  Healthy                                                           4.6s
 ✔ Container breach-checker-backend-4  Healthy                                                           4.6s

wynik nslookup backend, po kilka linii POST /check z logów sprzed i po restarcie frontendu 

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose exec frontend nslookup backend
>> 
Server:         127.0.0.11
Address:        127.0.0.11:53

Non-authoritative answer:

Non-authoritative answer:
Name:   backend
Address: 172.19.0.5
Name:   backend
Address: 172.19.0.3
Name:   backend
Address: 172.19.0.4

ntend-1  | 172.19.0.1 - - [19/Nov/2026:07:50:51 +0000] "POST /api/check HTTP/1.1" 200 16 "-" "curl/8.22.0" "-"
frontend-1  | 172.19.0.1 - - [19/Nov/2026:07:50:51 +0000] "POST /api/check HTTP/1.1" 200 16 "-" "curl/8.22.0" "-"
frontend-1  | 172.19.0.1 - - [19/Nov/2026:07:50:51 +0000] "POST /api/check HTTP/1.1" 200 16 "-" "curl/8.22.0" "-"
frontend-1  | 172.19.0.1 - - [19/Nov/2026:07:50:51 +0000] "POST /api/check HTTP/1.1" 200 16 "-" "curl/8.22.0" "-"


Dlaczego przed restartem frontendu ruch trafiał do jednej repliki?
Ponieważ w pierwszej kolejności nginx tłumaczy nazwę backend na adres przy swoim starcie, stąd przypisanie do jednej repliki. 

Dlaczego skalowanie byłoby niemożliwe, gdyby backend nadal miał ports: "5000:5000"?
Pojawiłby się wtedy "Error dependency backend failed to start" oraz "container breach-checker-backend-3 exited (1)". Wynika to z faktu iż na tym porcie może byc wyłacznie jeden kontener, w żadnym wypadku trzy.