pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Monikasubramani/Blood_Donation_system.git'
            }
        }

        stage('Install') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Run Server') {
            steps {
                bat 'node server.js'
            }
        }
    }
}
