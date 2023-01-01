pipeline {
    agent any

    stages {
        stage('Verify Branch') {
             steps {
                echo "$GIT_BRANCH"
             }
          }
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Goodbye') {
            steps {
                echo 'Goodbye World'
            }
        }

    }
}
