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
            post {
                success {
                    echo "Archiving artifacts..."
                    archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }     
     stage('Quality test Code') {
        steps{
            withSonarQubeEnv('My_Sonarqube') {
                    sh 'mvn sonar:sonar'
                }    
        }
    }

     stage("Deploy Code"){
            steps{
                sshagent(['ubuntu']) {
                sh "scp -o StrictHostKeyChecking=no target/*.war  ubuntu@3.26.60.192:/var/lib/tomcat9/webapps"
                }
              }
     }
 }
}
