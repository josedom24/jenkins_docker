pipeline {
    environment {
        IMAGEN = "josedom24/myapp"
        USUARIO = 'USER_DOCKERHUB'
    }
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
                    newApp = docker.build "$IMAGEN:$BUILD_NUMBER"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    docker.image("$IMAGEN:$BUILD_NUMBER").inside('-u root') {
                           sh 'apache2ctl -v'
                        }
                    }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry( '', USUARIO ) {
                        newApp.push()
                    }
                }
            }
        }
        stage('Clean Up') {
            steps {
                sh "docker rmi $IMAGEN:$BUILD_NUMBER"
                }
        }
    }
}
