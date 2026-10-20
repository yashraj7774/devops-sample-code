pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'python3 -m pip install --user -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'python3 -m unittest discover -s .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                    mkdir -p "${WORKSPACE}/python-app-deploy"
                    cp app.py requirements.txt "${WORKSPACE}/python-app-deploy/"
                '''
            }
        }

        stage('Test Application') {
            steps {
                echo 'Verifying the application...'
                sh '''
                    cd "${WORKSPACE}/python-app-deploy"
                    python3 -m unittest discover -s "${WORKSPACE}"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for more details.'
        }
    }
}
