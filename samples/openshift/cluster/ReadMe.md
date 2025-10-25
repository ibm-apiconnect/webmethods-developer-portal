* Create a new project

  `oc new-project dpocluster`

* Create registry secret for containers.webmethods.io

  'oc create secret docker-registry regcred \
  --docker-server=ibmwebmethods.azurecr.io \
  --docker-username=myuser \
  --docker-password=mypassword'

* Link the secret to your service account (e.g., default)

  'oc secrets link default regcred --for=pull'

* Create and register a elasticsearch service of type ClusterIP

  `oc create -f es-svc.yaml -n dpocluster`

* Create a stateful set with 3 replicas of elasticsearch of version 8.17.3

  `oc create -f elasticsearch.yaml -n dpocluster`

* Create and register a service of type ClusterIP for devportal server

  `oc create -f devportal-svc.yaml -n dpocluster`

* Create a stateful set with 3 replicas of devportal of version 11.1

  `oc create -f devportal.yaml -n dpocluster`

* Create and register a loadbalancer service to expose Http/Https ports

  `oc create -f devportal-lb.yaml -n dpocluster`

* Create a Route to access the application outside of Openshift cluster

  `oc create -f devportal-route.yaml -n dpocluster`
