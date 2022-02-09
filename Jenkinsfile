pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: "main", url: 'https://github.com/josedom24/jenkins_docker.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    def newApp = docker.build "josedom24/myapp:${env.BUILD_TAG}"
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Tareas para desplegar, construir, ...'
            }
        }
    }
}
