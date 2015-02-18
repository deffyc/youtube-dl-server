youtube-dl-server
=================

Very spartan and opinionated Web / REST interface for downloading youtube videos onto a server. [`bottle`](https://github.com/bottlepy/bottle) + [`youtube-dl`](https://github.com/rg3/youtube-dl).

How to use this image
---------------------

###Run on host networking

This example uses host networking for simplicitly. Also note the `-v` argument. This directory will be used to output the resulting videos

```
sudo docker run -d --net="host" --name youtube-dl -v /home/kevin/youtube-dl:/youtube-dl kmb32123/youtube-dl-server
```

###Start a download remotely

Downloads can be triggured by supplying the `{{url}}` of the requested video through the Web UI or through the REST interface via curl, etc.

####HTML

Just navigate to `http://{{address}}:8080/youtube-dl` and enter the requested `{{url}}`.

####Curl

```
curl -X POST --data-urlencode "url={{url}}" http://{{address}}:8080/youtube-dl/q
```

Implementation
--------------

The server uses [`bottle`](https://github.com/bottlepy/bottle) for the web framework and [`youtube-dl`](https://github.com/rg3/youtube-dl) to handle the downloading. For better or worse, the calls to youtube-dl are made through the shell rather then through the python API.

This docker image is based on [`python:3-onbuild`](https://registry.hub.docker.com/_/python/) and consequently [`debian:jessie`](https://registry.hub.docker.com/u/library/debian/).
