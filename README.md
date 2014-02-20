Fig
===

[![Build Status](https://travis-ci.org/orchardup/fig.png?branch=master)](https://travis-ci.org/orchardup/fig)
[![PyPI version](https://badge.fury.io/py/fig.png)](http://badge.fury.io/py/fig)

Fast, isolated development environments using Docker.

Define your app's environment with Docker so it can be reproduced anywhere:

    FROM orchardup/python:2.7
    ADD . /code
    WORKDIR /code
    RUN pip install -r requirements.txt
    CMD python app.py

Define the services that make up your app so they can be run together in an isolated environment:

```yaml
web:
  build: .
  links:
   - db
  ports:
   - "8000:8000"
   - "49100:22"
db:
  image: orchardup/postgresql
```

**Note** When mapping ports in the format HOST:CONTAINER you may experience erroneous results when using a container port lower than 60. This is due to YAML parsing numbers in the format "xx:yy" as sexagesimal (base 60) for this reason it is recommended to define your port mappings as strings.

(No more installing Postgres on your laptop!)

Then type `fig up`, and Fig will start and run your entire app:

![example fig run](https://orchardup.com/static/images/fig-example-large.f96065fc9e22.gif)

There are commands to:

 - start, stop and rebuild services
 - view the status of running services
 - tail running services' log output
 - run a one-off command on a service

Fig is a project from [Orchard](https://orchardup.com), a Docker hosting service. [Follow us on Twitter](https://twitter.com/orchardup) to keep up to date with Fig and other Docker news.

Installation and documentation
------------------------------

Full documentation is available on [Fig's website](http://orchardup.github.io/fig/).

Running the test suite
----------------------

    $ script/test


