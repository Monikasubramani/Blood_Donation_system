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

        stage('Run App') {
            steps {
                bat 'npm start'
            }
        }
    }
}
