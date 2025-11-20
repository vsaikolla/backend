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
        stage('Read the Version'){
            steps{
                script{
                    def PackageJson = readJSON file: 'package.json'
                    def AppVersion = PackageJson.Version
                    echo "Application Version: $AppVersion"
                }
            }
        }
        stage('Install Dependencies') { 
            steps {
                sh '''
                    npm install
                    ls -ltr
                    echo "$AppVersion"
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