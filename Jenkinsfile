pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    
    stages{
        stage ('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deploy to tomcat server'){         
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://3.110.142.220:8080/')], contextPath: null, war: '**/*.war'
            }
         
        }
    }
}
