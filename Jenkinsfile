pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code...'
                dir('my-app') {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                dir('my-app') {
                    sh 'mvn test'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Add code analysis steps here
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Add security scan steps here
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Add deployment steps here
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Add integration tests on staging environment steps here
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Add production deployment steps here
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            mail to: 'katiekhinezt@gmail.com',
                 subject: "Successful Pipeline Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build ${env.BUILD_NUMBER} of job ${env.JOB_NAME} was successful.\n\nCheck Jenkins for details."
        }
        failure {
            echo 'Pipeline failed.'
            mail to: 'katiekhinezt@gmail.com',
                 subject: "Failed Pipeline Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build ${env.BUILD_NUMBER} of job ${env.JOB_NAME} failed.\n\nCheck Jenkins for details."
        }
    }
}
