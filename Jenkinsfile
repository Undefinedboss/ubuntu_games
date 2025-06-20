pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build('world-of-games:latest')
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    docker.container = docker.run('world-of-games:latest', "-p 8777:8777 -v ${pwd()}/Scores.txt:/app/Scores.txt --name world_of_games_test")
                }
            }
        }
        stage('Test') {
            steps {
                sh 'python3 e2e.py'
            }
        }
        stage('Finalize') {
            steps {
                script {
                    docker.container.stop()
                    docker.container.remove()
                    docker.withRegistry('', 'dockerhub-credentials') {
                        docker.image('world-of-games:latest').push()
                    }
                }
            }
        }
    }
}
