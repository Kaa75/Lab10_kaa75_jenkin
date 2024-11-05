pipeline {
    agent any

    environment {
        VIRTUAL_ENV = '.venv'
    }

    stages {
        stage('Setup') {
            steps {
                script {
                    bat """
                    if not exist "${VIRTUAL_ENV}\\Scripts\\activate.bat" (
                        py -m venv ${VIRTUAL_ENV}
                    )
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
                    // Deployment logic, e.g., pushing to a remote server
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
