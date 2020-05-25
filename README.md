# runtime-tomcat-operator
Operator based on https://github.com/application-stacks/runtime-component-operator

Use openshift
```
OPERATOR_NAMESPACE=tomcat
WATCH_NAMESPACE=tomcat
oc new-project tomcat
```
Follow the instructions from https://github.com/application-stacks/runtime-component-operator/tree/master/deploy/releases/0.5.1

Create the ImageStream and add some images to the stream
```
oc create -f stream.yaml
oc tag docker.io/jfclere/tomcat tomcat-stream:latest --scheduled
```
Create the service for the KUBEPing clustering session replication
```
oc create -f service.yaml
```
Use quickstart-cr.yaml to start 2 replicas:
```
oc apply -f quickstart-cr.yaml
```
Use oc get routes to check the URL
```
[jfclere@pc-6 runtime-tomcat-operator]$ oc get routes
NAME      HOST/PORT                                     PATH      SERVICES   PORT       TERMINATION   WILDCARD
tomcat    tomcat-tomcat.apps.jclere.rhmw-runtimes.net             tomcat     8080-tcp                 None
```
Test via curl or browser: (I am using my demo webapp)
```
curl -v http://tomcat-tomcat.apps.jclere.rhmw-runtimes.net/demo
```
