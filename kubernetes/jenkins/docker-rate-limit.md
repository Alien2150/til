Today I was faced by the lovely Docker-Rate issue:

```
 You have reached your pull rate limit. You may increase the limit by authenticating and upgrading ... 
```

But I was a bit suppprised because we do a Pro license and I thought it was correctly configured :) 
In this TIL I learned a lot more about the internals how docker works in Kubernetes / Jenkins.

1. docker.config is (not always) your friend. Docker.config will help you for client based authentication. But there might be cases when this is not being used (e.g other users). Instead use the Kubernetes "ImagePullSecrets" as described here: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
2. Jenkins - Kubernetes ImagePullSecrets will ONLY help you pulling the pod image specified in the spec file. This will NOT help in cases you run a "docker build command" inside your Jenkinsfile. To fix that use a service-account as described here: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#add-imagepullsecrets-to-a-service-account and use "serviceAccount" on the Kubernetes Agent (https://github.com/jenkinsci/kubernetes-plugin)

The final solution:

1. Create a registry secret: ```k create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=<NAME> --docker-password=<ACCESS_TOKEN or PASSWORD> --namespace <NAMESPACE>```
2. Edit / Create a service-account used for your Jenkins-builds. Attach imagePullSecrets: 
```
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: "2020-08-13T16:22:01Z"
  labels:
    app.kubernetes.io/component: jenkins-master
    app.kubernetes.io/instance: jenkins
    app.kubernetes.io/name: jenkins
    helm.sh/chart: jenkins-1.19.0
  name: jenkins
  namespace: cicd
  resourceVersion: "269807032"
  selfLink: /api/v1/namespaces/cicd/serviceaccounts/jenkins
  uid: ff1f48ff-af01-4549-82d7-2a7b38411bfa
imagePullSecrets:
- name: regcred
```
3. Assign the service-account to your pod.yaml (spec):
```
spec:
  serviceAccount: "jenkins"
  containers:
```
