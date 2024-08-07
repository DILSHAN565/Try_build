pipeline {
    agent {
        docker {
            //image 'abhishekf5/maven-abhishek-docker-agent:v1'
            image 'thilanka998/thilanka-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket to access the host's Docker daemon
        }
    }

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
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
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('File System Scan') {
            steps {
                sh 'trivy fs --format table -o trivy-fs-report.html .'
            }
        }

        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonar') {
        //             sh ''' 
        //             $SCANNER_HOME/bin/sonar-scanner \
        //                 -Dsonar.projectName=Build_test \
        //                 -Dsonar.projectKey=Build_test \
        //                 -Dsonar.java.binaries=. 
        //             '''
        //         }
        //     }
        // }
        
        // stage('Quality Gate') {
        //     steps {
        //         script {
        //             waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
        //         }
        //     }
        // }

        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }

        /* Uncomment and configure this stage if you need to publish to Nexus
        stage('Publish to Nexus') {
            steps {
                withMaven(globalMavenSettingsConfig: 'global-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn deploy'
                }
            }
        }
        */

        // stage('Build the Docker Image') {
        //     steps {
        //         script {
        //             withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
        //                 sh 'docker build -t thilanka998/Boardgame:v1 .'
        //             }
        //         }
        //     }
        // }
    }
}
