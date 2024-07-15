pipeline {
  agent {
    docker {
      image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
  stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        // Uncomment the following line to enable the git checkout
        // git branch: 'main', url: 'https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero.git'
        git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/DILSHAN565/Try_build.git'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        // Build the project and create a JAR file
        sh 'mvn clean package'
      }
    }
  }
}
