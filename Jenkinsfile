// filepath: /c:/Users/karim/OneDrive/Desktop/University/eece_435L/Lab10/Jenkinsfile
pipeline {
    agent any
    environment {
        VIRTUAL_ENV = 'venv'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    if (!fileExists("${env.WORKSPACE}\\${VIRTUAL_ENV}")) {
                        bat "py -m venv ${VIRTUAL_ENV}"
                    }
                    bat """
                    call ${VIRTUAL_ENV}\\Scripts\\activate.bat
                    pip install -r requirements.txt
                    """
                }
            }
        }
        stage('Lint') {
            steps {
                script {
                    bat """
                    call ${VIRTUAL_ENV}\\Scripts\\activate.bat
                    flake8 app.py
                    """
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    bat """
                    call ${VIRTUAL_ENV}\\Scripts\\activate.bat
                    pytest
                    """
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo "Deploying application..."
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}