# python-gentoo

For using a modern version of python, nothing is better than gentoo. Python 2.7 is outdatd (debian, ubuntu). Life is too short for dealing with alpine and its compiation problems for scipy, xgboost, ... Here is a docker image for python based on gentoo.

# Usage in Dockfile
cat Dockerfile
```
FROM gobert42/python-gentoo
```

# Notes
* Free disk place, deleting pip cache folder:
```
RUN rm -rf /home/jacques/.cache/pip/*
```

* Add postgres support for python
```
RUN emerge dev-python/psycopg
```

# Release image
```
  docker push gobert42/python-gentoo:latest
```
