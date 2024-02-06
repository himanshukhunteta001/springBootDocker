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

        stage('Build Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-pass'){

                        sh 'docker build -t himanshukhunteta/spring-boot-docker:tag123 .'
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
