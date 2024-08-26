pipeline {
    agent any
    tools {
        maven 'Maven 3.8.1' // Ensure this matches the name of the Maven installation in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from Git repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Navigate to the Maven project directory
                dir('my-app') {
                    // Run Maven build command
                    sh 'mvn clean package'
                }
            }
        }
        stage('Test') {
            steps {
                dir('my-app') {
                    // Run Maven test command (optional)
                    sh 'mvn test'
                }
            }
        }
        stage('Archive') {
            steps {
                // Archive the build artifacts (optional)
                archiveArtifacts artifacts: 'my-app/target/*.jar', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            // Perform cleanup or notifications (e.g., email notifications)
            echo 'Pipeline finished.'
        }
    }
}

