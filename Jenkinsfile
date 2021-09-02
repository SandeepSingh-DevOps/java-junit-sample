pipeline{
    agent any

     tools {
        maven "maven-3"
    }
stages {
    
    
    stage("Build Code"){
            steps{
                sh "mvn clean package"
            } 
    }     
     stage('SonarQubr test') {
        steps{
            withSonarQubeEnv('My_Sonarqube') {
                    sh 'mvn sonar:sonar'
                }    
        }
    }
    
     stage("Deploy Code"){
            steps{
                sshagent(['ubuntu']) {
                sh "scp -o StrictHostKeyChecking=no target/*.jar  ubuntu@13.236.87.62:/var/lib/tomcat9/webapps"
                }
              }
     }
 }
}
