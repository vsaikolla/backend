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
        def appversion = '' // declaring a variable
    }
    stages {
        stage('Read the Version'){
            steps{
                script{
                    def PackageJson = readJSON file: 'package.json'
                    appversion = PackageJson.version
                    echo "Application Version: $appversion"
                }
            }
        }
        stage('Install Dependencies') { 
            steps {
                sh """
                    npm install
                    ls -ltr
                    echo "Application Version: $appversion"
                """
            }
        }
        stage('Build'){
            steps{
                sh """
                zip -q -r backend-${appversion}.zip * -x Jenkinsfile -x backend-${appversion}.zip
                ls -ltr
                """
            }
        }
    }
    post{
        always{
            echo 'i will always say hello'
            //deleteDir()
        }
        success{
            echo 'i will run if build is success'
        }
        failure{
            echo 'i will run if build is failure'
        }
    }
}