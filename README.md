# An-NGINX

Creates a docker image with custom build of NGINX

## Usage

```
$ ./docker-nginx [version]
```

### Examples:

Download the master branch from Github and run:
```
$ ./docker-nginx
$ docker run -dp 3000:80 an-nginx:master
```

Download specific release from Github and run:
```
$ ./docker-nginx 1.22.3
$ docker run -dp 3000:80 an-nginx:1.22.3
```

