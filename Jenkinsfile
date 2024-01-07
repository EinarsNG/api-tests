pipeline {
  agent any
  triggers{
    pollSCM("* * * * *")
  }
  environment{
    DOCKER_USER = credentials("docker-user")
    DOCKER_PASS = credentials("docker-pw")
  }
  stages {
    stage('docker-build-test-base') {
      when {
        anyOf {
          changeset 'Gemfile'
          changeset 'Dockerfile.base'
          changeset 'Jenkinsfile'
        }
      }
      steps {
        echo 'Building base image for api-tests'
        sh "docker build --no-cache -t einarsngalejs/api-tests-base . -f Dockerfile.base"
        sh "docker login -u $DOCKER_USER -p \"$DOCKER_PASS\""
        sh "docker push einarsngalejs/api-tests-base:latest"
      }
    }
    stage('docker-build-test-runner') {
      steps {
        echo 'Building runner image for api-tests'
        sh "docker build --no-cache -t einarsngalejs/api-tests-runner . -f Dockerfile.runner"
        sh "docker login -u $DOCKER_USER -p \"$DOCKER_PASS\""
        sh "docker push einarsngalejs/api-tests-runner:latest"
      }
    }
  }
}
