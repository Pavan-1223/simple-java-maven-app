pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {

        stage('Checkout & Clean') {
            steps {
                checkout scm
                bat 'mvn clean'
            }
        }

        stage('Install') {
            steps {
                bat 'mvn install'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }
    }

    post {

        success {
            emailext(
                subject: "Jenkins Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

The Jenkins build completed successfully.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build Status: SUCCESS

Please check Jenkins for complete build details.

Regards,
Jenkins
""",
                to: "YOUR_GMAIL@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "Jenkins Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

The Jenkins build has FAILED.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build Status: FAILURE

Please check the Jenkins console output for details.

Regards,
Jenkins
""",
                to: "gummanurpavan@gmail.com"
            )
        }
    }
}
