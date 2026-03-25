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
        
        
    }
}