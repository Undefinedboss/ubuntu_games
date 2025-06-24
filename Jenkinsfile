pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Undefinedboss/World-of-Games'
            }
        }

        stage('Build') {
            steps {
                sh './build.sh'
            }
        }

        stage('Run') {
            steps {
                sh 'docker-compose up -d'
                sleep(time: 10, unit: "SECONDS")
            }
        }

        stage('Test') {
            steps {
                sh 'python3 e2e.py'
            }
        }

        stage('Finalize') {
            steps {
                sh 'docker-compose down'
            }
        }
    }
}
