pipeline {
    agent any
    stages{
        stage('Build') {
            steps {
              sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('K8s') {
            steps {
                sh 'docker build -t teedy .'
                sh 'kubectl delete deployment hello-node'
                sh 'kubectl create deployment hello-node --image=fcviiiiictork/teedy:teedy'
                sh 'kubectl expose deployment hello-node --type=LoadBalancer --port=8080'
                sh 'minikube service hello-node'
            }
        }
    }
}