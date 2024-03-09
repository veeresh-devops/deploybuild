pipeline {
    // add your slave label name
    agent { label 'slave-node'}
    tools{
        maven 'maven'
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
              sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war  ec2-user@13.234.59.236:/opt/tomcat9/webapps"
	      }
         }
        }
        
    }
}
