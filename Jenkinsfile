pipeline {
    agent any

    environment {
        SERVICE_NAME = "myapp.service"
        DEPLOY_DIR = "/home/ubuntu/simple-Java-application"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Satishganiyada/simple-Java-application'
            }
        }

        stage('Build') {
            steps {
                sh "cd ${DEPLOY_DIR} && mvn clean install"
            }
        }

        stage('Test') {
            steps {
                sh "cd ${DEPLOY_DIR} && mvn test"
            }
        }

        stage('Deploy') {
            steps {
                echo "Stopping old service (if running)..."
                sh "sudo systemctl stop ${SERVICE_NAME} || true"

                echo "Copying new JAR to deploy directory..."
                sh "cp ${DEPLOY_DIR}/target/my-webapp-1.0.0.jar ${DEPLOY_DIR}/"

                echo "Starting systemd service..."
                sh "sudo systemctl start ${SERVICE_NAME}"
            }
        }
    }

    post {
        always {
            echo "Pipeline finished."
        }
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Deployment failed, check logs."
        }
    }
}
