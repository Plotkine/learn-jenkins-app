pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine' // alpine is a very slim linux distribution, ideal for CI/CD
                    reuseNode true // synchronizing workspace
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Tests') {
            agent {
                docker {
                    image 'node:18-alpine' // alpine is a very slim linux distribution, ideal for CI/CD
                    reuseNode true // synchronizing workspace
                }
            }
            steps {
                    echo "Test stage"
                    sh 'touch ./build/index.html'
                    sh 'npm test'
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml' // this command comes from the Junit Jenkins plugin
                                           // https://plugins.jenkins.io/junit/
        }
    }
}
