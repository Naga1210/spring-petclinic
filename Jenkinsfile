pipeline {
    agent {label 'spc'}

    stages {
        stage ('git checkout') {
            steps {
                git url:'https://github.com/Naga1210/spring-petclinic.git',
                branch:'main'
            }
        }
        stage ('build and scan') {
            steps {
                withCredentials([string(CredentialId:'sonar',variable:'Sonar_Token')]) {
                    withSonarQubeEnv('sonartoken') {
                        sh '''mvn package sonar:sonar \
                            -Dsonar.projectKey=Naga1210/spring-petclinic \
                            -Dsonar.orginization= Naga1210 \
                            -Dsonar.host.url=https://sonarcloud.io \
                            -Dsonar.login=$Sonar_Token'''
                    
                    }
                }
            }
        }
    }
}