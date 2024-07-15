pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
               
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/DILSHAN565/Try_build.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
                 //sh 'mvn -e compile -DskipTests'
                 //sh 'mvn -B -DskipTests clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
