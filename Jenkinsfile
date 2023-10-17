pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    chmod +x gradlew
                    ./gradlew build -x test
                '''
            }
        }
        stage('DockerSize') {
            steps {
                sh '''
                    docker stop eureka || true
                    docker rm eureka || true
                    docker rmi eureka || true
                    docker build -t eureka .
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d --name eureka --network gentledog eureka'
            }
        }
    }
}