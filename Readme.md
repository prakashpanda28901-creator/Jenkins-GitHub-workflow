CI/CD pipeline using jenkins and docker

created a app.py file for flask application
and created a requirement.txt file then created a dockerfile to build image
test docker locally: docker build -t flask app .
docker run -d -p 5000:5000 flask-app
open localhost:5000 and localhost:5000/about to see the output
then creating a repo jenkins-github workflow and push this code into github

start jenkins: sudo usermod -aG docker jenkins (to add jenkins users in docker group)(a = append, 
G = Supplimentary group)
sudo systemctl start jenkins
created a pipeline job name job2
below is my jenkins pipeline code
pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {
                git branch: 'main', 
                  url: 'https://github.com/prakashpanda28901-creator/Jenkins-GitHub-workflow.git'
            }

        }

        stage('Build Docker Image') {

            steps {
                sh 'docker build -t flask-app .'
            }

        }

        stage('Stop Old Container') {

            steps {
                sh '''
                docker stop flask-container || true
                docker rm flask-container || true
                '''
            }

        }

        stage('Deploy Container') {

            steps {
                sh '''
                docker run -d \
                --name flask-container \
                -p 5000:5000 \
                flask-app
                '''
            }

        }

    }

}
save build