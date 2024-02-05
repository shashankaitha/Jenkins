# **Jenkins Pipelines**

While installing jenkins, jenkins username will be created

Login into master node and swith to jenkins and genrate ssh-keygen

Create the server from the AMI which was generated for JFrog-MAVEN-Sonarqube

Start the SonarQube if its stop state

docker ps -a

docker start <container_id>

## _Ports:_ ##

1. Sonarqube : 9000
2. Jfrog : 8081


## _GithubAccess:_ ##

1. Login into Jenkins Server
2. Go to Below path and add the credentials
 Dashboard >Manage Jenkins >Credentials >System>Globalcredentials (unrestricted) > Add Credentials
3. Kind (Username with Password) --> Add Username (Github Access) -->   Add Private key(Copy and paste ec2 pem key) --> Save
4. Add Created Jenkins Key to the Github repo

5. Disable Host Key Verification:
    ```
    Dashboard >> Manage Jenkins > Security > Git Host Key Verification Configuration >> No Verification >> Apply
6. ## _Integrate Jenkins with Sonarqube:_ ##
    Credentials for Jenkins
    ```
    Username: admin , password path (cat /var/lib/jenkins/secrets/initialAdminPassword)

    ```
    Credentials for sonarqube (Default Credentials)

    ```
    username: admin
    password: admin
    ```

    a. Login into the SonarQube server
        Administration > Security > Users > Administrator > generate token(Jenkins Token)

    b. Add the generated token into the jenkins


        Dashboard >Manage Jenkins >Credentials >System>Globalcredentials (unrestricted) > Add Credentials > Secret Text > ID (Sonarqube_jenkins token)


    c. Add Sonarqube servers in the jenkins

        Manage jenkins> system > Sonarqube Server > Add sonarqube > Add Name(kellydevops-SonarQube-DEV) and Server URl and select the credentials(Sonarqube_jenkins token)

    d. Add Webhook
        Administration > Configuration > Webhooks > Create


7. Create a pipeline
   ```
    Dashboard > All >  Enter an Item Name > Select MultiBranch   Pipeline > Ok

    Branch Sources > GIT > Add Repo > Credentials

    Scan Multibranch Pipeline Triggers

    Scan by Webhook > TriggerToken
    ```
