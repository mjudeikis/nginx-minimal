# Minimal nginx OCP example

Sample with Alpine Linux as base image. Small container, about 6.7 MB size.


## Build image

To build the image with name minimal-nginx:

```
git clone https://github.com/mangirdaz/nginx-minimal.git
cd nginx-minimal
#create empty BC
oc new-build --binary --name nginx
#build
oc start-build nginx --from-file=. --follow
#deploy
oc new-app nginx --image-stream=nginx
#expose service
oc expose service nginx
#debuging 
oc debug dc/nginx


Build and push to secure registry:
#create secret
read -s DOCKERPASS
oc secrets new-dockercfg docker --docker-server=docker.io --docker-username=mangirdas --docker-password=$DOCKERPASS --docker-email=mangirdas@judeikis.lt
#link secret
oc secrets link builder docker
#start build
oc start-build test --from-file=.


Run external image:
oc import-image nginx-ext --from docker.io/mangirdas/nginx-hello-world --confirm
oc new-app nginx-ext --image-stream=nginx-ext

Other commands:
#get SA
oc serviceaccounts get-token default
#debuging 
oc debug dc/nginx

```
