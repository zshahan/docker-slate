Builds Slate source files into staticfiles and served with nginx

## Getting started
Ensure your project directory is like so
```
source/
Dockerfile
```
then issue a ```docker build .``` command.

After the build is finished, run with ```docker run ... IMAGE``` and nginx will start up serving ```/usr/share/nginx/html/```.
