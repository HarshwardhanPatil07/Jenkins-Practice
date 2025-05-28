For Code Refer the Repo https://github.com/HarshwardhanPatil07/jenkins-java-maven-app
Under which choose the AutomaticVersioning git Branch 

![alt text](/assets/SoftwareVersioning.png)

Automatic versioning 

1. from terminal to increment the maven project version (where next is written it gets updated to next version; parse used to divide into three parts)
```bash
mvn build-helper:parse-version versions:set \

-DnewVersion=\${parsedVersion.majorVersion}.\${parsedVersion.nextMinorVersion}\${parsedVersion.incrementalVersion} versions:commit
```

In CI/CD this command is basically included in code for automation in pom.xml file
In Stages create new stage 
![alt text](/assets/IncrementVersionJenkinsFile.png)


Store the value of version in array so that docker image gets update with the same variable(Parsing jenkins file and storing the value)

![alt text](/assets/ContainerVersion.png)
![alt text](/assets/DockerFileAutoVersion.png)