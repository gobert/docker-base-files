# gentoo

Base image for gentoo.

# Usage in Dockfile
cat Dockerfile
```
FROM gobert42/gentoo
```

# Usage notes

* Free disk place deleting portage tree
```
RUN rm /var/db/repos/gentoo/*
RUN rm -rf /var/cache/distfiles/*
RUN rm -rf /var/cache/binpkgs/*
```

# Release image
```
  docker push gobert42/gentoo:latest
```
