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
        stage('E2E test') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.50.1-noble' // https://playwright.dev/docs/docker
                    reuseNode true // synchronizing workspace
                }
            }
            steps {
                    sh '''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright install
                    npx playwright test // start the E2E test using playwright
                    '''
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
