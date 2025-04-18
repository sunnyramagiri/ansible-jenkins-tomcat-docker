pipeline {
    agent any

    tools {
        maven 'maven' // Ensure this matches the Maven installation name in Jenkins
    }

    environment {
        TOMCAT_URL = 'http://54.177.189.36:9070/manager/text'     // this is tomcat url 
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/sunnyramagiri/ansible-jenkins-tomcat-docker.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [                      // install the plugin for Deploy to container nd go to plugin syntax and look deploy war
                    tomcat9(
                        credentialsId: 'tomcat',        // Jenkins credentials (username/password for Tomcat)
                        path: '',                       // Deploy to the root context or specify a different context path
                        url: "${TOMCAT_URL}"            // Manager URL must end with /manager/text
                    )
                ],
                war: 'webapp/target/webapp.war'         // Specify exact WAR file location
            }
        }
    }
}
