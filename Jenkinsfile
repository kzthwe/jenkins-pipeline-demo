pipeline {
    agent any
    
    tools {
        maven 'Maven 3.8.1'  // Adjust Maven version as needed
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Building the application using Maven"
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo "Running unit and integration tests"
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'  // Publish test results
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    echo "Running code analysis with SonarQube"
                    // Assuming SonarQube is configured in Jenkins
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    echo "Performing security scan with OWASP Dependency Check"
                    sh 'mvn org.owasp:dependency-check-maven:check'
                }
            }
            post {
                always {
                    emailext subject: 'Security Scan Results',
                             body: 'Security scan has completed.',
                             recipientProviders: [developers()],
                             attachLog: true,
                             to: 'developer@example.com'
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to staging server"
                    // Example command for deployment (adjust as needed)
                    sh 'scp target/*.jar user@staging-server:/path/to/deploy'
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo "Running integration tests on staging"
                    // Commands to run integration tests
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to production server"
                    // Example command for deployment (adjust as needed)
                    sh 'scp target/*.jar user@production-server:/path/to/deploy'
                }
            }
        }
    }
    
    post {
        success {
            emailext subject: 'Pipeline Succeeded',
                     body: 'The pipeline has completed successfully.',
                     recipientProviders: [developers()],
                     to: 'developer@example.com'
        }
        failure {
            emailext subject: 'Pipeline Failed',
                     body: 'The pipeline has failed. Please check the Jenkins logs.',
                     recipientProviders: [developers()],
                     to: 'developer@example.com'
        }
    }
}

