Our Jenkins CI System was down due to an issue with Jenkins Update Center: https://twitter.com/jenkinsci/status/1326994705230393344
This was causing issues of Jenkins not being able to download the plugins anymore (This is a default behavior when deploying Jenkins using the Helm chart).

The solution:
* Build your own docker image (Copy the installPlugins list into plugins.txt)
```
FROM jenkins/jenkins:lts-alpine
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN JENKINS_UC_DOWNLOAD=http://mirrors.jenkins-ci.org jenkins-plugin-cli --verbose -f /usr/share/jenkins/ref/plugins.txt
```
* Change the Helm chart values:
  * avoid plugin overwrites / installation on startup:
    ```
    overwritePlugins: false
    installPlugins: {}
    master.overwritePluginsFromImage: true
    ```
  * change the base image/tag: 
    ```
     image: "XXXXX/cicd/jenkins"
     tag: "latest"
    ```
* Deploy the new helm chart
