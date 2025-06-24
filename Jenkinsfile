pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Undefinedboss/ubuntu_games'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x build.sh && ./build.sh'
            }
        }

        stage('Run') {
            steps {
                sh 'docker compose up -d'
                sleep(time: 10, unit: 'SECONDS')
            }
        }

        stage('Test') {
            steps {
                sh 'pip3 install selenium'
                sh 'python3 e2e.py'
            }
        }

        stage('Finalize') {
            steps {
                sh 'docker compose down'
            }
        }
    }
}
