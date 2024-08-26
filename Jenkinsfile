pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'katiekhinezt@gmail.com'
        MAVEN_HOME = '/opt/homebrew/Cellar/maven/3.9.9/libexec'
    }

    tools {
        maven 'Maven 3.9.9'  // Ensure this matches the Maven version you have configured in Jenkins
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    dir('my-app') {
                        sh '${MAVEN_HOME}/bin/mvn clean package'
                    }
                }
            }
        }

        // Add other stages if needed
    }

    post {
        success {
            script {
                echo 'Pipeline succeeded. Sending success email...'
                mail to: "${EMAIL_RECIPIENT}",
                     subject: "Jenkins Build Success",
                     body: "The Jenkins pipeline build was successful."
            }
        }
        failure {
            script {
                echo 'Pipeline failed. Sending failure email...'
                mail to: "${EMAIL_RECIPIENT}",
                     subject: "Jenkins Build Failure",
                     body: "The Jenkins pipeline build failed. Please check the build logs."
            }
        }
    }
}

