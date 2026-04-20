pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Monikasubramani/Blood_Donation_system.git'
            }
        }

        stage('Build') {
            steps {
                echo 'No build needed'
            }
        }

        stage('Deploy') {
            steps {
                bat 'echo Deploy step running...'
            }
        }
    }
}
