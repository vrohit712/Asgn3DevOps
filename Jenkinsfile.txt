pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vrohit712/Asgn3DevOps.git'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew build'            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker build -t rohitdockertwo .' 
                sh 'docker push rohitdockertwo'         // Push image to a registry
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
