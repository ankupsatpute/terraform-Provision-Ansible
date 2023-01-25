@Library("demo") _
pipeline{
    agent any
    environment {
    PATH = "/opt/apache-maven-3.8.7/bin:$PATH"
    
     }
    
    stages{
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }
        
        
        stage('CheckOut'){
            steps{
                script{
               echo "Git Checkout Started"
                fetchCode.gitcheckout()
               echo "Git Checkout Completed"            
               }
            }
        }
       
         stage('Build'){
            steps{
                script{
                    buildCode.buildCode()
                }
            }
        }
        
        stage('SonarQube Analysis'){
            when{
                branch "develop"
            }
            steps{
                withSonarQubeEnv('sonarqube-8.9.10.61524'){
                  script{
                       sonarQube.sonarQube()
                   }
                }
            }
        }
        
       
        
        stage('CheckOut for PR'){
            when {
                branch "PR-*"
            }
            steps{
               script{
               echo "Git Checkout Started"
               fetchCode.gitcheckout2()
               echo "Git Checkout Completed"            
               }
            }
        }
         
     
    }
}
