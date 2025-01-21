pipeline {
    agent any

    stages {
        stage('First stage') {
            steps {
                sh '''
                echo "First stage" // this is executed on Jenkins agent
                rm test.txt
                ls -a
                '''
            }
        }
    }
}
