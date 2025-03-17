# Jenkins

 docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

 docker ps

 docker exec -it 820ef2b7836e bash

 cat /var/jenkins_home/secrets/initialAdminPassword

 exit
## Installing NPM aand Node on jenkins container

docker exec -u 0 -it 820ef2b7836e bash // as root user

apt update

apt install curl

ls

curl -sL https://deb.nodesource.com/setup_20.x -o nodesource_setup.sh

bash nodesource_setup.sh

apt install nodejs

## Now in order to configure node in job I started freestyle job and given simple npm --version in execute as shell in Build Steps with Invoke top-level Maven targets with maven-3.9