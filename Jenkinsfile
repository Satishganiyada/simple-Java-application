pipeline {
    agent any

    environment {
        SERVICE_NAME = "myapp.service"               // Systemd service
        DEPLOY_DIR = "/home/ubuntu/simple-Java-application"  // Deployment folder
        JAR_NAME = "my-webapp-1.0.0.jar"            // JAR file name
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                git 'https://github.com/Satishganiyada/simple-Java-application'
            }
        }

        stage('Build') {
            steps {
                echo "Building project..."
                sh "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh "mvn test"
            }
        }

                stage('Deploy') {
            steps {
                echo "Stopping old service (if running)..."
                sh "sudo systemctl stop myapp.service || true"
        
                echo "Copying new JAR to deployment directory..."
                sh "sudo cp target/my-webapp-1.0.0.jar /home/ubuntu/simple-Java-application/"
        
                echo "Starting systemd service..."
                sh "sudo systemctl start myapp.service"
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
            echo "Deployment failed. Check Jenkins logs and service logs."
        }
    }
}

