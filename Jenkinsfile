pipeline {
    agent any

    environment {
        IMAGE_TAG = "jma-1.1"
    }

    tools {
        maven 'maven-3.9'
    }

    stages {
        stage('Build jar') {
            steps {
                script {
                    echo "Building the JAR file..."
                    sh 'mvn package'
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "Building and pushing Docker image with tag: ${IMAGE_TAG}"
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                        sh "docker build -t masjidan/demo-app:${IMAGE_TAG} ."
                        sh "docker push masjidan/demo-app:${IMAGE_TAG}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                    // Tambahkan langkah deployment sesuai kebutuhan Anda di sini
                }
            }
        }
    }
}
