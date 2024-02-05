pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        docker 'docker_home' // assuming 'docker' is the name of your Docker tool in Jenkins
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
                    bat 'mvn clean install'
                    echo "Build Application"
                }
            }
        }

        stage('Initialize') {
            steps {
                script {
                    def dockerHome = tool 'docker_home'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t himanshu/spring-boot-docker .'
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
