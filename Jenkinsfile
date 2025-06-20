pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    def customImage = docker.build("your-image-name:latest")
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    // Run the container
                    def container = docker.run("your-image-name:latest", "-p 8777:8777 -v ${pwd()}/Scores.txt:/app/Scores.txt")
                    // Save container reference for later use
                    env.CONTAINER_ID = container.id
                }
            }
        }
        // other stages...
    }

    post {
        always {
            script {
                // Cleanup: stop container if running
                if (env.CONTAINER_ID) {
                    sh "docker stop ${env.CONTAINER_ID}"
                    sh "docker rm ${env.CONTAINER_ID}"
                }
            }
        }
    }
}

