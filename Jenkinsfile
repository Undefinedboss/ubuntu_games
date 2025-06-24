pipeline {
    agent none  // Use per-stage agents instead of one global agent

    stages {
        stage('Checkout') {
            agent any  // Can be run on any node
            steps {
                git 'https://github.com/Undefinedboss/World-of-Games'
            }
        }

        stage('Build on Linux') {
            agent { label 'linux' }
            steps {
                sh './build.sh'
            }
        }

        stage('Run on Linux') {
            agent { label 'linux' }
            steps {
                sh 'docker-compose up -d'
                sleep(time: 10, unit: 'SECONDS')
            }
        }

        stage('Test on Linux') {
            agent { label 'linux' }
            steps {
                sh 'python3 e2e.py'
            }
        }

        stage('Finalize on Linux') {
            agent { label 'linux' }
            steps {
                sh 'docker-compose down'
                // Optional: push to DockerHub
                // sh 'docker tag world-of-games yourdockerhubusername/world-of-games:latest'
                // sh 'docker push yourdockerhubusername/world-of-games:latest'
            }
        }
    }
}
