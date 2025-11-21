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
        nexusUrl = 'nexus.sainath.online:8081'
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
                sudo yum install zip -y
                zip -q -r backend-${appversion}.zip * -x Jenkinsfile -x backend-${appversion}.zip
                ls -ltr
                """
            }
        }
        stage('Nexus Artifact Upload'){
            steps{
                script{
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${nexusUrl}",
                        groupId: 'com.expense',
                        version: "${appversion}",
                        repository: 'backend',
                        credentialsId: 'nexus-auth',
                        artifacts: [
                            [artifactId: 'backend',
                            classifier: '',
                            file: 'backend-' + "${appversion}" + '.zip',
                            type: 'zip']
                        ]
                    )
                }
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