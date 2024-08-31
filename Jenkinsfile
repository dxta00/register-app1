pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'maven3'
    }
   
    
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'master', credentialsId: 'github', url: 'https://github.com/dxta00/register-app1.git'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

        }

        stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
        stage("SonarQube Analysis"){
           steps {
	           script {
		           withSonarQubeEnv(credentialsId: 'Jenkins-sonarqube-token') {
                       sh "mvn sonar:sonar"
		               }
	            }	
            }
         }

       
   }	
}
