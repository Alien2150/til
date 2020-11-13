Our Jenkins CI System was down due to an issue with Jenkins Update Center: https://twitter.com/jenkinsci/status/1326994705230393344
This was causing issues of Jenkins not being able to download the plugins anymore (This is a default behavior when deploying Jenkins using the Helm chart).

The solution:
* Build your own docker image (Copy the installPlugins into plugins.txt)
```
FROM jenkins/jenkins:lts-alpine
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN JENKINS_UC_DOWNLOAD=http://mirrors.jenkins-ci.org jenkins-plugin-cli --verbose -f /usr/share/jenkins/ref/plugins.txt
```
* Change the HELM Values:
** set: ```overwritePlugins: false
    installPlugins: {}
    master.overwritePluginsFromImage: true
    ```
** change the base image/tag: ```
image: "772592230491.dkr.ecr.eu-west-1.amazonaws.com/cicd/jenkins"
```

* Deploy
