pipeline {
    // add your slave label name
    agent { label 'my_maven_slave'}
    tools{
        maven 'maven-test'
    }
    stages {
        stage ('Checkout_SCM') {

            steps {
          	    
	     checkout scm
            }
        }

        stage ('Maven_Build') {

            steps {
               sh 'mvn clean package'
            }
        }
        
        stage ('Deploy_Tomcat') {

            steps {
	      sshagent(['tomcat-web-server']) {
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@107.23.45.151:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
