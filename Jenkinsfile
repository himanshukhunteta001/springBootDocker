pipeline {
    agent any

     tools {
        maven 'MAVEN_HOME'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build Maven Package') {
            steps {
                script {
                    sh 'mvn clean install'
                    echo "Build Application"
                }
            }
        }

        stage(' Docker Build') {
            steps {
                // Build Docker image using the Dockerfile
                script {
                    def dockerImage = "spring-boot-docker"
                    sh "docker build -t ${dockerImage} ."
                }
            }
        }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
