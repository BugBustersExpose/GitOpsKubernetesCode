node {
  def app

  stage('Clone repository') {

    checkout scm
  }

  stage('Build image') {

    app = docker.build("bugbustersexpose/test")
  }

  stage('Test image') {

    app.inside {
      ssh 'echo "Test passed"'
    }
  }

stage('Push image') {
  
  docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
    app.push("${env.BUILD_NUMBER}")
  }
}
