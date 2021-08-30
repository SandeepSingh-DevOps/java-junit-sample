pipeline{
    agent any

     tools {
        maven "maven-3"
    }
stages {
    
    stage('Clean Code') {
        steps{
          sh 'mvn clean'
        }
    }
    
    stage("Build Code"){
            steps{
                sh "mvn package"
            } 
    }     
     stage('SonarQubr test') {
        steps{
            withSonarQubeEnv('My_Sonarqube') {
                    sh 'mvn sonar:sonar'
                }    
        }
    }
    
      stage("Junit Code"){
            steps{
                sh "mvn clean test"
            } 
    }  

     stage("Deploy Code"){
            steps{
                sshagent(['ubuntu']) {
                sh "scp -o StrictHostKeyChecking=no target/*.war  ubuntu@52.62.253.168:/var/lib/tomcat9/webapps"
                }
              }
     }
 }
}
