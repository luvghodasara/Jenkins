pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Use Maven to build your code
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests with JUnit
                sh 'mvn test'

                // Run integration tests with Selenium
                // You need to have Selenium WebDriver configured
                sh 'mvn integration-test'
            }
        }

        stage('Code Analysis') {
            steps {
                // Use SonarQube for code analysis
                // Assumes SonarQube Scanner is configured
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                // Use OWASP ZAP for security scanning
                sh 'zap-baseline.py -t http://your-app-url'
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Deploy to AWS Elastic Beanstalk
                // Assumes Elastic Beanstalk environment is configured
                sh 'eb deploy your-staging-environment'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on the staging environment with Postman
                // Assumes Postman collection and environment are configured
                sh 'newman run your-postman-collection.json --environment your-postman-environment.json'
            }
        }

        stage('Deploy to Production') {
            steps {
                // Deploy to AWS Elastic Beanstalk (Production Environment)
                sh 'eb deploy your-production-environment'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed"      
        }
    }
}
