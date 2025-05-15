pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'rashistudent29@gmail.com'
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
                        body: """The test stage has completed with status: ${currentBuild.currentResult}.
                                \nSee the attached build log for details.""",
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    try {
                        echo 'Running security scan...'
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
                        subject: "Security Scan Stage: ${currentBuild.currentResult}",
                        body: """The security scan stage has completed with status: ${currentBuild.currentResult}.
                                \nSee the attached build log and scan output for details.""",
                        to: "rashiagrawal299@gmail.com",
                        attachLog: true,
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

