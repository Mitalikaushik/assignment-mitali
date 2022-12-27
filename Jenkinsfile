pipeline{
    agent {'any'}
    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mitalikaushik/assignment-mitali.git']]])
            }
        }
        stage('build and push image to ecr'){
            steps{
                sh '''docker build -t as .
                docker tag sgecr:latest 630582687244.dkr.ecr.us-west-2.amazonaws.com/as:latest
                docker push 630582687244.dkr.ecr.us-west-2.amazonaws.com/as:latest'''
            }
        }
        stage('run container'){
            steps{
                sh '''docker run -d -p 8080:8080 630582687244.dkr.ecr.us-west-2.amazonaws.com/as:latest'''
            }
        }
}
}
