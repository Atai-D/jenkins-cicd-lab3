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
         stage('deploy') {
            steps {
                script {
                    def imageName = "node${env.BRANCH_NAME}:${env.IMAGE_TAG}"
                    def containerName = "node${env.BRANCH_NAME}"
                    def hostPort = env.BRANCH_NAME == 'main' ? '3000' : '3001'

                    echo "deploying branch: ${env.BRANCH_NAME}"
                    echo "image: ${imageName}"
                    echo "container: ${containerName}"
                    echo "host port: ${hostPort}"

                    sh "docker rm -f ${containerName} || true"
                    sh "docker run -d --name ${containerName} --restart unless-stopped -p ${hostPort}:3000 ${imageName}"
                }
            }
        }
    }
}
