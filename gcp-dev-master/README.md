
# Google Cloud Platform - Development Container

This container is based off [Google Cloud SDK](https://hub.docker.com/r/google/cloud-sdk/).

It also includes additional software and libraries so it can act as a local Google Cloud Platform development container (in particular to enable it to run as a fully functional Google App Engine environment).

## Build this container

```
docker build -t gcp-dev .
```

## Start this container

You can modify these parameters to suit your dev environment.

The key points here are:

- `$PWD` :: Will be mounted to `/usr/src/dev` in the container, make sure you run the docker command from a local folder you'd like to mount
- Assumes you have a GCP Auth container (`docker run -ti --name gcloud-config google/cloud-sdk gcloud auth login`)

```
docker run \
-it --rm \
-p 80:80 \
-p 40969:40969 \
-p 8000:8000 \
-p 8080:8080 \
-v "$PWD":/usr/src/myapp \
-w /usr/src/myapp \
--volumes-from gcloud-config \
gcp-dev bash
```

Key folders:

- `/google-cloud-sdk`
- `/usr/src/python-docs-samples`
- `/usr/src/dev`

## Develop and Debug using this container

From the container prompt `root@042b7e3cb4ba:/usr/src/dev#` ... you can do all sorts of things:

### See what's in your datastore

```
cd /usr/src/python-docs-samples/datastore/cloud-client && \
python tasks.py list
```

### More Info/Tips: Google App Engine - Python Quick Start

[Python Quickstart](https://cloud.google.com/appengine/docs/standard/python/quickstart)

```
cd /usr/src/python-docs-samples/appengine/standard/hello_world && \
dev_appserver.py --host 0.0.0.0 --port=8080 app.yaml


Starting API server at: http://localhost:40969
Starting module "default" running at: http://localhost:8080
Starting admin server at: http://localhost:8000

# quick python http server for testing
python -m SimpleHTTPServer 8080

cd /usr/src/dev/hello_word && \
dev_appserver.py --host 0.0.0.0 --port=8080 app.yaml
```
