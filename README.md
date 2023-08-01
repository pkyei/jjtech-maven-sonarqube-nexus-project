## Install Nexus Repository Manager
- create ec2 intsnace, select linux2 OS, intance type: t2.medium and get userdata from link below. 
- open port 8081 on secuirty group
- https://github.com/awanmbandi/maven-nexus-project-eagles-batch/blob/maven-nexus-install/nexus-install.sh
- access nexus on browser with PUBLIC_IP:8081
- click on sign in on top right corner
- username is "admin" : 
- ssh into nexus server and navigate to path from step above to get password: cat /opt/nexus/sonatype-work/nexus3/admin.password
- copy default password and paste in password section on nexus and sign in
- when prompted to customise new password, use: "admin", 
- Click on disable anonymous access and then Finish.
- 
 

## Install Apache Maven
- Create a linux2 instance (ensure to not select the 2023 linux ami) with t2.micro type. 
- ssh into the instance and follow the link below for installation setup.
- install tree with command: sudo yum install tree -y
- https://github.com/awanmbandi/maven-nexus-project-eagles-batch/blob/maven-nexus-install/maven-install.md

## Maven commands
1. clone the source code from repository where it is stored.
2. cd into the cloned folder
3. cd in the javawebapp folder where the source code for the app is found prior to start running maven commands.
4. Run the following `maven`/`mvn` commands to validate/package/deploy your app artifacts remotely
   - `mvn validate`   (validate the project is correct and all necessary information is available.)
   - `mvn compile`    (compile the source code of the project and craetes a target directory)
   - `mvn test`       (run tests using a suitable unit testing framework. These tests should not require the code be packaged or deployed.)
   - `mvn package`    (take the compiled code and package it in its distributable format, such as a WAR/JAR/EAR.)
   - `mvn verify`     (run any checks to verify the package is valid and meets quality criteria.)
   - `mvn install`    (install the package into the local repository, for use as a dependency in other projects locally.)

## Install SonarQube
- Launch ec2-instance with OS: ubuntu 20.04, type:t2.medium
- Security group should allow port 9000 for inbound traffic
- https://github.com/awanmbandi/eagles-batch-devops-projects/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
- Access sonarqube on port PUBLIC_IP:9000
- click login and user username:admin and password:admin

## Configure Nexus Repository 

Series of tutorial code snippets for use
#Maven publish tutorial steps
Publishing artifact to Nexus snapshot and release repo using maven.

1. Create a snapshot repo using nexus, or use default coming in out of the box. DEFAULT 
2. Create a release repo using nexus, or use default coming out of the box. DEFAULT
3. Create a group repo having both release, snapshot and other third party repos. or use default coming out of the box.
4. Navigate to vsCode and in the settings.cml file,
- check to ensure your username and paswword for nexus is admin:admin on line 32 & 33.
- update nexus repository urls with the current IP of nexus server on line 63 and 74 of settings.xml
- update url for sonarqube on line 86  in the settings.xml file.
- update nexus url in pom.xml file on line 57 and 61
5. Go settings.xml under <MAVEN_INSTALL_LOCATION>\apache-maven-3.6.0\conf or C:\Users\<USER_NAME>\.m2  or mkdir ~/.m2
6. Create/Move profiles named snapshot and release in settings.xml in `~/.m2` (can be done in pom.xml as well)
7. Add server user name and pwd in setting.xml (Encrypted recommended).
8. Edit pom.xml and add repository and snapshot repository in distribution management tag DEFAULT/DONE
9. Mark id should match in step 7 with server id of settings.xml, UPDATE NEXUS IP
10. Run the following `maven`/`mvn` commands to validate/package/deploy your app artifacts remotely
   - `mvn validate`   (validate the project is correct and all necessary information is available.)
   - `mvn compile`    (compile the source code of the project)
   - `mvn test`       (run tests using a suitable unit testing framework. These tests should not require the code be packaged or deployed.)
   - `mvn package`    (take the compiled code and package it in its distributable format, such as a WAR/JAR/EAR.)
   - `mvn verify`     (run any checks to verify the package is valid and meets quality criteria.)
   - `mvn install`    (install the package into the local repository, for use as a dependency in other projects locally.)
   - `mvn deploy`     (done in an integration or release environment, copies the final package to the remote/SNAPSHOT repository 
                      for sharing with other developers and projects.)

11. Change the version from 1.0-Snapshot to 1.0
12. Run `mvn deploy` to deploy to Snapshot Repo or `mvn clean deploy -P release`, to deploy it to Release Repo

## Maven Lifecycle Phases
- https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#a-build-lifecycle-is-made-up-of-phases


##############################

mvn sonar:sonar \
  -Dsonar.projectKey=JavaProject \
  -Dsonar.host.url=http://3.92.198.127:9000 \
  -Dsonar.login=283258f8fc205fc88918a943c72d4f76afe5d582
