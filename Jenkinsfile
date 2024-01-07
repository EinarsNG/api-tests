pipeline {
    agent any

    stages {
        stage('docker-build-test-base') {
            steps {
                echo 'Building base image for api-tests'
                sh "docker build -t einarsngalejs/api-tests-base . -f Dockerfile.base"
            }
        }
        stage('docker-build-test-runner') {
            steps {
                echo 'Building runner image for api-tests'
                sh "docker build -t einarsngalejs/api-tests-runner . -f Dockerfile.runner"
            }
        }
    }
}

