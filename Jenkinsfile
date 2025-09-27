pipeline {
    agent any

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
                // Deployment steps specific to your environment
               // echo "Deploying application..."
               sh 'nohup java -jar target/my-webapp-1.0.0.jar > app.log 2>&1 &'
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