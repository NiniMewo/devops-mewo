pipeline {
    agent any
    stages {
        stage('Initialize') {
            steps {
                script {
                    echo 'Starting the Pipeline...'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running unit tests...'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the application to staging environment...'
                }
            }
        }
    }
    post {
        success {
            script {
                echo 'Pipeline completed successfully!'
            }
        }
        failure {
            script {
                echo 'Pipeline failed. Check logs for details.'
            }
        }
        always {
            script {
                echo 'This post section runs regardless of the pipeline result.'
            }
        }
    }
}