pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Building the code using Maven to compile and package the application.'
                echo 'Tool: Maven'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running unit tests with JUnit and integration tests with Selenium.'
                echo 'Tools: JUnit (Unit Testing), Selenium (Integration Testing)'
            }
            post {
                always {
                    echo 'Sending email for Unit and Integration Tests...'
                    emailext(
                        subject: "Build ${currentBuild.fullDisplayName} - Unit and Integration Tests Stage",
                        body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}",
                        to: "mino.menuranga@gmail.com"
                    )
                    echo 'Email sent for Unit and Integration Tests.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Analyzing code quality using SonarQube to ensure industry standards are met.'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Performing security scans using OWASP ZAP to identify vulnerabilities.'
                echo 'Tool: OWASP ZAP'
            }
            post {
                always {
                    echo 'Sending email for Security Scan...'
                    emailext(
                        subject: "Build ${currentBuild.fullDisplayName} - Security Scan Stage",
                        body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}",
                        to: "mino.menuranga@gmail.com"
                    )
                    echo 'Email sent for Security Scan.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying the application to an AWS EC2 instance for staging.'
                echo 'Tool: AWS CLI'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Running integration tests in the staging environment using Postman.'
                echo 'Tool: Postman'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to an AWS EC2 instance for production.'
                echo 'Tool: AWS CLI'
            }
        }
    }

    post {
        failure {
            echo 'Sending failure email...'
            emailext(
                subject: "Build ${currentBuild.fullDisplayName} - Failure",
                body: "The build has failed. Please check the Jenkins logs for more details.",
                to: "mino.menuranga@gmail.com"
            )
            echo 'Failure email sent.'
        }
        success {
            echo 'Sending success email...'
            emailext(
                subject: "Build ${currentBuild.fullDisplayName} - Success",
                body: "The build has succeeded. All stages completed successfully.",
                to: "mino.menuranga@gmail.com"
            )
            echo 'Success email sent.'
        }
    }
}
