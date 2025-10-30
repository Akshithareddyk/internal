pipeline {
    agent any   

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                sh "docker build -t kubdemoapp:v1 ."
            }
        }

        stage('Docker Login') {
            steps {
                echo "Logging into Docker Hub"
                sh 'echo docker login -u akshithareddy27 -p docker123'
            }
        }

        stage('Tag & Push Docker Image to Docker Hub') {
            steps {
                echo "Tagging and Pushing Docker Image"
                sh "docker tag kubdemoapp:v1 akshithareddy27/week8:kubeimage1"
                sh "docker push akshithareddy27/week8:kubeimage1"
            }
        }

        stage('Deploy to Kubernetes') { 
            steps { 
                echo "Deploying to Kubernetes"
                sh 'kubectl apply -f deployment.yaml --validate=false' 
                sh 'kubectl apply -f service.yaml' 
            } 
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Please check the logs.'
        }
    }
}
