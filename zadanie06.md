
Przy lower.():

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose exec backend pytest -v
====================================================================== test session starts =======================================================================
platform linux -- Python 3.12.15, pytest-8.4.2, pluggy-1.7.0 -- /usr/local/bin/python3.12
cachedir: .pytest_cache
rootdir: /app
collected 9 items                                                                                                                                                

tests/test_check.py::test_leaked_hash_is_found PASSED                                                                                                      [ 11%]
tests/test_check.py::test_unknown_hash_is_not_found PASSED                                                                                                 [ 22%]
tests/test_check.py::test_missing_hash_field PASSED                                                                                                        [ 33%]
tests/test_check.py::test_plaintext_password_is_rejected PASSED                                                                                            [ 44%]
tests/test_check.py::test_big_letters PASSED                                                                                                               [ 55%]
tests/test_check.py::test_small_letters PASSED                                                                                                             [ 66%]
tests/test_check.py::test_too_short_hash_is_rejected PASSED                                                                                                [ 77%]
tests/test_check.py::test_invalid_hex_characters_are_rejected PASSED                                                                                       [ 88%]
tests/test_check.py::test_invalid_request_body_is_rejected PASSED                                                                                          [100%]

======================================================================= 9 passed in 0.31s 

Po usunieciu lower:

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose exec backend pytest -v
====================================================================== test session starts =======================================================================
platform linux -- Python 3.12.15, pytest-8.4.2, pluggy-1.7.0 -- /usr/local/bin/python3.12
cachedir: .pytest_cache
rootdir: /app
collected 9 items                                                                                                                                                

tests/test_check.py::test_leaked_hash_is_found PASSED                                                                                                      [ 11%]
tests/test_check.py::test_unknown_hash_is_not_found PASSED                                                                                                 [ 22%]
tests/test_check.py::test_missing_hash_field PASSED                                                                                                        [ 33%]
tests/test_check.py::test_plaintext_password_is_rejected PASSED                                                                                            [ 44%]
tests/test_check.py::test_big_letters PASSED                                                                                                               [ 55%]
tests/test_check.py::test_small_letters PASSED                                                                                                             [ 66%]
tests/test_check.py::test_too_short_hash_is_rejected PASSED                                                                                                [ 77%]
tests/test_check.py::test_invalid_hex_characters_are_rejected PASSED                                                                                       [ 88%]
tests/test_check.py::test_invalid_request_body_is_rejected PASSED                                                                                          [100%]

======================================================================= 9 passed in 0.37s

Wyniki bez lower:

PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose exec backend pytest
====================================================================== test session starts =======================================================================
platform linux -- Python 3.12.15, pytest-8.4.2, pluggy-1.7.0
rootdir: /app
collected 9 items                                                                                                                                                

tests/test_check.py .........                                                                                                                              [100%]

======================================================================= 9 passed in 0.36s ======

testy nie wykryły usuniecia lower poniewz bez niego tak naprawde nie jestemsy w stanie stwierdzic wielkosci liter

#zadanie 2
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose stop db
>> 
[+] stop 1/1
 ✔ Container breach-checker-db-1 Stopped                                                                                                                      0.4s
PS C:\Users\krysia\Documents\GitHub\breach-checker> '{"hash":"7c4a8d09ca3762af61e59520943dc26494f8941b"}' | curl.exe -s -o blad.html -w "HTTP %{http_code}\n" -X POST http://localhost:8080/api/check -H "Content-Type: application/json" -d '@-'
>> 
HTTP 500
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose logs --tail 20 backend
>> docker compose restart backend
>> docker compose ps -a
>> docker inspect --format '{{.State.Status}} {{.State.ExitCode}}' breach-checker-backend-1
>> 
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:37:25] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:37:36] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:37:46] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:37:56] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:38:07] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:38:17] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:38:27] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:38:38] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:38:48] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:38:58] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:39:09] "GET /health HTTP/1.1" 200 -
backend-1  | 127.0.0.1 - - [26/Nov/2026 07:39:19] "GET /health HTTP/1.1" 200 -
[+] restart 0/1
 - Container breach-checker-backend-1 Restarting                                                                                                              0.6s
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED         STATUS                                     PORTS
breach-checker-backend-1    breach-checker-backend    "flask --app app run…"   backend    7 minutes ago   Up Less than a second (health: starting)   5000/tcp
breach-checker-db-1         postgres:16-alpine        "docker-entrypoint.s…"   db         7 minutes ago   Exited (0) 2 minutes ago                   
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   7 minutes ago   Up 7 minutes                               0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
running 0
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose ps -a
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED         STATUS                      PORTS
breach-checker-backend-1    breach-checker-backend    "flask --app app run…"   backend    7 minutes ago   Exited (1) 21 seconds ago   
breach-checker-db-1         postgres:16-alpine        "docker-entrypoint.s…"   db         7 minutes ago   Exited (0) 2 minutes ago    
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   7 minutes ago   Up 7 minutes                0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose ps -a
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED         STATUS                      PORTS
breach-checker-backend-1    breach-checker-backend    "flask --app app run…"   backend    8 minutes ago   Exited (1) 47 seconds ago   
breach-checker-db-1         postgres:16-alpine        "docker-entrypoint.s…"   db         8 minutes ago   Exited (0) 3 minutes ago    
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   8 minutes ago   Up 8 minutes                0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker inspect 677b5d767b51
[
    {
        "Id": "677b5d767b517624eced6f8a1756881905d837985e4face182bc49ee87e98443",
        "Created": "2026-11-26T07:31:54.107813994Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 3827,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2026-11-26T07:32:05.968143279Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:316b83b9cf2ed6802461422fdf774361285cca122087c94cba8fda7d22cc29a4",
        "ResolvConfPath": "/var/lib/docker/containers/677b5d767b517624eced6f8a1756881905d837985e4face182bc49ee87e98443/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/677b5d767b517624eced6f8a1756881905d837985e4face182bc49ee87e98443/hostname",
        "HostsPath": "/var/lib/docker/containers/677b5d767b517624eced6f8a1756881905d837985e4face182bc49ee87e98443/hosts",
        "LogPath": "",
        "Name": "/breach-checker-frontend-1",
        "RestartCount": 0,
        "Driver": "overlayfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "local",
                "Config": {}
            },
            "NetworkMode": "breach-checker_default",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "8080"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                0,
                0
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": null,
            "DnsOptions": null,
            "DnsSearch": null,
            "ExtraHosts": [],
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": null,
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/acpi",
                "/proc/asound",
                "/proc/interrupts",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/sys/devices/virtual/powercap",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "Storage": {
            "RootFS": {
                "Snapshot": {
                    "Name": "overlayfs"
                }
            }
        },
        "Mounts": [],
        "Config": {
            "Hostname": "677b5d767b51",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": true,
            "AttachStderr": true,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.31.8",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=1.0.2",
                "NJS_RELEASE=1",
                "ACME_VERSION=0.4.1"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "breach-checker-frontend",
            "Volumes": null,
            "WorkingDir": "/",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "Labels": {
                "com.docker.compose.config-hash": "108ac1a9e932394e01630954c07794439545f2d42d2f0db1be99534f022ad11c",
                "com.docker.compose.container-number": "1",
                "com.docker.compose.depends_on": "backend:service_healthy:false",
                "com.docker.compose.image": "sha256:da0b4e4f15ac4d5ed78c1e8b88ab8152a76f4cc7118c1367485b2a587d1cc19a",
                "com.docker.compose.oneoff": "False",
                "com.docker.compose.project": "breach-checker",
                "com.docker.compose.project.config_files": "C:\\Users\\krysia\\Documents\\GitHub\\breach-checker\\docker-compose.yml,C:\\Users\\krysia\\Documents\\GitHub\\breach-checker\\docker-compose.override.yml",
                "com.docker.compose.project.working_dir": "C:\\Users\\krysia\\Documents\\GitHub\\breach-checker",
                "com.docker.compose.service": "frontend",
                "com.docker.compose.version": "5.7.0",
                "maintainer": "krystyna.kapelewska@example.com"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "SandboxID": "172988d1212abe71bcaf90812499b9f6ed33b6b37b2b74e36908b1e742744c87",
            "SandboxKey": "/var/run/docker/netns/172988d1212a",
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "8080"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "8080"
                    }
                ]
            },
            "Networks": {
                "breach-checker_default": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "breach-checker-frontend-1",
                        "frontend"
                    ],
                    "DriverOpts": null,
                    "GwPriority": 0,
                    "NetworkID": "4cb761ad2abd0d9e3d1c5b4dfe8da2c22c913b5a67ac85e4406dbca3a519782b",
                    "EndpointID": "92bcd05beab80fa31e42f676bc87f5ccc49965e8a9e1221e239e740e09c14399",
                    "Gateway": "172.19.0.1",
                    "IPAddress": "172.19.0.4",
                    "MacAddress": "a2:40:f3:76:f8:c5",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": [
                        "breach-checker-frontend-1",
                        "frontend",
                        "677b5d767b51"
                    ]
                }
            }
        },
        "ImageManifestDescriptor": {
            "mediaType": "application/vnd.oci.image.manifest.v1+json",
            "digest": "sha256:da0b4e4f15ac4d5ed78c1e8b88ab8152a76f4cc7118c1367485b2a587d1cc19a",
            "size": 2566,
            "platform": {
                "architecture": "amd64",
                "os": "linux"
            }
        }
    }
]
PS C:\Users\krysia\Documents\GitHub\breach-checker> 

See 'docker inspect --help' for more information
PS C:\Users\krysia\Documents\GitHub\breach-checker> docker compose ps
NAME                        IMAGE                     COMMAND                  SERVICE    CREATED         STATUS         PORTS
breach-checker-frontend-1   breach-checker-frontend   "/docker-entrypoint.…"   frontend   9 minutes ago   Up 8 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
PS C:\Users\krysia\Documents\GitHub\breach-checker>   


blad.html:

OperationalError
psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname

Traceback (most recent call last)
File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 1536, in __call__
    ) -> cabc.Iterable[bytes]:
        """The WSGI server calls the Flask application object as the
        WSGI application. This calls :meth:`wsgi_app`, which can be
        wrapped to apply middleware.
        """
        return self.wsgi_app(environ, start_response)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 1514, in wsgi_app
            try:
                ctx.push()
                response = self.full_dispatch_request()
            except Exception as e:
                error = e
                response = self.handle_exception(e)
                           ^^^^^^^^^^^^^^^^^^^^^^^^
            except:  # noqa: B001
                error = sys.exc_info()[1]
                raise
            return response(environ, start_response)
        finally:
File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 1511, in wsgi_app
        ctx = self.request_context(environ)
        error: BaseException | None = None
        try:
            try:
                ctx.push()
                response = self.full_dispatch_request()
                           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
            except Exception as e:
                error = e
                response = self.handle_exception(e)
            except:  # noqa: B001
                error = sys.exc_info()[1]
File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 919, in full_dispatch_request
            request_started.send(self, _async_wrapper=self.ensure_sync)
            rv = self.preprocess_request()
            if rv is None:
                rv = self.dispatch_request()
        except Exception as e:
            rv = self.handle_user_exception(e)
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
        return self.finalize_request(rv)
 
    def finalize_request(
        self,
        rv: ft.ResponseReturnValue | HTTPException,
File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 917, in full_dispatch_request
 
        try:
            request_started.send(self, _async_wrapper=self.ensure_sync)
            rv = self.preprocess_request()
            if rv is None:
                rv = self.dispatch_request()
                     ^^^^^^^^^^^^^^^^^^^^^^^
        except Exception as e:
            rv = self.handle_user_exception(e)
        return self.finalize_request(rv)
 
    def finalize_request(
File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 902, in dispatch_request
            and req.method == "OPTIONS"
        ):
            return self.make_default_options_response()
        # otherwise dispatch to the handler for that endpoint
        view_args: dict[str, t.Any] = req.view_args  # type: ignore[assignment]
        return self.ensure_sync(self.view_functions[rule.endpoint])(**view_args)  # type: ignore[no-any-return]
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 
    def full_dispatch_request(self) -> Response:
        """Dispatches the request and on top of that performs request
        pre and postprocessing as well as HTTP exception catching and
        error handling.
File "/app/app.py", line 38, in check
        return jsonify({"error": "pole 'hash' musi być skrótem SHA-1 (40 znaków hex)"}), 400
 
    # Pełny SHA-1 popularnego hasła łatwo odwrócić - w logu tylko początek
    print(f"check: hash={h[:5]}...", flush=True)
 
    conn = connect()
           ^^^^^^^^^
    try:
        with conn.cursor() as cur:
            # %s = parametr zapytania: wartość h nigdy nie staje się częścią kodu SQL
            cur.execute("SELECT EXISTS (SELECT 1 FROM leaked_hashes WHERE hash = %s)", (h,))
            found = cur.fetchone()[0]
File "/app/app.py", line 11, in connect
 
app = Flask(__name__)
 
def connect():
    # Dane połączenia przychodzą ze zmiennych środowiskowych ustawionych w docker-compose.yml
    return psycopg2.connect(
           
        host=os.environ["DB_HOST"],
        dbname=os.environ["DB_NAME"],
        user=os.environ["DB_USER"],
        password=os.environ["DB_PASSWORD"],
    )
File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
        kwasync['async'] = kwargs.pop('async')
    if 'async_' in kwargs:
        kwasync['async_'] = kwargs.pop('async_')
 
    dsn = _ext.make_dsn(dsn, **kwargs)
    conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    if cursor_factory is not None:
        conn.cursor_factory = cursor_factory
 
    return conn


Plik blad.html zawieral bezposredni kod z plikow, co w prawdziwej sytuacji byloby niedopuszczalne, poniewaz po pierwsze moglo by to doprowadzic do skopiowania roziwazan zastosowanych w produkcie, a po drugie mogloby po prostu grozic wyciekiem danych wrazliwych, albo metod testowania programu, ktorych znajomosc z pewnoscia polepsyzlaby sytuacje potencjalnego hakera.

ZADANIE 3

Wynik przed zmiana 

PS C:\Users\krysia\Documents\GitHub\breach-checker> curl http://localhost:8080/nginx.conf                                                                         
                                                                                                                                                                  
Security Warning: Script Execution Risk
Invoke-WebRequest parses the content of the web page. Script code in the web page might be run when the page is parsed.
      RECOMMENDED ACTION:
      Use the -UseBasicParsing switch to avoid script code execution.

      Do you want to continue?
    
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): y


StatusCode        : 200
StatusDescription : OK
Content           : {115, 101, 114, 118...}
RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 326
                    Content-Type: application/octet-stream
                    Date: Thu, 26 Nov 2026 07:56:30 GMT
                    ETag: "6afdf668-146"
                    Last-Modified: We...
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 326], [Content-Type, application/octet-stream]...}
RawContentLength  : 326


Dockerfile/frontend:
COPY index.html style.css script.js /usr/share/nginx/html/
