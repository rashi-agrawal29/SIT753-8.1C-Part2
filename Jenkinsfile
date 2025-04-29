pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'rashiagrawal299@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        echo 'Running tests...'
                        // Simulate test
                        sh 'echo "Test logs..." > test_log.txt'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "Test Stage: ${currentBuild.currentResult}",
                        body: "The test stage has completed with status: ${currentBuild.currentResult}",
                        to: "${EMAIL_RECIPIENT}",
                        attachmentsPattern: 'test_log.txt'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Running security scan...'
                        // Simulate scan
                        sh 'echo "Security scan logs..." > security_log.txt'
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        throw err
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "Security Scan: ${currentBuild.currentResult}",
                        body: "The security scan stage has completed with status: ${currentBuild.currentResult}",
                        to: "${EMAIL_RECIPIENT}",
                        attachmentsPattern: 'security_log.txt'
                    )
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
