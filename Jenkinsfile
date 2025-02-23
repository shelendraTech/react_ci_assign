pipeline {
    agent any 

    stages {

        stage('Clean Up Code') {
            steps {
                script {
                    echo "Cleaning up code"
                    cleanWs()
                }
            }
        }

        stage('Checkout Code') {
            steps {
                script {
                    echo 'Checking out code'
                    checkout scm
                }
            }
        }

        stage('Show Files and Directories Before Setup') {
            steps {
                script {
                    echo 'Showing files and directories before setup'
                    sh 'ls -la'
                }
            }
        } 

        stage('Setup Node.js') {
            agent {
                docker {
                    image 'node:22.11.0-alpine3.20'  // Using Node.js 22 with Alpine Linux
                    args '-u root'  // Run as root to avoid permission issues
                }
            }
            steps {
                script {
                    echo 'Verifying Node.js & npm versions'
                    sh '''
                        node --version
                        npm --version
                    '''
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies'
                    sh 'npm install'
                }
            }
        }

        stage('Show Files and Directories After Install') {
            steps {
                script {
                    echo 'Showing files and directories after install'
                    sh 'ls -la'
                }
            }
        }

        stage('Build App') {
            steps {
                script {
                    echo 'Building App' 
                    sh 'npm run build'
                }
            }
        } 

        stage('Show Files and Directories After Build') {
            steps {
                script {
                    echo "Showing files and directories after build"
                    sh 'ls -la'
                }
            }
        }
    }
}
