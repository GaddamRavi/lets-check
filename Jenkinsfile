pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/GaddamRavi/lets-check.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                python3 --version
                python3 -m venv $VENV
                . $VENV/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                . $VENV/bin/activate
                pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                echo "Build successful at $(date)" > output.txt
                '''
                archiveArtifacts artifacts: 'output.txt', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                . $VENV/bin/activate
                echo "Starting application..."
                python3 app.py
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}