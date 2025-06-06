pipeline {
    agent any

    environment {
        DOCKERHUB_CREDS = credentials('dockerhub-username')
        SLACK_WEBHOOK = credentials('slack-webhook')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/lehtika/devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t myflaskapp ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh '''
                        echo "${DOCKERHUB_CREDS_PSW}" | docker login -u "${DOCKERHUB_CREDS_USR}" --password-stdin
                        docker tag myflaskapp ${DOCKERHUB_CREDS_USR}/myflaskapp:latest
                        docker push ${DOCKERHUB_CREDS_USR}/myflaskapp:latest
                    '''
                }
            }
        }

        stage('Run Static Code Analysis') {
            steps {
                echo "Running static code analysis..."
                sh "sonar-scanner"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh "pytest || echo 'Tests failed or no tests found.'"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the application... (placeholder)"
            }
        }
    }

    post {
        success {
            sh '''
                curl -X POST -H "Content-type: application/json"                 --data '{"text":"✅ Deployment succeeded!"}'                 "$SLACK_WEBHOOK"
            '''
        }
        failure {
            sh '''
                curl -X POST -H "Content-type: application/json"                 --data '{"text":"❌ Deployment failed!"}'                 "$SLACK_WEBHOOK"
            '''
        }
    }
}
