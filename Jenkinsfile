pipeline {
    agent any

    tools {
        nodejs 'Node_7.8.0'
    }

    stages {
        stage('checkout') {
            step {
                checkout scm
            }
        }
        
        stage('build') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'npm install'
            }
        }

        stage('test') {
            steps {
                sh 'npm test'
            }
        }
    }
}
