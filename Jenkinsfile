pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    stages {
        stage('Install Dependencies') { 
            steps {
                sh '''
                    npm install
                    ls -ltr
                '''
            }
        }
    }
    post{
        always{
            echo 'i will always say hello'
            deleteDir()
        }
        success{
            echo 'i will run if build is success'
        }
        failure{
            echo 'i will run if build is failure'
        }
    }
}