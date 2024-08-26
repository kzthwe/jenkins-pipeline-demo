pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 's224051483@deakin.edu.au'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Ensure the directory contains the correct POM file
                    dir('my-app') {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Ensure the directory contains the correct POM file
                    dir('my-app') {
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Running code analysis...'
                    // Example tool: SonarQube
                    // Replace with your actual code analysis tool command
                    sh 'sonar-scanner -Dsonar.projectKey=my-app'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Example tool: OWASP Dependency-Check
                    // Replace with your actual security scan tool command
                    sh 'dependency-check --project my-app --out . --scan my-app'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging server...'
                    // Example deployment script or command
                    // You may need to adjust this based on your deployment tool
                    sh 'deploy-staging.sh'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Example test script or command
                    sh 'integration-tests-staging.sh'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production server...'
                    // Example deployment script or command
                    // You may need to adjust this based on your deployment tool
                    sh 'deploy-production.sh'
                }
            }
        }
    }

    post {
        success {
            script {
                echo 'Pipeline succeeded. Sending success email...'
                mail to: "${EMAIL_RECIPIENT}",
                     subject: "Jenkins Build Success",
                     body: "The Jenkins pipeline build was successful.",
                     attachLog: true
            }
        }
        failure {
            script {
                echo 'Pipeline failed. Sending failure email...'
                mail to: "${EMAIL_RECIPIENT}",
                     subject: "Jenkins Build Failure",
                     body: "The Jenkins pipeline build failed. Please check the build logs.",
                     attachLog: true
            }
        }
    }
}

