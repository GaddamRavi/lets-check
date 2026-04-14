// Jenkinsfile
pipeline {
    agent any

    stages {

        stage('Clone Code') {
    steps {
        git branch: 'main',
            url: 'https://github.com/GaddamRavi/lets-check.git'
        }
        }


        stage('Install Dependencies') {
    steps {
        sh 'pip3 install -r requirements.txt'
    }
}

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}