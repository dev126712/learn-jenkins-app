pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm fund
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test'){
             agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps{
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }

        stage('DebianTest'){
            agent{
                docker{
                    image 'debian:stable'
                }
            }

            steps{
                sh '''
                    ping -c 5 8.8.8.8
                '''
            }
        }
    }
}
