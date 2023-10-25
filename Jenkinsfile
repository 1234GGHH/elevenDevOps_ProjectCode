pipeline {
    // add your slave label name
    agent { label 'slave_sever'}
    tools{
        maven 'maven'
    }
    stages {
        stage ('Checkout SCM') {

            steps {
			    checkout scm
            }
        }

        stage ('Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('deploy') {
                     
            steps {
               sshagent(['jenkins_tomcat']) {
                sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@16.171.238.85:/opt/tomcat9/webapps"
               }
            }
        }

        
    }
}
