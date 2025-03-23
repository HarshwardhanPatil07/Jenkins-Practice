# Running the Jenkins Container

Start the Jenkins container with the following command:

```bash
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

Verify that the container is running:

```bash
docker ps
```

# Accessing the Jenkins Container

To interact with the container:

Open a Bash session:

```bash
docker exec -it <container_id> bash
```

Replace <container_id> with your actual container ID.

Retrieve the initial admin password:

```bash
cat /var/jenkins_home/secrets/initialAdminPassword
```

Exit the container:

```bash
exit
```

# Installing Node.js and NPM in the Jenkins Container

To install Node.js and NPM, follow these steps:

Access the container as the root user:

```bash
docker exec -u 0 -it <container_id> bash
```

Update package lists:

```bash
apt update
```

Install curl:

```bash
apt install curl
```

Download the NodeSource setup script for Node.js 20.x:

```bash
curl -sL https://deb.nodesource.com/setup_20.x -o nodesource_setup.sh
```

Run the setup script:

```bash
bash nodesource_setup.sh
```

Install Node.js:

```bash
apt install nodejs
```

# Configuring a Jenkins Job to Verify Node.js

To confirm that Node.js and NPM are properly installed, create a Jenkins job:

Create a new freestyle job.

Add a Build Step:

Choose "Execute shell".

Enter the following command to check the installed NPM version:

```bash
npm --version
```

Integrate Maven by using the "Invoke top-level Maven targets" option with Maven 3.9.

1. Install Nodejs from plugins 

2. Go in Tools and add Nodejs

3. now you can go to job build steps and add nodejs below maven 

4. you can do source code management in your job by using the git. 

5. Add the repository url and then add jenkins and provide your credentials so jenkins can access the repo.


## How to Recover Password if the initialAdminPassword File Gets Deleted

### Reset the Admin Password by Disabling Security Temporarily

1. **Open a shell in your Jenkins container:**
    ```bash
    docker exec -it cd42f9560272 /bin/bash
    ```

2. **Open the Jenkins configuration file (`config.xml`) located in `/var/jenkins_home` using an editor (e.g., `vi`):**
    ```bash
    vi /var/jenkins_home/config.xml
    ```

3. **Locate the `<useSecurity>` tag and change its value from `true` to `false`:**
    ```xml
    <useSecurity>false</useSecurity>
    ```

4. **Save the file and exit the editor, then restart the container:**
    ```bash
    docker restart cd42f9560272
    ```

5. **Access Jenkins at `http://localhost:8080`. You should now be able to log in without a password. Once in, re-enable security by setting up a new admin user and password.**


## Attaching to Previous Volume for New Container by Killing the Older One

To attach to the previous volume for a new container by killing the older one, run the following command:

```powershell
PS C:\> docker run -p 8080:8080 -p 50000:50000 -d `
>> -v jenkins_home:/var/jenkins_home `
>> -v /var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts
```


## Docker in Jenkins: Pushing to Docker Hub

1. **Open a shell in your Jenkins container as the root user:**
    ```bash
    docker exec -u 0 -it cd42f9560272 bash
    ```

2. **Install Docker inside the Jenkins container:**
    ```bash
    curl https://get.docker.com/ > dockerinstall && chmod 777 dockerinstall && ./dockerinstall
    ```

3. **Adjust permissions for Docker socket:**
    ```bash
    ls -l /var/run/docker.sock
    srw-rw---- 1 root root 0 Mar 19 12:27 /var/run/docker.sock
    chmod 666 /var/run/docker.sock
    ls -l /var/run/docker.sock
    srw-rw-rw- 1 root root 0 Mar 19 12:27 /var/run/docker.sock
    ```

4. **Configure Jenkins:**
    - Add repository and credentials.
    - Add Maven 3.9.
    - In build steps, execute the following shell command to build the Docker image:
        ```bash
        docker build -t java-maven-app:1.0 .
        ```

5. **Build the Docker image:**
    - The Docker image is now built.

6. **Push the Docker image to Docker Hub:**
    ![Docker Image](/assets/Jenkins_DockerImage.png)
    ```bash
    docker build -t harshwardhan07/harshwardhan:jenkinsJMA-1.0 .
    docker login -u $USERNAME -p $PASSWORD
    docker push harshwardhan07/harshwardhan:jenkinsJMA-1.0
    ```

    - Successfully pushed.
    ![Docker-Hub_Repository](/assets/Docker-Hub_Repository.png)


Finally!! lol!
![JenkinsBuilds](/assets/JenkinsBuilds.png)


FreeStyle project over - - - - - - - - - - -



Pipeline

Script is written in groovy

GO ahead with pipeline in jenkins Dashboard

in definition select Pipeline script from SCM bcoz want to use git for script

now configure your git repo url, credentials, and your project branch

after that it will look in root folder for Jenkinsfile

![Pipeline_1st](/assets/Pipeline_1st.png)

URL for ENV Variables in Jenkins http://localhost:8080/env-vars.html/


Full Pipeline Successful
![fullPipelineStageView](/assets/fullPipelineStageView.png)
![Full_Pipeline](/assets/Full_Pipeline.png)

## MultiBranch Pipeline

Each branch (e.g., feature-branch, hotfix, release) can have its own pipeline execution.
Jenkins automatically detects new branches with Jenkinsfile and runs pipelines for them.
Useful for testing code changes before merging.
Different branches can have different Jenkinsfile configurations, allowing for unique build, test, and deployment steps.

1. select multibranch in new item in jenkins
2. select Branch Sources as git 
3. and in discover branches select Filter by name (with regular expression) which adds branch automatically when it gets added

![Multibranch_View](/assets/Multibranch_View.png)

You can Add Expression of BRANCH_NAME so it gets identified at build and deploy phase

![TypesOfJenkinsJobs](/assets/TypesOfJenkinsJobs.png)