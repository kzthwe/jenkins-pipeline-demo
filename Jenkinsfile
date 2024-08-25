pipeline {
    agent any
    tools {
        maven 'Maven 3.8.1'  // Adjust Maven version as needed
    }
    stages {
        stage('Build') {
            steps {
                echo "Building the application using Maven"
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit and integration tests"
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Running code analysis with SonarQube"
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo "Performing security scan with OWASP Dependency Check"
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging server"
                sh 'scp target/*.jar user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                // Commands to run integration tests
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production server"
                sh 'scp target/*.jar user@production-server:/path/to/deploy'
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

