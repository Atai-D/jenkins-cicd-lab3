pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    environment {
        IMAGE_TAG = 'v1.0'
    }

    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('build') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'npm install --no-progress --loglevel=warn'
            }
        }

        stage('test') {
            steps {
                sh 'npm test'
            }
        }

        stage('docker build') {
            steps {
                script {
                    def imageName = "node${env.BRANCH_NAME}:${env.IMAGE_TAG}"

                    echo "Building Docker image: ${imageName}"

                    sh "docker build -t ${imageName} ."
                }
            }
        }
    }
}
