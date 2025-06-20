pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Undefinedboss/World-of-Games'
            }
        }

        stage('Build') {
            steps {
                bat 'build.bat'
            }
        }

        stage('Run') {
            steps {
                bat 'docker-compose up -d'
                sleep(time: 10, unit: "SECONDS") // Wait for the app to start
            }
        }

        stage('Test') {
            steps {
                bat 'python e2e.py'
            }
        }

        stage('Finalize') {
            steps {
                bat 'docker-compose down'
                // Uncomment and configure DockerHub credentials if needed
                // bat 'docker tag world-of-games yourdockerhubusername/world-of-games:latest'
                // bat 'docker push yourdockerhubusername/world-of-games:latest'
            }
        }
    }
}
