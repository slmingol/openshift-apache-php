# basic apache container with php on openshift
## Build locally with docker, then push to openshift registry
My payload was wiki.tar.gz which had all my site contents, replace that with your tar
You might also not want to land this index.html, feel free to remove it.
### Get oc token
```oc whoami -t```
### Get the url for registry
```oc get route docker-registry -n default```
### login to registry with docker
```docker login -u jmainguy -p 82pHug7j72tmyqPjTCn157JGXL9QV3as docker-registry-default.apps.example.com``` 
### Build image
```docker build -t=docker-registry-default.apps.example.com/web/example```
### Push image
```docker push docker-registry-default.apps.example.com/web/example```
### Deploy
```oc new-app web/example --name=example```
### Expose svc and route
```oc expose svc/example```