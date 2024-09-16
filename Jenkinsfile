pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Building the code using Maven to compile and package the application.'
                echo 'Tool: Maven'
                // Simulating log generation for build stage
                sh 'echo "Build log content" > build-logs/build.log'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running unit tests with JUnit and integration tests with Selenium.'
                echo 'Tools: JUnit (Unit Testing), Selenium (Integration Testing)'
                // Simulate log generation for tests
                sh 'mkdir -p test-logs && echo "JUnit test log" > test-logs/test.log'
            }
            post {
                always {
                    emailext(
                        subject: "Build ${currentBuild.fullDisplayName} - Unit and Integration Tests Stage",
                        body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}.",
                        to: "mino.menuranga@gmail.com",
                        attachLog: true,  // Automatically attach the full console log
                        attachmentsPattern: '**/test-logs/*.log'  // Attach test logs if available
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Analyzing code quality using SonarQube to ensure industry standards are met.'
                echo 'Tool: SonarQube'
                // Simulate log generation for code analysis
                sh 'echo "SonarQube log content" > analysis-logs/code-analysis.log'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Performing security scans using OWASP ZAP to identify vulnerabilities.'
                echo 'Tool: OWASP ZAP'
                // Simulate security scan log generation
                sh 'mkdir -p security-logs && echo "OWASP ZAP log" > security-logs/security.log'
            }
            post {
                always {
                    emailext(
                        subject: "Build ${currentBuild.fullDisplayName} - Security Scan Stage",
                        body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}.",
                        to: "mino.menuranga@gmail.com",
                        attachLog: true,  // Automatically attach the full console log
                        attachmentsPattern: '**/security-logs/*.log'  // Attach security logs if available
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying the application to an AWS EC2 instance for staging.'
                echo 'Tool: AWS CLI'
                // Simulate log generation for deployment
                sh 'echo "Deploy to Staging log content" > deploy-logs/staging.log'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Running integration tests in the staging environment using Postman.'
                echo 'Tool: Postman'
                // Simulate log generation for integration tests on staging
                sh 'echo "Postman test log" > test-logs/integration-staging.log'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to an AWS EC2 instance for production.'
                echo 'Tool: AWS CLI'
                // Simulate log generation for production deployment
                sh 'echo "Deploy to Production log content" > deploy-logs/production.log'
            }
        }
    }

    post {
        failure {
            emailext(
                subject: "Build ${currentBuild.fullDisplayName} - Failure",
                body: "The build has failed. Please check the Jenkins logs for more details.",
                to: "mino.menuranga@gmail.com",
                attachLog: true,  // Automatically attach the full console log
                attachmentsPattern: '**/build-logs/*.log'  // Attach build logs if available
            )
        }
        success {
            emailext(
                subject: "Build ${currentBuild.fullDisplayName} - Success",
                body: "The build has succeeded. All stages completed successfully.",
                to: "mino.menuranga@gmail.com",
                attachLog: true  // Automatically attach the full console log
            )
        }
    }
}
