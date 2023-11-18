pipeline {
    // add your slave label name
    agent { label 'jenkins-slave'}
    tools{
        maven 'maven-tool'
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
               sshagent(['tomcat_jenkins']) {
                sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@51.20.41.254:/opt/tomcat9/webapps"
               }
            }
        }

        
    }
}
