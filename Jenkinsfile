node {
  def app
  stage("Clone repository") {
    checkout scm
  }
  
  stage("Build image") {
    if (env.BRANCH_NAME == "develop") {
      app = docker.build("legendmt25/kiii-jenkins")
    }
  }
  
  stage("Push image") {
    if (env.BRANCH_NAME == "develop") {
      docker.withRegistry("https://registry.hub.docker.com", "dockerhub") {
        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
        app.push("${env.BRANCH_NAME}-latest")
      }
    }
  }

}