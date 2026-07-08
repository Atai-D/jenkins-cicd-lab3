pipeline {
    agent any

    tools {
        nodejs 'node'
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
    }
}
