pipeline {
    agent any
    triggers{
      pollSCM("* * * * *")
    }
    stages {
        stage('docker-build-test-base') {
            when {
              anyOf {
                changeset 'Gemfile'
                changeset 'Dockerfile.base'
              }
            }
            steps {
              echo 'Building base image for api-tests'
              sh "docker build --no-cache -t einarsngalejs/api-tests-base . -f Dockerfile.base"
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

