pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: '*/master', url: 'https://github.com/vrohit712/Asgn3DevOps.git'
            }
        }
        stage('Build') {
            echo 'Building....'            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'         // Push image to a registry
                // Alternatively, deploy to a server via SSH or another method
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            junit 'build/test-results/**/*.xml'  // Publish test results
        }
    }
}
