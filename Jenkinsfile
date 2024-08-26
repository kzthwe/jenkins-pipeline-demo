pipeline {
    agent any

    tools {
        // Make sure the name matches the Maven installation name in Jenkins Global Tool Configuration
        maven 'Maven 3.9.9'
    }

    environment {
        // Define any environment variables if needed
        MAVEN_OPTS = '-Xms256m -Xmx512m'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code from SCM...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add deployment steps here
                // Example: sh 'scp target/my-app.jar user@server:/path/to/deploy'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
            mail to: 'katiekhinezt@gmail.com',
                 subject: "Build Succeeded: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                 body: "Build succeeded! Check Jenkins for details: ${env.BUILD_URL}"
        }
        failure {
            echo 'Build failed!'
            mail to: 'katiekhinezt@gmail.com',
                 subject: "Build Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                 body: "Build failed! Check Jenkins for details: ${env.BUILD_URL}",
                 attachLog: true
        }
    }
}

