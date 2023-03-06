pipeline {
    agent any
    environment{
        PATH = "/opt/maven/bin:$PATH"
    }
    
    tools {
        maven 'maven'
    }
    stages{
        stage('clone'){
            steps{
            git credentialsId: 'git-creds', url: 'https://github.com/awskumar007/devOpsWeb'
           }
        }
        stage('Build'){
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

        stage ('Deploy2tomcat'){
        steps {
            deploy adapters: [tomcat9(credentialsId: 'tomcat-deployer', path: '', url: 'http://3.110.212.6:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
