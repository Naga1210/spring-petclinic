pipeline {
    agent { label 'spc' }

    triggers {
        pollSCM('H/5 * * * *')   // every 5 minutes
    }

    stages {

        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/Naga1210/spring-petclinic.git', branch: 'main'
            }
        }

        // stage('Build and Scan') {
        //     steps {
        //         withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
        //             withSonarQubeEnv('sonar') {
        //                 sh '''
        //                 mvn clean package sonar:sonar \
        //                 -Dsonar.projectKey=Naga1210_spring-petclinic \
        //                 -Dsonar.organization=Naga1210 \
        //                 -Dsonar.host.url=https://sonarcloud.io \
        //                 -Dsonar.login=$SONAR_TOKEN
        //                 '''
        //             }
        //         }
        //     }
        // }

        stage('Docker image push to ecr and pullin from docker hub') {
            steps {
                
                    sh '''
                    docker image pull nginx:1.29 && \
                    aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin 052247097669.dkr.ecr.ap-northeast-1.amazonaws.com && \
                    docker tag nginx:1.29 052247097669.dkr.ecr.ap-northeast-1.amazonaws.com/dev/spcimage:latest && \
                    docker push 052247097669.dkr.ecr.ap-northeast-1.amazonaws.com/dev/spcimage:latest
                    '''
                
            }
        }

    }
}