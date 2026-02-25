pipeline {
    agent any

    stages {
        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Backends') {
            steps {
                sh '''
                docker rm -f backend1 backend2 nginx || true
                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app
                '''
            }
        }

        stage('Run NGINX') {
            steps {
                sh '''
                docker run -d --name nginx \
                -p 8085:80 \
                --link backend1 \
                --link backend2 \
                -v $(pwd)/nginx/default.conf:/etc/nginx/nginx.conf \
                nginx
                '''
            }
        }
    }
}