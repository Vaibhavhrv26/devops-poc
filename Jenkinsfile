pipeline {
    agent any

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {

        stage('Clone') {
            steps {
                echo 'Cloning repository'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    $SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.projectKey=devops-poc \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://51.20.84.128:9000 \
                    -Dsonar.login=squ_514c1f4e51cd0b104dce863a40681c8c6db729d7
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-poc .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f poc-container || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8081:80 --name poc-container devops-poc'
            }
        }
    }
}
