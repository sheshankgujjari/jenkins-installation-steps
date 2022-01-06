### PreRequisites

Login to Jenkins
First thing, we will login to our Jenkins account



Install GitHub Integration and Maven Plugins in Jenkins
To build Java project with maven we need to install some plugins like,

GitHub Integration Plugin
Maven Integration Plugin
To install plugins follow below steps

Navigate to Dashboard->> Manage Jenkins ->> Manage Plugin

Now search for “GitHub Integration Plugin” and click on Download now and install after restart.


once the plugins are downloaded successfully. So now click on Restart Jenkins checkbox.


Please wait while Jenkins is restarting

### JDK Jenkins Integration 

1. Find JDK path
```
$ readlink -f $(which javac)

$ readlink -f $(which java)
```

2. Navigate to Dashboard->> Manage Jenkins->> Global tool Configuration

3. Click on JDK->> Add JDK, Give a JDK name and provide your JAVA_HOME path where the JDK is present.

4. Enter Name **JDK**

5. Enter JAVA_HOME **/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-4.el8_5.x86_64**



### Maven Jenkins Integration 
1. Navigate to Dashboard->> Manage Jenkins->> Global tool Configuration

2. Click on Maven->> Add Maven, We can provide our Installed Maven path or we can also use Jenkins default one.In this case we are using Jenkins default Maven version.

3. Click on install automatically

4. Version which Jenkins choses is **3.8.4**







## Create Jenkins Job


Create Pipeline Job in Jenkins
Now we will create a new Pipeline Job in Jenkins, So, click on “New Item” on the Jenkins Dashboard as shown below.


Enter Job name and select “Pipeline”, Click OK.


Enter Project details in Jenkins Pipeline
Provide some description for the newly created job in General Section, Click on GitHub project and provide the GitHub URL.

you can use https://github.com/sheshankgujjari/simple-java-maven-app  with jenkinsfile


Now we will set the Build Triggers, Select Build whenever a SNAPSHOT and GitHub hook trigger for GITScm polling as triggers.


Now in Pipeline section click on drop down and select Pipeline script from SCM.


In SCM select Git and below it provide your Git repository URL **https://github.com/sheshankgujjari/simple-java-maven-app.git**where your project is located and Add your GitHub credentials if applicable.


By default Jenkins provide branch as Master but you can change it to dev, main, or to whatever your branch is.(if you don’t know you can check the branch by going to your GitHub repository OR by running git branch command on your shell).

Our branch is main branch so will change master to main


Now comes the most important part of your Project / Job configuration, Provide accurate path of your Jenkinsfile.


Click on Apply and Save.

#6. Jenkinsfile to Build Java Project using Maven in Jenkins Pipeline
Now we see how to write a Declarative Pipeline script to build java project using maven.

Why Declarative Pipeline ?

Declarative Pipeline is a latest method mostly used in now a day to write Pipeline rather that that typical way (Scripted) because Declarative provides new feature which can even be tested in Git for source control)

Below is Jenkinsfile to Build Java Project using Maven in Jenkins and genrate junit test report.

pipeline {
    agent any
    tools {
        maven "MAVEN"
        jdk "JDK"
    }
    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}

Note- Replace and add your workspace path in dir.


Now open your Jenkins Dashboard and click on your job, Now click on Build Now

you can see Jenkins Pipeline Build stages.

check the console output to check Jenkins pipeline logs.

We have covered How to Build Java Project using Maven in Jenkins Pipeline.
