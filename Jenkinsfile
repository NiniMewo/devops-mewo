pipeline {
    agent none

    environment {
        NODE_ENV = 'production'
        DOCKER_IMAGE_PYTHON = 'python:3.12.1-alpine3.19'
        DOCKER_IMAGE_NODE = 'node:16-alpine'
    }

    stages {
        stage('Prepare Environment') {
            agent any
            steps {
                checkout scm // Checkout code from Source Control Management
                echo 'Environment prepared.'
            }
        }

        stage('Build and Test Django') {
            agent {
                docker {
                    image "${env.DOCKER_IMAGE_PYTHON}"
                    args '-v /var/run/docker.sock:/var/run/docker.sock -v ${WORKSPACE}:/app'
                }
            }
            steps {
                dir('sources/realWorldApp-Conduit-Django') {
                    script {
                        sh 'pip install --no-cache-dir -r requirements.txt'
                        sh 'python manage.py migrate'
                        echo 'Building the Django code...'
                        sh 'python manage.py test'
                        echo 'Running Django unit tests...'
                    }
                }
            }
        }

        stage('Build and Test Vue.js') {
            agent {
                docker {
                    image "${env.DOCKER_IMAGE_NODE}"
                    args '-v ${WORKSPACE}:/app'
                }
            }
            steps {
                dir('sources/realWorldApp-Conduit-vue3') {
                    script {
                        sh 'npm install --no-cache'
                        sh 'npm run build'
                        echo 'Building the Vue.js code...'
                        sh 'npm run test'
                        echo 'Running Vue.js unit tests...'
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main' // Only deploy from the main branch
            }
            agent any
            steps {
                script {
                    echo 'Deploying the application to staging environment...'
                    // Add deployment scripts here
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
        always {
            cleanWs() // Clean up the workspace after the pipeline execution
        }
    }
}
