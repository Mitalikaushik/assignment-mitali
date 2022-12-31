pipeline{
    agent {label 'App'}
    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mitalikaushik/assignment-mitali.git']]])
            }
        }
        stage('build and push image to ecr'){
            steps{
                sh '''docker build -t assign .
                docker tag assign:latest 788051511621.dkr.ecr.us-east-1.amazonaws.com/assign:latest
                docker push 788051511621.dkr.ecr.us-east-1.amazonaws.com/assign:latest'''
            }
        }
        stage('run container'){
            steps{
                sh '''docker run -d -p 8080:8080 788051511621.dkr.ecr.us-east-1.amazonaws.com/assign:latest'''
            }
        }
}
}
