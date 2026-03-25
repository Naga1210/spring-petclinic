pipeline {
    agent {label 'spc'}
    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage ('git checkout') {
            steps {
                git url:'https://github.com/Naga1210/spring-petclinic.git',
                branch:'main'
            }
        }
        
        stage ('build and scan') {
            steps {
                withCredentials([string(credentialsId:'SONAR_TOKEN',variable:'SONAR_TOKEN')]) {
                    withSonarQubeEnv('sonar') {
                        sh ''' mvn clean package sonar:sonar \
                             -Dsonar.projectKey=Naga1210_spring-petclinic \
                             -Dsonar.organization=Naga1210 \
                             -Dsonar.host.url=https://sonarcloud.io \
                             -Dsonar.login=$SONAR_TOKEN '''
                    
                    }
                }
            }
        }
    }
}
