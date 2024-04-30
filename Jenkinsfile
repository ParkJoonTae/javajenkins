pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
	
    stages{
        stage("Cleanup Workspace"){
                steps {
                	cleanWs()
                }
        }

        stage("Checkout from SCM"){
	// 'github'는 전 단계에서 Jenkins Credentials에 정의 
                steps {
                	git branch: 'main', credentialsId: 'github', url: 'https://github.com/Ashfaque-9x/register-app'
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

	stage("Git status"){
            steps {
        	sh "git status"
            }
       }
   }
   
	stage("SonarQube Analysis"){
            steps {
                script {
                    withSonarQubeEnv(credentialId: 'jenkins-sonarqube-token'){
                        sh "mvn sonar:sonar"
                    }
                }
            }
       }
   }
}

