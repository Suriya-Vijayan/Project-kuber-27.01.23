pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Suriya-Vijayan/Project-kuber-27.01.23.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t newimage /var/lib/jenkins/workspace/Project-k8s'
                sh 'sudo docker tag newimage suriyavijayan1126/newimage:latest'
                sh 'sudo docker tag newimage suriyavijayan1126/newimage:${BUILD_NUMBER}'
            }

       }
       stage('push the Docker image') {
           steps {
               sh 'sudo docker image push suriyavijayan1126/newimage:latest'
               sh 'sudo docker image push suriyavijayan1126/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f /var/lib/jenkins/workspace/Project-k8s/pod.yaml'
                sh 'kubectl rollout restart deployment loadbalancer-pod'
            }

        }

    }
   
}