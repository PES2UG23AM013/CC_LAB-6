pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Build NGINX Image') {
            steps {
                sh 'docker build -t custom-nginx nginx'
            }
        }

        stage('Run Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 nginx 2>/dev/null || true

                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app

                docker run -d --name nginx \
                -p 8085:80 \
                --link backend1 \
                --link backend2 \
                custom-nginx
                '''
            }
        }
    }
}