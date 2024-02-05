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
                    bat 'mvn clean install'
		            echo "Build Application"
                }
            }
        }
        stage('Build Docker Image'){
            steps {
                script {
                    def wslDockerCommand = """wsl -e docker build -t himanshu/spring-boot-docker ."""
                    bat(wslDockerCommand)
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