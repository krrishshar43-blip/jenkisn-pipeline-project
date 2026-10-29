pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Code GitHub se aa gaya'
                sh 'ls -la'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t cicd-demo-app:${BUILD_NUMBER} -t cicd-demo-app:latest .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm cicd-demo-app:latest | grep -q "Build successful"'
                echo 'Test passed'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker rm -f cicd-demo-container || true'
                sh 'docker run --name cicd-demo-container cicd-demo-app:latest'
            }
        }
    }

    post {
        success {
            echo 'Pipeline SUCCESS: Build, Test aur Deploy ho gaya'
        }
        failure {
            echo 'Pipeline FAILED: console output check karo'
        }
    }
}
