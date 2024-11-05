pipeline {
    agent any
    environment {
        VIRTUAL_ENV = isUnix() ? 'venv' : 'venv\\Scripts\\activate'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    // Detects OS and sets up a virtual environment accordingly
                    if (isUnix()) {
                        if (!fileExists("${env.WORKSPACE}/venv")) {
                            sh 'python3 -m venv venv'
                        }
                        sh "source venv/bin/activate && pip install -r requirements.txt"
                    } else {
                        if (!fileExists("${env.WORKSPACE}\\venv")) {
                            bat 'python -m venv venv'
                        }
                        bat "venv\\Scripts\\activate && pip install -r requirements.txt"
                    }
                }
            }
        }
        stage('Lint') {
            steps {
                script {
                    if (isUnix()) {
                        sh "source venv/bin/activate && flake8 app.py"
                    } else {
                        bat "venv\\Scripts\\activate && flake8 app.py"
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh "source venv/bin/activate && pytest"
                    } else {
                        bat "venv\\Scripts\\activate && pytest"
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying application..."
                // Add deployment steps as needed
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
