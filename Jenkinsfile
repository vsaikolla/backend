pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment{
        def AppVersion = ''
    }
    stages {
        stage('Read the Version'){
            steps{
                script{
                    def PackageJson = readJSON file: 'package.json'
                    AppVersion = PackageJson.version
                    echo "Application Version: $AppVersion"
                }
            }
        }
        stage('Install Dependencies') { 
            steps {
                sh '''
                    npm install
                    ls -ltr
                    echo "Application Version: $AppVersion"
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