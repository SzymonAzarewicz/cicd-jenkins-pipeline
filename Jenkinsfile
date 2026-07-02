pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                sh 'git branch'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }
        stage('Docker Build') {
            steps {
                script{

                    if(env.BRANCH_NAME == 'main')
                    {
                        env.PORT = 3000
                    }
                    else if(env.BRANCH_NAME == 'dev')
                    {
                        env.PORT = 3001
                    }
                }
                sh "docker build -t node${env.PORT}:v1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                sh "docker run -p ${env.PORT}:${env.PORT} -d node${env.PORT}:v1.0"
            }
        }
    }
}
