pipeline {

    agent any

    stages {

        stage('Clone') {

            steps {

                echo 'Cloning repository'

            }

        }

        stage('Build Docker Image') {

            steps {

                sh 'sudo docker build -t devops-poc .'

            }

        }

        stage('Remove Old Container') {

            steps {

                sh 'sudo docker rm -f poc-container || true'

            }

        }

        stage('Run Container') {

            steps {

                sh 'sudo docker run -d -p 8081:80 --name poc-container devops-poc'

            }

        }

    }

}
 
