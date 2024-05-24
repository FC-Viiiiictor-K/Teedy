pipeline {
    agent any
    stages{
        stage('Package') {
            steps {
              checkout scmGit(branches: [[name: '*/master']], extensions: [],
userRemoteConfigs: [[url: 'https://github.com/FC-Viiiiictor-K/Teedy.git']])
              sh 'mvn -B -DskipTests clean package'
            }
        }
        // Building Docker images
        stage('Building image') {
            steps{
                sh 'docker build -t teedy .'
            }
        }

        // Uploading Docker images into Docker Hub
        stage('Upload image') {
            steps{
                withCredentials([usernamePassword(credentials
Id: 'dockerhub', passwordVariable: '030306fcK', usernameVariable: 'fcviiiiictork')]) {
                    sh "docker login -u $fcviiiiictork -p $030306fcK"
                    sh 'docker tag teedy $fcviiiiictork/teedy'
                    sh 'docker push $fcviiiiictork/teedy'
                }
            }
        }

        //Running Docker container
        // Run three different containers on port 8082, 8083, 8084
        stage('Run containers'){
            steps{
                sh 'docker run -d -p 8082:8080 --name teedy01 teedy'
                sh 'docker run -d -p 8083:8080 --name teedy02 teedy'
                sh 'docker run -d -p 8084:8080 --name teedy03 teedy'
            }
        }
    }
}