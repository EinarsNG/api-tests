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
        build-docker("einarsngalejs/api-tests-base", "Dockerfile.base")
      }
    }
    stage('docker-build-test-runner') {
      steps {
        build-docker("einarsngalejs/api-tests-runner", "Dockerfile.runner")
      }
    }
  }
}

def build-docker(String tag, String file) {
  echo "Building $tag image for api-tests"
  sh "docker build --no-cache -t $tag . -f $file"
  sh "docker login -u $DOCKER_USER -p \"$DOCKER_PASS\""
  sh "docker push $tag:latest"
}
