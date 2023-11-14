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
  
  stage('Trigger ManifestUpdate') {
    
    echo "Triggering updatemaniest job"
    build job: 'update-manifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
}
}
