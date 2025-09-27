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
                sh 'mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                echo "Stopping old service (if running)..."
                sh 'sudo systemctl stop myapp.service || true'
        
                echo "Copying new JAR to deploy directory..."
                sh 'sudo cp target/my-webapp-1.0.0.jar /home/ubuntu/simple-Java-application/'
        
                echo "Starting systemd service..."
                sh 'sudo systemctl start myapp.service'
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

