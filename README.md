This README explains on how to install MediaWiki and mariadb with the below requirements:

https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Red_Hat_Linux

1. Create a Docker image out of the Dockerfile that's available in the repo. For this assignment, as the requirements are as above, I have created the dockerfile and published the image in Docker Hub. The image is available in Docker hub as below:

        docker.io/rishikbsr/thoughtworks-mediawiki:1.0.1

2. Now, you can proceed with installing the Helm Chart. In this, I have published mediawiki using mediawiki.isense.qa.forge.connected.honeywell.com as the certs were available in "isense-tls" secret. (Modify this as per your requirement)

3. You can install the helm chart using helm install. The mariadb has a PVC and PV while mediawiki has Configmap that's used to mount the LocalSettings.php

4. Initially disable ConfigMap by commenting the deployment.yaml(post helm installation/preinstallation, but postinstallation is easy) not to include configmap of Localsetting.php, as during installation, you will get LocalSettings.php file. Then include that in the Localsettings.php configmap and uncomment the lines. That's it, WE ARE GOOD TO GO !

5. Our Mediawiki is set up and ready !! Hurray !!!