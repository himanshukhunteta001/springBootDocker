pipeline {
    agent any

     tools {
        maven 'MAVEN_HOME'
        dockerTool 'docker_home', 
                  installationType: 'Installer',
                  installer: [
                      'latest'   // Use 'latest' or specify a specific version
                  ]
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
                    def dockerHome = tool 'dockerhome'
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
